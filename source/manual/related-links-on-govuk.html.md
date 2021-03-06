---
title: Related links on GOV.UK
parent: "/manual.html"
layout: manual_layout
type: learn
section: Related links
owner_slack: "#govuk-developers"
last_reviewed_on: 2019-07-22
review_in: 6 months
---

## Overview

Since July 2019, related links on GOV.UK have been supplemented by links generated through an automated machine learning pipeline. The first job in this pipeline uses data on how pages are linked together (the structural network) and analytics from users' behaviour on the site (the functional network) to create a set of most relevant related links for a subset of pages.

Once these links have been created, a second job ingests the links via the Publishing API to be shown to users navigating the site.

The code for the process of generating and ingesting related links can be found in the [govuk-related-links-recommender repository on GitHub](https://github.com/alphagov/govuk-related-links-recommender).

## When we show the new related links

Machine learning generated related links are created exclusively for Whitehall content, with a number of measures in place to ensure that we always show manually curated links set by publishers.

- Related links are only generated for a number of content types, with exclusions in place for content that should not be linked _from_, linked _to_, or both. These exclusions can be found at https://github.com/alphagov/govuk-related-links-recommender/tree/master/src/config.
- Generated related links are stored within the `suggested_ordered_related_items` property of a content item, while all existing and manually curated links continue to be stored within the `ordered_related_items` property.
- If links exist with `ordered_related_items` for a content item, we do not show generated related links.
- Requests need to have the header `Govuk-Use-Recommended-Related-Links` header set to `True` in order to show suggested related links - [this is set by the CDN for all requests](https://github.com/alphagov/govuk-cdn-config/blob/master/vcl_templates/www.vcl.erb#L238).


## Concourse pipeline details

Related links are generated and ingested via the following jobs, which are defined in the [govuk-related-links pipeline on Concourse](https://cd.gds-reliability.engineering/teams/govuk-tools/pipelines/govuk-related-links).

### `link-generation`

This job runs the process to generate new related links for a subset of pages on GOV.UK, via the `provision-generation-machine` and `run_link_generation` scripts, which in turn triggers the Python script `run_all.py`.

The related links generated from this process are stored in an S3 environment-specific `govuk-related-links` bucket.

Currently, this job is scheduled to run once every three weeks via a `time` resource attached to the production `run-generation-production` step.

### `link-ingestion`

This job runs the process of ingesting related links via the Publishing API.

Links are retrieved from the environment-specific S3 bucket mentioned previously and then fed (in batches) to the Publishing API. There is a 20 minute delay between batches.

Currently, this job is triggered manually after reviewing a spreadsheet of the generated related links; it will be scheduled to run automatically by the end of September 2019.

## Rolling back Links

Should we ever need to roll back any suggested related links, there are a number of ways we can do this.

### Links for individual pages

To rollback suggested related links for an individual page (to show the original related links), use the [Run rake task job on Jenkins](https://deploy.publishing.service.gov.uk/job/run-rake-task/) with the following parameters set:
  - `TARGET_APPLICATION: publishing-api`
  - `MACHINE_CLASS: publishing_api`
  - `RAKE_TASK: content:reset_related_links_for_pages['CONTENT_ID’]`, where `CONTENT_ID` is the content id of the page to remove suggested links from

### Links for certain document types

To exclude a document type or page from having links generated _to_ it, _from_ it, or both, [update the exclusions in the GitHub repository](https://github.com/alphagov/govuk-related-links-recommender/tree/master/src/config). Note: this will take effect from the _next_ time the related links generation process is run, and will not affect current links.

### Suspending all suggested related links

To immediately and temporarily stop showing all suggested related links (for example, if a problem has led to bad links being generated for a large percentage of content / high traffic content), you will need to update the CDN to set the `Govuk-Use-Recommended-Related-Links` header to `False` and then [deploy the CDN](https://deploy.publishing.service.gov.uk/job/Deploy_CDN/) for `vhost: www`.

The root cause of the problem should be investigated and a new set of related links generated and ingested through the pipeline, if possible. Should the fix not be immediate, we might consider re-ingesting an older batch of related links from S3.

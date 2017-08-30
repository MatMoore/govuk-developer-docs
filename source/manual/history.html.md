---
owner_slack: "#2ndline"
title: Technical history of GOV.UK
section: Basics
layout: manual_layout
parent: "/manual.html"
last_reviewed_on: 2017-07-12
review_in: 3 months
---

## 2010

The story of GDS starts with Martha Lane-Fox's letter to Francis Maude.

_Read more in ["A GDS Story 2010"](https://gds.blog.gov.uk/story-2010/)._

## 2011

On May 11th, 2011 the GOV.UK alpha is delivered after 12 weeks of building.

The work on the beta starts. In July, [publisher](https://github.com/alphagov/publisher/commit/30f441053c152be9d67f1ae8d3f44f1b5d972c33) and [panopticon](https://github.com/gds-attic/panopticon/commit/5ac69cbf048acd381c369465ca905f580dcdb85d) are created.
In September, the [first commits to frontend](https://github.com/alphagov/frontend/commit/89118e41a87f53b2253895e12593bd344878c4cf) appear. At the same time libraries like [govspeak](https://github.com/alphagov/govspeak) and [slimmer](https://github.com/alphagov/slimmer) are first developed.

The search engine [Rummager](https://github.com/alphagov/rummager/commit/e568c2ce003f4bd25979bffc719390847cfcf580) is created on November 1st, 2011. It uses Solr as a back-end.

At the same time the "Inside Government" project is underway. The main application of this is Whitehall, which sees the [first commit on 19 September 2011](https://github.com/alphagov/whitehall/commit/8fa277204b3859131640df556c2346cafcf57a8f).

_Read more in ["A GDS Story 2011"](https://gds.blog.gov.uk/story-2011/)._

## 2012

The beta of GOV.UK is [launched on 31 January](https://gds.blog.gov.uk/2012/01/31/this-is-why-we-are-here/). It is followed a month later by [the beta of Inside Government](https://gds.blog.gov.uk/2012/02/28/introducing-the-next-phase-of-the-gov-uk-beta/).

On April 2nd, the [first commit to "Sign-on-o-Tron II" appears](https://github.com/alphagov/signon/commit/d82798abe10189930f89803e959fb3494b956f9b). The app is later renamed to "Signon".

May sees first commit to [content api](https://github.com/alphagov/govuk_content_api/commit/38f285d8b571a83ce0f59b6fb8bd17a31d8c0060).

In September, [Rummager moves to Elasticsearch](https://github.com/alphagov/rummager/pull/23).

On 17 October, GOV.UK is formally live. On November 15th, [Inside Government](https://gds.blog.gov.uk/2012/11/15/launching-inside-government/) is live. The program known as "transition" starts, which aims to migrate hundreds of websites to GOV.UK.

_Read more in ["A GDS Story 2012"](https://gds.blog.gov.uk/story-2012/)._

## 2013

In April the [first commits to router](https://github.com/alphagov/router/commit/134c5663f69473dade40f641060a6a5a247e6231) are made. Router will replace the routing layer of GOV.UK, which is until then managed in Nginx configuration.

[Bouncer is created](https://github.com/alphagov/bouncer/commit/aa27534e5dd7bd8cb0afd6083aa05b7c0ba6829d) on 4 July 2013. It redirects old websites to their new new location on GOV.UK.
10 September, [the transition application](https://github.com/alphagov/transition/commit/723647d6c835332dc931a653d744aca8a4670b4a) is created to manage the redirects.

On 27 September 2013, the [first commit to Need API](https://github.com/alphagov/maslow/commit/959c5c506197c0534ba4ee5b40aa7646957ebef8) is made.

_Read more in ["A GDS Story 2013"](https://gds.blog.gov.uk/story-2013/)._

## 2014

The first [commit to content-store](https://github.com/alphagov/content-store/commit/2d3eb695b5214d4898df54cddfec4f6c5238938d) appears on 25 March 2014. In the same month, the [unified search API is debuted](https://github.com/alphagov/rummager/pull/204), which means Rummager can return search results for all applications.

In April 2014, [the "collections" app is created](https://github.com/alphagov/collections/pull/1) which will serve the specialist sector pages that are currently served from frontend.

In March, [specalist-publisher](https://github.com/alphagov/manuals-publisher) is first built.

In July [work starts on hmrc-manuals-api](https://github.com/alphagov/hmrc-manuals-api/pull/1).

In August 2014, [collections-publisher is created](https://github.com/alphagov/collections-publisher/pull/1) to manage specialist sectors.

The [publishing-api is created](https://github.com/alphagov/publishing-api/pull/1) on December 5th, 2014. It is created as a [Go application](https://github.com/alphagov/publishing-api/pull/3).

_Read more in ["A GDS Story 2014"](https://gds.blog.gov.uk/story-2014/)._

## 2015

Publishing API is [converted to Rails](https://github.com/alphagov/publishing-api/pull/48) in July 2015.

In October 2015, works starts on [service manual publisher](https://github.com/alphagov/service-manual-publisher/pull/1). It will replace the service manual, a Jekyll site.

Content Tagger is [created on November 15, 2016](https://github.com/alphagov/content-tagger/commit/326d87bc6ce0db6cdaa1a6be092a8c991d4b00bc). It will be used to tag content using the new publishing platform.

_Read more in ["A GDS Story 2015"](https://gds.blog.gov.uk/story-2015/)._

## 2016

In March, [service manual frontend](https://github.com/alphagov/service-manual-frontend/pull/1) is born.

In April 2016 works starts to rebuild specialist publisher. https://github.com/alphagov/specialist-publisher/issues/1.

In September, manuals-publisher is spun off from specialist-publisher.

Trade tariff moves off GOV.UK to the PaaS

_Read more in ["A GDS Story 2016"](https://gds.blog.gov.uk/story-2016/)._

## 2017

New navigation pages are built.

- Panopticon is retired.
- EFG moves off GOV.UK infrastructure.
- All editions are moved from Whitehall to government-frontend.

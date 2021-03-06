---
owner_slack: "#govuk-platform-health"
title: Troubleshoot data.gov.uk
section: data.gov.uk
layout: manual_layout
parent: "/manual.html"
last_reviewed_on: 2019-03-06
review_in: 6 months
---
[find]: apps/datagovuk_find
[publish]: apps/datagovuk_publish
[ckan]: apps/ckanext-datagovuk

## Different number of datasets in [CKAN] to [Find]

Determine the number of datasets in CKAN using the API.

```
https://data.gov.uk/api/3/search/dataset
```

Determine the number of datsets in the Publish Postgres database using the Rails console.

```
cf ssh publish-data-beta-production
/tmp/lifecycle/launcher /home/vcap/app 'rails console' ''
>>> Dataset.count
```

If these numbers match, but the number of datasets served on Find is still different, identify the number of published in the Publish Postgres database.

```
cf ssh publish-data-beta-production
/tmp/lifecycle/launcher /home/vcap/app 'rails console' ''
>>> Dataset.published.count
```

With the current set up, all datasets that are available through the CKAN API will be marked as public in the Publish Postgres database.  Therefore, if you get a different number of datasets, you should mark them all as published in the Publish Postgres database.

```
cf ssh publish-data-beta-production
/tmp/lifecycle/launcher /home/vcap/app 'rails console' ''
>>> Dataset.update(status: 'published')
```

A [reindex](/manual/data-gov-uk-operations.html#reindexing-find) must then be done to update the status with the Elastic instance that serves Find.

## Datasets published in CKAN are not appearing on Find

Check the Sidekiq queue (see [monitoring section](/manual/data-gov-uk-monitoring.html#sidekiq-publish)) length to ensure the queue length is not too long.  You should not be seeing more jobs than the number of datasets in CKAN.

If the queue is too long, you should clear the queue.  The next sync process will repopulate the queue with any relevant datasets that require updating.

## Harvesters not processing or seem stuck

The harvesting process runs as a single threaded program, if any harvesting
process crashes by raising an exception, it will take out the entire process.
We have configured Upstart to restart the process automatically, but if the
service keeps crashing, Upstart will decide it's unhealthy and stop that after
a while.

You can check whether the process is still running by checking if entries are
still being written to the log file on the `ckan` machine:

```bash
$ govukcli set-context production-aws
$ govukcli ssh ckan
```

```bash
$ sudo tail -f /var/log/ckan/procfile_harvester_fetch_consumer.err.log
```

Or you could check that the services are all showing as `started` on the `ckan`
machine:

```bash
$ sudo initctl list | grep harvester
```

If the server has stopped, there is a Fabric script that will restart it for
you. This script first checks whether the harvesting process is running or not
so if you suspect the process has crashed, you can run this script first to
try and restart the process.

```bash
$ fab aws_production class:ckan ckan.restart_harvester
```

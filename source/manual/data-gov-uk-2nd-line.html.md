---
owner_slack: "#govuk-platform-health"
title: Common 2nd line support requests for data.gov.uk
section: data.gov.uk
layout: manual_layout
parent: "/manual.html"
last_reviewed_on: 2018-12-21
review_in: 6 months
---
[ckan]: https://ckan.publishing.service.gov.uk
[dgu-docs]: https://guidance.data.gov.uk

This document details some of the requests that GOV.UK 2nd line support may receive regarding data.gov.uk.  [Separate documentation][dgu-docs] exists for publishers.

## Users and Publishers
Users have their own accounts and can login using either their username or email address.   A user can be a member of one or more publishing organisations, and can have either the role 'Admin' or 'Editor' for each organisation.  Users with 'Admin' status can add/remove users from the organisation for which they are an admin.  They only have 'admin' rights on their own organisation, contrasted to a 'sysadmin' who has admin rights across all organisations.

### Create a user account
There are two routes for creating an new account for a new user:

1. A publishing organisation's 'Admin' user(s) can invite new users to create an account.  The 'Admin' user should follow the instructions in [Assign users to publishers](#assign-users-to-publishers-setting-user-permissions), but login as themselves rather than a sysadmin user.  This route is also described in the [publisher guidance][dgu-docs].
2. A sysadmin user (e.g. 2nd line) can create an account for the new user.  Follow the instructions in [Assign users to publishers](#assign-users-to-publishers-setting-user-permissions) inputting the user's email address instead of their username.  An invite email is generated and sent to the publisher.

> An account should only be created if the user intends to publish on data.gov.uk.  Previously users have been able to register accounts to follow publishers.  This is no longer offered.

### Create a publishing organisation
1. Login to [CKAN][ckan] as a sysadmin user (credentials are available in the `govuk-secrets` password store, under `datagovuk/ckan`).
2. Click the 'Publishers' button in the header.
3. Click 'Add Publisher' and complete the form.
4. Ensure that a publishing user has been assigned as an 'Admin' for this organisation (this would normally be the person who makes the request, so they can then add further 'Editor' users without needing to contact support).

> Check the authenticity of a request before adding a user as a publishing admin (i.e. make sure they actually belong to the department they want to publish for, bearing in mind that some parent organisations may publish on behalf of child organisations, e.g. BEIS can publish for the Civil Nuclear Police Authority).

### Assign users to publishers (setting user permissions)
1. Login to [CKAN][ckan] as a sysadmin user (credentials are available in the `govuk-secrets` password store, under `datagovuk/ckan`).
2. Navigate to the relevant page for the publisher (use the 'Publishers' button in the header).
3. Click the 'Manage' button.
4. Click onto the 'Members' tab, then the 'Add Member' button.
5. Add the user's existing account, or enter their email address to send them an invite, ensuring you select the relevant role for the user (either admin or editor).

> Users should first be guided to request addition by an admin of their organisation, if possible.  This is to reduce the burden of these requests on the 2nd line team and to ensure only those with the correct authority are actually added as publishers.

> Check the authenticity of a request before adding a user as a publisher (i.e. make sure they actually belong to the department they want to publish for, bearing in mind that some parent organisations may publish on behalf of child organisations, e.g. BEIS can publish for the Civil Nuclear Police Authority).

## Datasets
### Delete or withdraw a dataset
Users are not permitted to remove their own datasets.  There are a [limited number of circumstances](https://guidance.data.gov.uk/deleting_datasets.html) in which a dataset will be withdrawn.  This is to be done by 2nd line, following a request from the publisher.  Datasets are never hard-deleted (known as "purged" in CKAN), instead they are marked as "withdrawn" (a soft-deletion), which removes them from the Find interface but allows them to be viewed through the publishing interface (CKAN).

> Before making any deletions, you should check that the person making the request actually belongs to the organisation who own the document (or are from a superseding department, e.g. someone from BEIS could request a withdrawal for a dataset published by BIS).

#### Deleting a single dataset
1. Login to [CKAN][ckan] as a sysadmin user (credentials are available in the `govuk-secrets` password store, under `datagovuk/ckan`).
2. Navigate to the relevant dataset (use the 'Datasets' button in the header).
3. Click the 'Manange' button.
4. Click the red 'Delete' button.
5. Once withdrawn, it will take up to 30 minutes to sync across to Find and clear the cache.

#### Bulk deleting datasets
Sometimes a publisher will request a large deletion of datasets.  In these cases, you can bulk withdraw the datasets using the instructions contained in the [supporting CKAN](/manual/data-gov-uk-supporting-ckan.html#deleting-a-dataset) documentation.  Refer to the instructions for 'Deleting a dataset' (which is a soft-delete).  **Do not purge the dataset - this is a hard-delete.**

## Harvesting
Harvesting is where publishers can automatically import their data to data.gov.uk without having to manually enter it into the web interface.  They can be set up to run automatically at specified periods, or run manually on-demand.

### Get the status of a harvester
1. Login to [CKAN][ckan] as a sysadmin user (credentials are available in the `govuk-secrets` password store, under `datagovuk/ckan`).
2. Navigate to the relevant harvester (use the 'Harvest' button in the header).
3. You will see a list of the datasets imported by this harvest source.
4. Click the 'Manage' button to get the status.
5. A summary of the current status will be shown.  Individual runs (and the error messages logged) can be access from the 'Jobs' tab.

### Restart a harvester
1. Login to [CKAN][ckan] as a sysadmin user (credentials are available in the `govuk-secrets` password store, under `datagovuk/ckan`).
2. Navigate to the relevant harvester (use the 'Harvest' button in the header).
3. You will see a list of the datasets imported by this harvest source.
4. Click the 'Manage' button.
5. If the harvester is currently running, click the 'Stop' button to stop it.  Once it has stopped, or if it is not currently running, click the 'Reharvest' button.  You will know if the harvester is running because the 'Reharvest' button will be disabled.

## Organogram Publishing
Organograms are files that allow the people structure of an organisation to be visualised.  They are split into two files: one for senior staff (grades SCS1, SCS2 and SCS3, or equivalent) and another for junior staff (all other grades).  The senior staff file is more detailed than the junior staff file, with staff names included for posts classified as grades SCS2 and SCS3.

Organograms are the only datasets in data.gov.uk where we host the data itself rather than linking to an external resource.  The data files are hosted in a S3 bucket (named `datagovuk-integration-ckan-organogram`, `datagovuk-staging-ckan-organogram` or `datagovuk-production-ckan-organogram`, depending on the environment).

### XLS to CSV Conversion
Publishers upload their organograms as a Excel (XLS) file that contains macros.  A script is run which converts these to the two CSV files (junior staff and senior staff).

> Publishers **must** select the correct 'Schema Vocabulary' for their organogram dataset (i.e. one of the two 'organisation structure' values) in order for the upload option to become available and for the XLS-to-CSV conversion to run.
---
owner_slack: "#govuk-2ndline"
title: Give a content designer access to GitHub
parent: "/manual.html"
layout: manual_layout
section: Tools
last_reviewed_on: 2018-06-01
review_in: 3 months
---

Content designers working on GOV.UK may need GitHub access to edit content
which is stored as code in an application, for example
[smart answers][smart-answers-github]. For this we have a
[dedicated GitHub team][github-team] that content designers can be added to.
When added to this team a content designer can create a branch within a GOV.UK
repository and open a pull request, however a developer will be required to
merge the request into the master branch.

Developers on 2nd Line may receive a ticket to add/remove content designers
from this access.

## Adding someone to the GitHub team

When a content designer joins they will need to be added to our monitoring
software and then can be added to the GitHub team. These are the steps to
follow:

1. Edit the [users.yml][] file in [govuk-user-reviewer][] with the following
   details for each designer: their name, GitHub username and role in
   GOV.UK - [example][user-example]
1. Raise this as a pull request
1. Once PR is merged email
   govuk-senior-tech-members@digital.cabinet-office.gov.uk
   with the GitHub usernames asking for the users to be added to
   https://github.com/orgs/alphagov/teams/gov-uk-content-designers
   which is the "GOV.UK Content Designers" GitHub team
1. Once added to the team the content designers will receive an invite that
   they will have to accept to join the team

## Removing someone from the GitHub team

When a content designer leaves GOV.UK they need to be removed from the GitHub
team to revoke their access.

First, check the [users.yml][] file in [govuk-user-reviewer][] to see if the
users are listed as having access. If they are not listed you do need to take
any further steps.

If they are listed follow these steps:

1. Email govuk-senior-tech-members@digital.cabinet-office.gov.uk
   with the GitHub usernames asking for the users to be removed from
   https://github.com/orgs/alphagov/teams/gov-uk-content-designers
   which is the "GOV.UK Content Designers" GitHub team
1. Edit the [users.yml][] file in [govuk-user-reviewer][] to remove the users
1. Raise this as a pull request
1. Once merged 2nd Line will be alerted if the users continues to have
   access despite having left

[smart-answers-github]: https://github.com/alphagov/smart-answers
[github-team]: https://github.com/orgs/alphagov/teams/gov-uk-content-designers
[users.yml]: https://github.com/alphagov/govuk-user-reviewer/blob/master/config/users.yml
[govuk-user-reviewer]: https://github.com/alphagov/govuk-user-reviewer
[user-example]: https://github.com/alphagov/govuk-user-reviewer/pull/114/commits/2bfff951faf1eb57b70022f90e926e51605e63a0
---
owner_slack: "#govuk-2ndline"
title: Use AWS on the command line
section: AWS accounts
layout: manual_layout
parent: "/manual.html"
last_reviewed_on: 2018-10-10
review_in: 3 months
---

💡 Before you can access something in AWS, you [need to set up your AWS account](/manual/set-up-aws-account.html).

---

## 1. Create `~/.aws/config`

1. You can find the `role_arn` in the ["Role ARN" table in the docs][secret-docs]
1. You can find your `mfa_serial` under "Assigned MFA device" in your user profile [in the AWS Console](/manual/aws-console-access.html):

  ![](images/aws-how-to-get-mfa.png)

Create `~/.aws/config`:

```ini
[profile govuk-<environment>]
source_profile = gds
role_arn = <Role ARN>
mfa_serial = <MFA ARN>

[profile gds]
region = eu-west-1
```

## 2. Create `~/.aws/credentials`

First, create a pair of [access keys][access-keys].

![](images/aws-how-to-get-access-keys.png)

Create `~/.aws/credentials`:

```ini
[gds]
aws_access_key_id = <access key id>
aws_secret_access_key = <secret access key>
```

## 3. Test it! 🚀

To test your configuration run:

```
aws --profile govuk-integration s3 ls
```

You should be prompted for an MFA token. If successful, you should receive some output.

[secret-docs]: https://github.com/alphagov/govuk-aws-data/blob/master/docs/govuk-aws-accounts.md
[access-keys]: https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys
# IAM Identity Provider<a name="idp"></a>

When you add SSO access to an AWS account, AWS SSO creates an IAM identity provider in each AWS account\. An IAM identity provider helps keep your AWS account secure because you don't have to distribute or embed long\-term security credentials, such as IAM access keys, in your application\.

## Repair the IAM Identity Provider<a name="repairidp"></a>

Use the following procedure to repair your identity provider in case it was deleted or modified\.

**To repair an identity provider for an AWS account**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. In the table, select the AWS account that is associated with the identity provider that you want to repair\.

1. On the AWS account details page, under **IAM identity provider**, choose **Repair identity provider**\.

## Remove the IAM Identity Provider<a name="removeidp"></a>

Use the following procedure to remove the IAM identity provider from AWS SSO\.

**To remove the IAM identity provider from AWS SSO**

1. Open the [AWS SSO management console](https://console.aws.amazon.com/singlesignon)

1. Choose **AWS accounts**

1. In the table select the AWS account that is associated with the IAM identity provider that you want to remove\.

1. On the **Details** page for the AWS account, under **IAM identity provider**, choose **Remove identity provider**\.
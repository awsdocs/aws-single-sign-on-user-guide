# IAM identity provider<a name="idp"></a>

When you add single sign\-on access to an AWS account, IAM Identity Center creates an IAM identity provider in each AWS account\. An IAM identity provider helps keep your AWS account secure because you don't have to distribute or embed long\-term security credentials, such as IAM access keys, in your application\.

## Repair the IAM identity provider<a name="repairidp"></a>

If you accidentally delete or modify your identity provider, you must manually reapply your user and group assignments\. Reapplying your user and group assignments recreates the identity provider\. For more information, see:
+ [Multi\-account permissions](manage-your-accounts.md)
+ [Application assignments](manage-your-applications.md)
# Multi\-account permissions<a name="manage-your-accounts"></a>

AWS IAM Identity Center \(successor to AWS Single Sign\-On\) is integrated with AWS Organizations so that administrators can pick multiple AWS accounts whose users need single sign\-on \(SSO\) access to the AWS Management Console\. These AWS accounts can be either the management account of the AWS Organizations or a member account\. A management account is the AWS account that is used to create the organization\. The rest of the accounts that belong to an organization are called member accounts\. For more information about the different account types, see [AWS Organizations Terminology and Concepts](http://docs.aws.amazon.com/organizations/latest/userguide/orgs_getting-started_concepts.html) in the *AWS Organizations User Guide*\.

After you assign access from the IAM Identity Center console, you can use permission sets to further refine what users can do in the AWS Management Console\. For more information about permission sets, see [Create and manage permission sets](permissionsets.md)\. 

Users follow a simple sign\-in process:

1. Users use their directory credentials to sign in to the AWS access portal\.

1. Users then choose the AWS account name that will give them federated access to the AWS Management Console for that account\.

1. Users who are assigned multiple permission sets choose which IAM role to use\.

Permission sets are a way to define permissions centrally in IAM Identity Center so that they can be applied to all of your AWS accounts\. These permission sets are provisioned to each AWS account as an IAM role\. The AWS access portal gives users the ability to retrieve temporary credentials for the IAM role of a given AWS account so they can use it for short\-term access to the AWS CLI\. For more information, see [Getting IAM role credentials for CLI access](howtogetcredentials.md)\.

To use IAM Identity Center with AWS Organizations, you must first enable IAM Identity Center, which grants IAM Identity Center the capability to create [Service\-linked roles](slrconcept.md) in each account in your organization\. These roles are not created until after you [Assign user access](useraccess.md#assignusers) for a given account\.

You can also connect an AWS account that is not part of your organization by setting up the account as a custom SAML 2\.0 application in IAM Identity Center\. In this scenario, you provision and manage the IAM roles and trust relationships that are required to enable SSO access\. For more information on how to do this, see [Add and configure a custom SAML 2\.0 application](samlapps.md#addconfigcustomapp)\.

**Topics**
+ [Delegated administration](delegated-admin.md)
+ [Single sign\-on access](useraccess.md)
+ [Create and manage permission sets](permissionsets.md)
+ [Resiliency design and Regional behavior](resiliency-regional-behavior.md)
# Manage SSO to Your AWS Accounts<a name="manage-your-accounts"></a>

AWS Single Sign\-On is integrated with AWS Organizations so that administrators can pick multiple AWS accounts whose users need single sign\-on \(SSO\) access to the AWS Management Console\. These AWS accounts can be either the master account of the AWS Organizations or a member account\. A master account is the AWS account that is used to create the organization\. The rest of the accounts that belong to an organization are called member accounts\. For more information about the different account types, see [AWS Organizations Terminology and Concepts](http://docs.aws.amazon.com/organizations/latest/userguide/orgs_getting-started_concepts.html) in the *AWS Organizations User Guide*\.

Once you assign access from the AWS SSO console, you can use permission sets to further refine what users can do in the AWS Management Console\. For more information about permission sets, see [Permission Sets](permissionsets.md)\. 

Users follow a simple sign\-in process:

1. Users use their directory credentials to sign in to the user portal\.

1. Users then choose the AWS account name that will give them federated access to the AWS Management Console for that account\.

1. Users who are assigned multiple permission sets choose which IAM role to use\.

Permission sets are a way to define permissions centrally in AWS SSO so that they can be applied to all of your AWS accounts\. These permission sets are provisioned to each AWS account as an IAM role\. The user portal gives users the ability to retrieve temporary credentials for the IAM role of a given AWS account so they can use it for short\-term access to the AWS CLI\. For more information, see [How to Get Credentials of an IAM Role for Use with CLI Access to an AWS Account](howtogetcredentials.md)\.

To use AWS SSO with AWS Organizations, you must first [Enable AWS SSO](step1.md), which grants AWS SSO the capability to create [Service\-Linked Roles](slrconcept.md) in each account in your AWS organization\. These roles are not created until after you [Assign User Access](useraccess.md#assignusers) for a given account\.

You can also connect an AWS account that is not part of your organization by setting up the account as a custom SAML application in AWS SSO\. In this scenario, you provision and manage the IAM roles and trust relationships that are required to enable SSO access\. For more information on how to do this, see [Add and Configure a Custom SAML 2\.0 Application](samlapps.md#addconfigcustomapp)\.

**Topics**
+ [Single Sign\-On Access](useraccess.md)
+ [Permission Sets](permissionsets.md)
+ [IAM Identity Provider](idp.md)
+ [Service\-Linked Roles](slrconcept.md)
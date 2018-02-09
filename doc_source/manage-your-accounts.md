# Manage SSO to Your AWS Accounts<a name="manage-your-accounts"></a>

AWS Single Sign\-On is integrated with AWS Organizations so that administrators can pick multiple AWS accounts whose users need single sign\-on \(SSO\) access to the AWS Management Console\. Once you assign access from the AWS SSO console, you can use permission sets to further refine what users can do in the AWS Management Console\. For more information about permission sets, see [Permission Sets](permissionsets.md)\. 

Users follow a simple sign\-in process:

1. Users use their directory credentials to sign in to the user portal\.

1. Users then choose the AWS account name that will give them federated access to the AWS Management Console for that account\.

1. Users who are assigned multiple permission sets choose which IAM role to use\.

Permission sets terminology is only used in the AWS SSO console; in the user portal, users instead see these as IAM roles\.

To use AWS SSO with AWS Organizations, you must first [Enable AWS SSO](step1.md), which grants AWS SSO the capability to create [Service\-Linked Roles](slrconcept.md) in each account in your AWS organization\. These roles are not created until after you [Assign User Access](useraccess.md#assignusers) for a given account\.

You can also connect an AWS account that is not part of your organization by setting up the account as a custom SAML application in AWS SSO\. In this scenario, you provision and manage the IAM roles and trust relationships that are required to enable SSO access\. For more information on how to do this, see [Add and Configure a Custom SAML 2\.0 Application](samlapps.md#addconfigcustomapp)\.


+ [Single Sign\-On Access](useraccess.md)
+ [Permission Sets](permissionsets.md)
+ [IAM Identity Provider](idp.md)
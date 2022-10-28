# Identity Center enabled applications<a name="app-enablement"></a>

IAM Identity Center provides support for integration by other AWS applications and services\. These applications can use IAM Identity Center to perform authentication and can access information about users and groups\. For example, a user might sign into an application that generates performance dashboards for resources that the user controls\. The user might then share the dashboard by looking up a group in IAM Identity Center\.

To enable this capability, IAM Identity Center provides an identity store which contains user and group attributes, excluding sign\-in credentials\. 

You can use either of the following methods to keep the users and groups in your IAM Identity Center identity store updated:
+ Use the IAM Identity Center identity store as your main identity source\. If you choose this method, you manage your users and groups from within the IAM Identity Center console or AWS CLI\.
+ Set up provisioning \(synchronization\) of users and groups coming from either of the following identity sources to your IAM Identity Center identity store:
  + **Active Directory** \- For more information, see [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)\.
  + **External identity provider** \- For more information, see [Connect to an external identity provider](manage-your-identity-source-idp.md)\.

  If you choose this provisioning method, you continue managing your users and groups from within your identity source and those changes would get synced to the IAM Identity Center identity store\.

Regardless of which identity source you choose, IAM Identity Center has the ability to share the user and group information with Identity Center enabled applications\. This capability makes it possible to connect an identity source to IAM Identity Center once and then share identity information with multiple applications in the AWS Cloud\. This eliminates the need to set up federation and identity provisioning with each application independently\. This sharing feature also makes it easy to give users in your workforce access to many applications in different AWS accounts\.

## Considerations for sharing identity information in AWS accounts<a name="considerations-app-enablement"></a>

The attributes contained in IAM Identity Center are the basic attributes commonly used across applications\. These attributes include information such as first and last name, phone number, email address, address, and preferred language\. You might want to consider which applications and which accounts can use this personally identifiable information\.

To control access to this information, you have two options\. First, you can choose to enable access in only the AWS Organizations management account or in all AWS Organizations accounts\. Second, you can use service control policies \(SCPs\) to control which applications can access the information in which AWS Organizations accounts\. For example, if you enable access in the AWS Organizations management account only, then applications in member accounts have no access to the information\. However, if you enable access in all accounts, you can use SCPs to disallow access by all applications except those you want to permit\.

## Allow Identity Center enabled applications in AWS accounts<a name="enable-app-enablement"></a>

When you enable IAM Identity Center for the first time, AWS allows use of Identity Center enabled applications automatically in all AWS Organizations accounts\. To constrain applications, you must implement SCPs\.

If you enabled IAM Identity Center prior to November 25, 2019, IAM Identity Center disables the use of Identity Center enabled applications in all AWS Organizations accounts\. To use Identity Center enabled applications, you must enable them in the management account and optionally enable them in member accounts\. If you enable them in the management account only, you can enable them in member accounts in the future\. To enable these applications, use the **Enable access** option in the IAM Identity Center **Settings** page in the Identity Center enabled applications section\.
# Users, groups, and provisioning<a name="users-groups-provisioning"></a>

IAM Identity Center manages access to all your AWS Organizations accounts, Identity Center enabled applications, and other business applications that support the Security Assertion Markup Language \(SAML\) 2\.0 standard\.

## User name and email address uniqueness<a name="username-email-unique"></a>

When working in IAM Identity Center, users must be uniquely identifiable\. IAM Identity Center implements a user name that is the primary identifier for your users\. Although most people set the user name equal to a user’s email address, IAM Identity Center and the SAML standard do not require this\. However, a large percentage of SAML\-based applications use an email address as the unique identifier for users\. They obtain this from assertions that a SAML identity provider sends during authentication\. Such applications depend upon the uniqueness of email addresses for each user\. As such, IAM Identity Center allows you to specify something other than an email address for user sign\-in\. IAM Identity Center requires that all user names and email addresses for your users are non\-NULL and unique\.

## Groups<a name="groups-concept"></a>

Groups are a logical combination of users that you define\. You can create groups and add users to the groups\. IAM Identity Center does not support adding a group to a group \(nested groups\)\. Groups are useful when assigning access to AWS accounts and applications\. Rather than assign each user individually, you give permissions to a group\. Later, as you add or remove users from a group, the user dynamically gets or loses access to accounts and applications that you assigned to the group\.

## User and group provisioning<a name="user-group-provision"></a>

You can create users and groups directly in IAM Identity Center, or work with users and groups you have in Active Directory or an another external identity provider\. Before IAM Identity Center can be used to assign users and groups access permissions in an AWS account, IAM Identity Center must first be aware of the users and groups\. Similarly, Identity Center enabled applications can work with users and groups for which IAM Identity Center is aware\. Provisioning is the process of making user and group information available for use by IAM Identity Center and Identity Center enabled applications\.

Provisioning in IAM Identity Center varies based on the identity source that you use\. For more information, see [Manage your identity source](manage-your-identity-source.md)\.
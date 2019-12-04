# Users, Groups, and Provisioning<a name="users-groups-provisioning"></a>

AWS SSO manages access to all your AWS Organizations accounts, AWS SSO\-integrated applications, and other business applications that support the Security Assertion Markup Language \(SAML\) 2\.0 standard\.

## User name and email address uniqueness<a name="username-email-unique"></a>

When working in AWS SSO, users must be uniquely identifiable\. AWS SSO implements a user name that is the primary identifier for your users\. Although most people set the user name equal to a user’s email address, AWS SSO and the SAML standard do not require this\. However, a large percentage of SAML\-based applications use an email address as the unique identifier for users\. They obtain this from assertions that a SAML identity provider sends during authentication\. Such applications depend upon the uniqueness of email addresses for each user\. As such, AWS SSO allows you to specify something other than an email address for user sign\-in\. AWS SSO requires that all user names and email addresses for your users are non\-NULL and unique\.

## Groups<a name="groups-concept"></a>

Groups are a logical combination of users that you define\. You can create groups and add users to the groups\. AWS SSO does not support adding a group to a group \(nested groups\)\. Groups are useful when assigning access to AWS accounts and applications\. Rather than assign each user individually, you give permissions to a group\. Later, as you add or remove users from a group, the user dynamically gets or loses access to accounts and applications that you assigned to the group\.

## User and group provisioning<a name="user-group-provision"></a>

You can create users and groups directly in AWS SSO, or work with users and groups you have in Active Directory or an external identity provider\. In order for AWS SSO to assign users and groups for permissions in an AWS SSO account, AWS SSO must first be aware of the users and groups\. Similarly, AWS SSO\-integrated applications can work with users and groups for which AWS SSO is aware\. Provisioning is the process of making user and group information available for use by AWS SSO and AWS SSO\-integrated applications\.

Provisioning in AWS SSO varies based on the identity source you use\. For more information, see [Manage Your Identity Source](manage-your-identity-source.md)\.
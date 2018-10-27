# Manage Your AWS SSO Directory<a name="manage-your-directory-sso"></a>

AWS Single Sign\-On provides you with a default directory where you can store your users and groups\. If you choose to store them in AWS SSO, all you need to do is the following:

1. Create your users and groups\.

1. Add your users as members to the groups\. 

1. Assign the groups with the desired level of access to your AWS accounts and applications\. 

**Note**  
Users and groups that you create in your AWS SSO directory are available in AWS SSO only\. 

If you prefer to manage users in AWS Managed Microsoft AD, you can discontinue use of your AWS SSO directory at any time and instead connect AWS SSO to your Microsoft AD using AWS Directory Service\. For more information, see [Connect to Your Microsoft AD Directory](manage-your-directory-connected.md)\.

**Topics**
+ [Add Users](addusers.md)
+ [Add Groups](addgroups.md)
+ [Add Users to Groups](adduserstogroups.md)
+ [Edit User Properties](edituser.md)
+ [Disable a User](disableuser.md)
+ [Reset a User Password](resetuserpwd.md)
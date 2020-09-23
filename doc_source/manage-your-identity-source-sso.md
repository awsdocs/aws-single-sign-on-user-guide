# Manage Identities in AWS SSO<a name="manage-your-identity-source-sso"></a>

AWS Single Sign\-On provides you with a default store where you can store your users and groups\. If you choose to store them in AWS SSO, all you need to do is the following:
+ Create your users and groups\.
+ Add your users as members to the groups\. 
+ Assign the groups with the desired level of access to your AWS accounts and applications\. 

If you prefer to manage users in AWS Managed Microsoft AD, you can discontinue use of your AWS SSO store at any time and instead connect AWS SSO to your Microsoft AD using AWS Directory Service\. For more information, see [Connect to Your Microsoft AD Directory](manage-your-identity-source-ad.md)\.

If you prefer to manage users in an external identity provider \(IdP\), you can connect AWS SSO to your IdP and enable automatic provisioning\. For more information, see [Connect to Your External Identity Provider](manage-your-identity-source-idp.md)\.

**Note**  
When identities are deleted in the AWS SSO store, corresponding assignments also get deleted in AWS SSO\. However in Microsoft AD, when identities are deleted \(either in AD or the synced in identities\), corresponding assignments are not deleted\. 

## Provisioning When Users are in AWS SSO<a name="provision-users-sso"></a>

When you create users and groups directly in AWS SSO, provisioning is automatic\. These identities are immediately available for use in making assignments and for use by AWS SSO\-integrated applications\. For more information, see [User and group provisioning](users-groups-provisioning.md#user-group-provision)\.

**Topics**
+ [Provisioning When Users are in AWS SSO](#provision-users-sso)
+ [Add Users](addusers.md)
+ [Add Groups](addgroups.md)
+ [Add Users to Groups](adduserstogroups.md)
+ [Edit User Properties](edituser.md)
+ [Disable a User](disableuser.md)
+ [Reset a User Password](resetuserpwd.md)
+ [Password Requirements for the AWS SSO Identity Store](password-requirements.md)
+ [Supported User and Group Attributes](supported-attributes.md)
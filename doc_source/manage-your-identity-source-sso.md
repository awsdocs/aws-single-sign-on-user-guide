# Manage identities in AWS SSO<a name="manage-your-identity-source-sso"></a>
+ Create your users and groups\.
+ Add your users as members to the groups\. 
+ Assign the groups with the desired level of access to your AWS accounts and applications\. 

If you prefer to manage users in AWS Managed Microsoft AD, you can discontinue use of your AWS SSO store at any time and instead connect AWS SSO to your Microsoft AD using AWS Directory Service\. For more information, see [Connect to your Microsoft AD directory](manage-your-identity-source-ad.md)\.

If you prefer to manage users in an external identity provider \(IdP\), you can connect AWS SSO to your IdP and enable automatic provisioning\. For more information, see [Connect to your external identity provider](manage-your-identity-source-idp.md)\.

**Note**  
When identities are deleted in the AWS SSO identity store, corresponding assignments also get deleted in AWS SSO\. However in Microsoft AD, when identities are deleted \(either in AD or the synced in identities\), corresponding assignments are not deleted\. 

## Provisioning when users are in AWS SSO<a name="provision-users-sso"></a>

When you create users and groups directly in AWS SSO, provisioning is automatic\. These identities are immediately available for use in making assignments and for use by AWS SSO\-integrated applications\. For more information, see [User and group provisioning](users-groups-provisioning.md#user-group-provision)\.

**Topics**
+ [Provisioning when users are in AWS SSO](#provision-users-sso)
+ [Add users](addusers.md)
+ [Add groups](addgroups.md)
+ [Add users to groups](adduserstogroups.md)
+ [Edit user properties](edituser.md)
+ [Disable user access](disableuser.md)
+ [Reset a user password](resetuserpwd.md)
+ [Password requirements when managing identities in AWS SSO](password-requirements.md)
+ [Supported user and group attributes](supported-attributes.md)
+ [Using predefined attributes from the AWS SSO identity store for access control in AWS](using-predefined-attributes.md)
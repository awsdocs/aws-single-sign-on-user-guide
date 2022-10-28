# Manage identities in IAM Identity Center<a name="manage-your-identity-source-sso"></a>
+ Create your users and groups\.
+ Add your users as members to the groups\. 
+ Assign the groups with the desired level of access to your AWS accounts and applications\. 

If you prefer to manage users in AWS Managed Microsoft AD, you can stop using your Identity Center directory at any time and instead connect IAM Identity Center to your directory in Microsoft AD by using AWS Directory Service\. For more information, see [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)\.

If you prefer to manage users in an external identity provider \(IdP\), you can connect IAM Identity Center to your IdP and enable automatic provisioning\. For more information, see [Connect to an external identity provider](manage-your-identity-source-idp.md)\.

**Note**  
When identities are deleted in the Identity Center directory, corresponding assignments also get deleted in IAM Identity Center\. However in Microsoft AD, when identities are deleted \(either in AD or the synced in identities\), corresponding assignments are not deleted\. 

To manage users and groups in the IAM Identity Center store, AWS supports the API operations listed in [Identity Center Actions](https://docs.aws.amazon.com/singlesignon/latest/IdentityStoreAPIReference/API_Operations.html)\.

**Note**  
If you use an external identity provider or Active Directory as your identity source, we recommend that you use Create, Update, and Delete APIs with caution\. IAM Identity Center does not support outbound synchronization, so your identity source does not automatically update with the changes that you make to users or groups using these APIs\.

## Provisioning when users are in IAM Identity Center<a name="provision-users-sso"></a>

When you create users and groups directly in IAM Identity Center, provisioning is automatic\. These identities are immediately available for use in making assignments and for use by Identity Center enabled applications\. For more information, see [User and group provisioning](users-groups-provisioning.md#user-group-provision)\.

**Topics**
+ [Provisioning when users are in IAM Identity Center](#provision-users-sso)
+ [Add users](addusers.md)
+ [Add groups](addgroups.md)
+ [Add users to groups](adduserstogroups.md)
+ [Edit user properties](edituser.md)
+ [Reset a user password](resetuserpwd.md)
+ [Send email OTP for users created from API](userswithoutpwd.md)
+ [Password requirements when managing identities in IAM Identity Center](password-requirements.md)
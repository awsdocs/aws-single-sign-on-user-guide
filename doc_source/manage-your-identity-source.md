# Manage Your Identity Source<a name="manage-your-identity-source"></a>

You can configure your identity source in AWS SSO to determine where your users and groups are stored\. Once configured, you can then look up users or groups in your store to grant them single sign\-on access to AWS accounts, cloud applications, or both\.

AWS SSO automatically provides you with a store by default, which you can use to manage your users and groups within AWS SSO\. If you choose to store them in AWS SSO, create your users and groups and assign their level of access to your AWS accounts and applications\. Alternatively, you can choose to [Connect to Your External Identity Provider](manage-your-identity-source-idp.md) using Azure Active Directory, or [Connect to Your Microsoft AD Directory](manage-your-identity-source-ad.md) using AWS Directory Service\.

**Note**  
AWS SSO does not support SAMBA4\-based Simple AD as a connected directory\.

**Topics**
+ [Considerations for Changing Your Identity Source](manage-your-identity-source-considerations.md)
+ [Change Your Identity Source](manage-your-identity-source-change.md)
+ [Manage Identities in AWS SSO](manage-your-identity-source-sso.md)
+ [Connect to Your Microsoft AD Directory](manage-your-identity-source-ad.md)
+ [Connect to Your External Identity Provider](manage-your-identity-source-idp.md)
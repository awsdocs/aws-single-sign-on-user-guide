# Manage your identity source<a name="manage-your-identity-source"></a>

Your identity source in AWS SSO defines where your users and groups are managed\. Once configured, you can then look up users or groups in your store to grant them single sign\-on access to AWS accounts, cloud applications, or both\.

You can have only one identity source per AWS organization\. You can choose one of the following as your identity source: 


+ **AWS SSO identity store –** When you enable AWS SSO for the first time, it is automatically configured with an AWS SSO identity store as your default identity source\. This is where you create your users and groups, and assign their level of access to your AWS accounts and applications\. 
+ **Active Directory –** Choose this option if you want to continue managing users in either your self\-managed Active Directory \(AD\) or your AWS Managed Microsoft AD directory using AWS Directory Service\. 
+ **External identity provider –** Choose this option if you prefer to manage users in an external identity provider \(IdP\) such as Okta or Azure Active Directory\. 

**Note**  
AWS SSO does not support SAMBA4\-based Simple AD as an identity source\.

**Topics**
+ [Considerations for changing your identity source](manage-your-identity-source-considerations.md)
+ [Change your identity source](manage-your-identity-source-change.md)
+ [Manage identities in AWS SSO](manage-your-identity-source-sso.md)
+ [Connect to your Microsoft AD directory](manage-your-identity-source-ad.md)
+ [Connect to your external identity provider](manage-your-identity-source-idp.md)
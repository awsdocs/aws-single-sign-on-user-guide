# Manage your identity source<a name="manage-your-identity-source"></a>

Your identity source in IAM Identity Center defines where your users and groups are managed\. After you configure your identity source, you can look up users or groups to grant them single sign\-on access to AWS accounts, cloud applications, or both\.

You can have only one identity source per organization in AWS Organizations\. You can choose one of the following as your identity source: 


+ **Identity Center directory –** When you enable IAM Identity Center for the first time, it is automatically configured with an Identity Center directory as your default identity source\. This is where you create your users and groups, and assign their level of access to your AWS accounts and applications\. 
+ **Active Directory –** Choose this option if you want to continue managing users in either your self\-managed directory in Active Directory \(AD\) or your AWS Managed Microsoft AD directory using AWS Directory Service\. 
+ **External identity provider –** Choose this option if you want to manage users in an external identity provider \(IdP\) such as Okta or Azure Active Directory\. 

**Note**  
IAM Identity Center does not support SAMBA4\-based Simple AD as an identity source\.

**Topics**
+ [Considerations for changing your identity source](manage-your-identity-source-considerations.md)
+ [Change your identity source](manage-your-identity-source-change.md)
+ [Manage sign\-in and attribute use for all identity source types](manage-your-identity-source-attribute-use.md)
+ [Manage identities in IAM Identity Center](manage-your-identity-source-sso.md)
+ [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)
+ [Connect to an external identity provider](manage-your-identity-source-idp.md)
# Step 2: Choose your identity source<a name="get-started-choose-identity-source"></a>

Your identity source in IAM Identity Center defines where your users and groups are managed\. You can choose one of the following as your identity source: 


+ **Identity Center directory –** When you enable IAM Identity Center for the first time, it is automatically configured with an Identity Center directory as your default identity source\. This is where you create your users and groups, and assign their level of access to your AWS accounts and applications\. 
+ **Active Directory –** Choose this option if you want to continue managing users in either your AWS Managed Microsoft AD directory using AWS Directory Service or your self\-managed directory in Active Directory \(AD\)\. 
+ **External identity provider –** Choose this option if you want to manage users in an external identity provider \(IdP\) such as Okta or Azure Active Directory\. 

After you enable IAM Identity Center, you must choose your identity source\. The identity source that you choose determines where IAM Identity Center searches for users and groups that need single sign\-on access\. After you choose your identity source, you'll create or specify a user and assign them administrative permissions to your AWS account\.

**Important**  
If you're already managing users and groups in Active Directory or an external identity provider \(IdP\), we recommend that you consider connecting this identity source when you enable IAM Identity Center and choose your identity source\. This should be done before you create any users and groups in the default Identity Center directory and make any assignments\. If you're already managing users and groups in one identity source in IAM Identity Center, changing to a different identity source might remove all user and group assignments that you configured in IAM Identity Center\. If this occurs, all users, including the administrative user in IAM Identity Center, will lose single sign\-on access to their AWS accounts and applications\. For more information, see [Considerations for changing your identity source](manage-your-identity-source-considerations.md)\.

**Topics**
+ [Connect Active Directory or an external IdP and specify a user](get-started-connect-id-source-ad-idp-specify-user.md)
+ [Use the default directory and create a user in IAM Identity Center](get-started-use-identity-center-directory-create-user-in-identity-center.md)
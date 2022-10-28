# Step 3: Choose your identity source and create an IAM Identity Center administrative user<a name="get-started-choose-identity-source"></a>

After you enable IAM Identity Center and create a permission set, you must choose your identity source\. The identity source that you choose determines where IAM Identity Center searches for users and groups that need single sign\-on access\. After you choose your identity source, you'll create or specify a user and assign them administrative permissions to your AWS account\.

**Important**  
If you're already managing users and groups in Active Directory or an external identity provider \(IdP\), we recommend that you consider connecting this identity source when you enable IAM Identity Center and choose your identity source\. This should be done before you create any users and groups in the default Identity Center directory and make any assignments\. If you're already managing users and groups in one identity source, changing to a different identity source might remove all user and group assignments that you configured in IAM Identity Center\. If this occurs, all users, including the administrative user in IAM Identity Center, will lose single sign\-on access to their AWS accounts and applications\. For more information, see [Considerations for changing your identity source](manage-your-identity-source-considerations.md)\.

**Topics**
+ [Connect Active Directory or an external IdP](get-started-connect-id-source-ad-idp.md)
+ [Use the default Identity Center directory](get-started-use-identity-center-directory.md)
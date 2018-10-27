# Manage Your Directory<a name="manage-your-directory"></a>

You can configure your directory in AWS SSO to determine where your users and groups are stored\. Once configured, you can then look up users or groups in your directory to grant them single sign\-on access to AWS accounts, cloud applications, or both\.

AWS SSO automatically provides you with a directory by default, which you can use to manage your users and groups within AWS SSO\. If you choose to store them in AWS SSO, create your users and groups and assign their level of access to your AWS accounts and applications\. Alternatively, you can choose to [Connect AWS SSO to an On\-Premises Active Directory](connectonpremad.md) or [Connect AWS SSO to an AWS Managed Microsoft AD Directory](connectawsad.md) using AWS Directory Service\.

**Note**  
AWS SSO does not support SAMBA4\-based Simple AD as a connected directory\.

**Topics**
+ [Manage Your AWS SSO Directory](manage-your-directory-sso.md)
+ [Connect to Your Microsoft AD Directory](manage-your-directory-connected.md)
+ [Change Your Directory Type](manage-your-directory-change.md)
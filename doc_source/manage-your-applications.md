# Application assignments<a name="manage-your-applications"></a>

With AWS IAM Identity Center \(successor to AWS Single Sign\-On\), you can easily control who can have single sign\-on access to your cloud applications\. Users get one\-click access to these applications after they use their directory credentials to sign in to their AWS access portal\.

IAM Identity Center securely communicates with these applications through a trusted relationship between IAM Identity Center and the application's service provider\. This trust is created when you add the application from the IAM Identity Center console and configure it with the appropriate metadata for both IAM Identity Center and the service provider\. 

After the application has been successfully added to the IAM Identity Center console, you can manage which users or groups need permissions to the application\. By default, when you add an application, no users are assigned to the application\. In other words, newly added applications in the IAM Identity Center console are inaccessible until you assign users to them\. IAM Identity Center supports the following applications types:
+ Identity Center enabled applications
+ Cloud applications
+ Custom Security Assertion Markup Language \(SAML 2\.0\) applications

You can also grant your employees access to the AWS Management Console for a given AWS account in your organization\. For more information on how to do this, see [Multi\-account permissions](manage-your-accounts.md)\.

The following sections explain how to configure user access to your AWS applications and third\-party software as a service \(SaaS\) applications\. You can also configure any custom applications that support identity federation with SAML 2\.0\. 

**Topics**
+ [Identity Center enabled applications](awsapps.md)
+ [Cloud applications](saasapps.md)
+ [Custom SAML 2\.0 applications](samlapps.md)
+ [Manage IAM Identity Center certificates](managecerts.md)
+ [Application properties](appproperties.md)
+ [Assign user access](assignuserstoapp.md)
+ [Remove user access](removeaccessfromapp.md)
+ [Map attributes in your application to IAM Identity Center attributes](mapawsssoattributestoapp.md)
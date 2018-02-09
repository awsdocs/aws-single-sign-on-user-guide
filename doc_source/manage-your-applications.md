# Manage SSO to Your Applications<a name="manage-your-applications"></a>

With AWS Single Sign\-On you can easily control who should have single sign\-on \(SSO\) access to your cloud applications\. Users get one\-click access to these applications once they sign in to their user portal with their directory credentials\.

AWS SSO securely communicates with these applications through a trusted relationship between AWS SSO and the application's service provider\. This trust is created when you add the application using the AWS SSO console and configure it with the appropriate metadata for both the AWS SSO service and the service provider\. 

Once the application has been successfully added to the AWS SSO console, you can then manage which users or groups need permissions to the application\. By default, when you add an application no users are assigned to the application\. In other words, newly added applications in the AWS SSO console are inaccessible until you assign users to them\. AWS SSO supports the following applications types:

+ Cloud applications

+ Custom Security Assertion Markup Language \(SAML 2\.0\) applications

You can also grant your employees access to the AWS Management Console for a given AWS account in your organization\. For more information on how to do this, see [Manage SSO to Your AWS Accounts](manage-your-accounts.md)\.

The following sections explain how to configure user access to your third\-party software as a service \(SaaS\) applications and any custom applications that support identity federation with SAML 2\.0\. 


+ [Cloud Applications](saasapps.md)
+ [Custom SAML 2\.0 Applications](samlapps.md)
+ [Assign User Access](assignuserstoapp.md)
+ [Remove User Access](removeaccessfromapp.md)
+ [Map Attributes in Your Application to AWS SSO Attributes](mapawsssoattributestoapp.md)
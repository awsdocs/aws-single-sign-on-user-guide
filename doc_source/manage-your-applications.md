# Manage SSO to Your Applications<a name="manage-your-applications"></a>

With AWS Single Sign\-On, you can easily control who can have single sign\-on \(SSO\) access to your cloud applications\. Users get one\-click access to these applications after they use their directory credentials to sign in to their user portal\.

AWS SSO securely communicates with these applications through a trusted relationship between AWS SSO and the application's service provider\. This trust is created when you add the application from the AWS SSO console and configure it with the appropriate metadata for both AWS SSO and the service provider\. 

After the application has been successfully added to the AWS SSO console, you can manage which users or groups need permissions to the application\. By default, when you add an application, no users are assigned to the application\. In other words, newly added applications in the AWS SSO console are inaccessible until you assign users to them\. AWS SSO supports the following applications types:
+ AWS SSO\-integrated applications
+ Cloud applications
+ Custom Security Assertion Markup Language \(SAML 2\.0\) applications

You can also grant your employees access to the AWS Management Console for a given AWS account in your organization\. For more information on how to do this, see [Manage SSO to Your AWS Accounts](manage-your-accounts.md)\.

The following sections explain how to configure user access to your AWS applications and third\-party software as a service \(SaaS\) applications\. You can also configure any custom applications that support identity federation with SAML 2\.0\. 

**Topics**
+ [AWS SSO\-Integrated Applications](awsapps.md)
+ [Cloud Applications](saasapps.md)
+ [Custom SAML 2\.0 Applications](samlapps.md)
+ [Manage AWS SSO Certificates](managecerts.md)
+ [Application Properties](appproperties.md)
+ [Assign User Access](assignuserstoapp.md)
+ [Remove User Access](removeaccessfromapp.md)
+ [Map Attributes in Your Application to AWS SSO Attributes](mapawsssoattributestoapp.md)
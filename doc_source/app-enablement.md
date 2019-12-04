# AWS SSO\-Integrated Application Enablement<a name="app-enablement"></a>

AWS SSO provides support for integration by other AWS applications and services\. These applications can use AWS SSO to perform authentication and can access information about users and groups\. For example, a user might sign into an application that generates performance dashboards for resources that the user controls\. The user might then share the dashboard by looking up a group in AWS SSO\.

To enable this capability, AWS SSO contains an identity store that contains user and group attributes, excluding sign\-in credentials\. These attributes have several things in common:
+ Synchronized \(provisioned\) automatically via just\-in\-time \(JIT\) provisioning when you use Microsoft Active Directory as your identity source
+ Provisioned continuously and automatically when you configure a System for Cross\-domain Identity Management \(SCIM\) 2\.0 connection to AWS SSO
+ Provisioned manually from the AWS SSO console when you use an external identity provider without SCIM 2\.0 automatic provisioning
+ Created in AWS SSO when you use AWS SSO as your identity source

Regardless of what you use as your identity source, AWS SSO has the ability to share the user and group information with AWS SSO\-integrated applications\. This capability makes it possible to connect an identity source to AWS SSO once and then share identity information with multiple applications in the AWS Cloud\. This eliminates the need to set up federation and identity provisioning with each application independently\. This sharing feature also makes it easy to give your workforce \(employees\) access to many applications in different AWS accounts\.

## Considerations for Sharing Identity Information in AWS Accounts<a name="considerations-app-enablement"></a>

The attributes contained in AWS SSO are the basic attributes commonly used across applications\. These attributes include information such as first and last name, phone number, email address, address, and preferred language\. You might want to consider which applications and which accounts can use this personally identifiable information\.

To control access to this information, you have two options\. First, you can choose to enable access in only the AWS Organizations master account or in all AWS Organizations accounts\. Second, you can use service control policies \(SCPs\) to control which applications can access the information in which AWS Organizations accounts\. For example, if you enable access in the AWS Organizations master account only, then applications in member accounts have no access to the information\. However, if you enable access in all accounts, you can use SCPs to disallow access by all applications except those you want to permit\.

## Enable AWS SSO\-Integrated Applications in AWS Accounts<a name="enable-app-enablement"></a>

When you enable AWS SSO for the first time, AWS enables use of integrated applications automatically in all AWS Organizations accounts\. To constrain applications, you must implement SCPs\.

If you enabled AWS SSO prior to November 25, 2019, AWS SSO disables the use of integrated applications in all AWS Organizations accounts\. To use AWS SSO\-integrated applications, you must enable them in the master account and optionally enable them in member accounts\. If you enable them in the master account only, you can enable them in member accounts in the future\. To enable these applications, use the **Enable access** option in the AWS SSO **Settings** page in the AWS SSO\-integrated applications section\.
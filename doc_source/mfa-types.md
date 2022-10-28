# MFA types<a name="mfa-types"></a>

MFA types represent the different mechanisms that users will be able to register and provide as secondary means of verifying their identity when challenged\. All MFA types are supported for both browser\-based console access as well as using the AWS CLI v2 with IAM Identity Center\. 

IAM Identity Center MFA provides support to enable one or both of the following types of client\-side authentication types\. 
+ Authenticator apps
+ Security keys and built\-in authenticators

Alternatively, you can also use your own RADIUS implementation connected through AWS Managed Microsoft AD\. For more information, see [RADIUS MFA](about-radius.md)\.

For more information, see [Configure MFA types](how-to-configure-mfa-types.md)\.

**Topics**
+ [Authenticator apps](mfa-types-apps.md)
+ [Security keys and built\-in authenticators](mfa-types-keys.md)
+ [RADIUS MFA](about-radius.md)
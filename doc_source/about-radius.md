# RADIUS MFA<a name="about-radius"></a>

[Remote Authentication Dial\-In User Service \(RADIUS\)](https://en.wikipedia.org/wiki/RADIUS) is an industry\-standard client\-server protocol that provides authentication, authorization, and accounting management so users can connect to network services\. AWS Directory Service includes a RADIUS client that connects to the RADIUS server upon which you have implemented your MFA solution\. For more information, see [Enable Multi\-Factor Authentication for AWS Managed Microsoft AD](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_mfa.html)\. 

You can use either RADIUS MFA or MFA in AWS SSO for user sign\-ins to the user portal, but not both\. MFA in AWS SSO is an alternative to RADIUS MFA in cases where you want AWS native two\-factor authentication for access to the portal\.

When you enable MFA in AWS SSO, your users need an MFA device to sign in to the AWS SSO user portal\. If you had previously used RADIUS MFA, enabling MFA in AWS SSO effectively overrides RADIUS MFA for users who sign in to the user portal\. However, RADIUS MFA continues to challenge users when they sign in to all other applications that work with AWS Directory Service, such as Amazon WorkDocs\.

If your MFA is **Disabled** on the AWS SSO console and you have configured RADIUS MFA with AWS Directory Service, RADIUS MFA governs user portal sign\-in\. This means that AWS SSO falls back to RADIUS MFA configuration if MFA is disabled\.
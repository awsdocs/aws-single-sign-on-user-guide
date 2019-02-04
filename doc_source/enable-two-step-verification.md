# Enable Two\-Step Verification<a name="enable-two-step-verification"></a>

By default, when a user signs in to the user portal, they sign in with their email address and password \(the first step\)\. This is the standard authentication mechanism used in AWS SSO\. But if the two\-step verification option is enabled, users receive a verification code \(the second step\) sent to their assigned email address\. Users must use this verification code to be authenticated to the user portal\. These factors together provide additional security by preventing access to your user portal unless users supply valid user credentials and a valid verification code\.

**Note**  
When a verification code is sent to a user, it is only valid for 10 minutes\.

## Considerations Before Using Two\-Step Verification in AWS SSO<a name="two-step-considerations"></a>

Before you enable email\-based verification as your two\-step verification method, consider the following information:
+ All users must have first verified their email address before they can begin using email\-based verification during sign\-in\.
+ Do not enable two\-step verification if your users require signing in to the user portal to access to their email\. For example, your users might use Office 365 on the user portal to read their email\. In this case, users would not be able to retrieve the verification code and would be unable to sign in to the user portal\.
+ If you are already using RADIUS MFA that you configured with AWS Directory Service, then you do not need to enable two\-step verification within AWS SSO\. Two\-step verification is an alternative to RADIUS MFA for Microsoft Active Directory users of AWS SSO\. For more information, see [About RADIUS MFA](#about-radius)\.

## Verification Modes<a name="two-step-modes"></a>

Verification modes help you determine the level of security you want to enforce across all your users during sign\-in\. The default mode when you first configure AWS SSO is **Disabled**\. While in this mode, no two\-step verification method is enabled so users continue to sign in using their user name, password and/or RADIUS MFA as normal\. You can use either of the following modes to enable two\-step verification:
+ **Context\-aware**
+ **Always\-on**

**Note**  
If you have configured AWS SSO to use a connected directory and decide to enable either **Context\-aware** or **Always\-on** mode, your users must sign in to the user portal using the down\-level logon name format \(DOMAIN\\UserName\)\. This restriction does not apply when you are using an AWS SSO directory\. With an AWS SSO directory, users can sign in using either their down\-level logon name format or their UPN logon name format \([UserName@Corp\.Example\.com](mailto:UserName@Corp.Example.com)\)\. For general information about sign in formats, see [User Name Formats](https://docs.microsoft.com/en-us/windows/desktop/secauthn/user-name-formats) on the Microsoft documentation website\.

### Context\-aware<a name="context-aware"></a>

In this mode, AWS SSO analyzes the sign\-in context \(browser, location, and devices\) for each user to determine whether the user is signing in with a previously trusted context\. If a user is signing in from an unknown location or is using an unknown device, SSO prompts the user to verify their second\-factor of authentication\. The user is prompted for a verification code in addition to their email address and password credentials\.

This mode provides additional protection while making it easier for users who frequently sign in from their offices because they do not need to complete two\-step verification on every sign\-in\. SSO prompts users with two\-step verification during initial sign\-ins to create a baseline for successful sign\-ins\. Once a stable baseline is established, AWS SSO uses the baseline to determine a “trusted” sign\-in and does not challenge users for a verification code\. Users are only required to provide additional verification when their sign\-in context changes\. Such changes include signing in from a new device, a new browser, or an unknown location\.

**Note**  
Changing from **Disabled** mode to **Context\-aware** mode overrides existing RADIUS MFA settings that are configured in AWS Directory Service while signing in to AWS SSO for this directory\. For more information, see [About RADIUS MFA](#about-radius)\.

### Always\-on<a name="always-on"></a>

In this mode, AWS SSO requires that all users provide a verification code on every sign\-in\. You should use this mode if you have organizational or compliance policies that require your users to complete two\-step verification every time they sign in to the user portal\. For example, PCI DSS strongly recommends two\-step verification during every sign\-in to access applications that support high\-risk payment transactions\.

## About RADIUS MFA<a name="about-radius"></a>

[Remote Authentication Dial\-In User Service \(RADIUS\)](https://en.wikipedia.org/wiki/RADIUS) is an industry\-standard client–server protocol that provides authentication, authorization, and accounting management to enable users to connect to network services\. AWS Directory Service includes a RADIUS client that connects to the RADIUS server upon which you have implemented your MFA solution\. For more information, see [Enable Multi\-Factor Authentication for AWS Managed Microsoft AD](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_mfa.html) \.

### RADIUS MFA and AWS SSO<a name="radius-and-sso"></a>

You can use either RADIUS MFA or two\-step verification in AWS SSO for user sign\-ins to the user portal, but not both\. Two\-step verification in AWS SSO is an alternative to RADIUS MFA in cases where you are looking for AWS native two\-factor authentication for access to the portal\.

When you enable two\-step verification in AWS SSO, your users require a verification code when they sign in to the SSO user portal\. If you had previously used RADIUS MFA, enabling two\-step verification in AWS SSO effectively overrides RADIUS MFA for users who sign into the AWS SSO user portal\. However, RADIUS MFA continues to challenge users when they sign in to all other apps that work with AWS Directory Service, such as Amazon WorkDocs\.

If your two\-step verification is **Disabled** on the AWS SSO console and you have configured RADIUS MFA with AWS Directory Service, RADIUS MFA governs user portal sign\-in\. This means that AWS SSO falls back to RADIUS MFA configuration if two\-step verification is disabled\. 

**Topics**
+ [How to Enable Two\-Step Verification](how-to-enable-two-step.md)
+ [How to Disable Two\-Step Verification](how-to-disable-two-step.md)
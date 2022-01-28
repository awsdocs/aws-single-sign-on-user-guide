# Enable MFA<a name="mfa-enable-how-to"></a>

Use the following steps to enable MFA using the AWS SSO console\. Before you enable MFA, we recommend that you first review details about [MFA types](mfa-types.md)\.

**Note**  
If you’re using an external IdP, you will not see the **Multi\-factor authentication** section\. The external IdP manages MFA settings rather than AWS SSO managing them\.

**To enable MFA**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. In the left navigation pane, choose **Settings**\.

1. On the **Settings** page, under **Multi\-factor authentication**, choose **Configure**\.

1. On the **Configure multi\-factor authentication** page, choose one of the following authentication modes based on the level of security that your business needs:
   + **Only when their sign\-in context changes \(context\-aware\)**

     In this mode \(the default\), AWS SSO analyzes the sign\-in context \(browser, location, and devices\) for each user\. AWS SSO then determines whether the user is signing in with a previously trusted context\. If a user is signing in from an unknown IP address or is using an unknown device, AWS SSO prompts the user for MFA\. This prompt comes in addition to their email address and password credentials\.

     This mode provides additional protection for users who frequently sign in from their offices\. This mode is also easier for those users because they do not need to complete MFA on every sign\-in\. AWS SSO prompts users with MFA once and permits them to trust their device\. Once a user indicates that they want to trust a device, AWS SSO does not challenge the user for MFA for that device\. Users are required to provide additional verification only when their sign\-in context changes\. Such changes include signing in from a new device, a new browser, or an unknown IP address\.
   + **Every time they sign in \(always\-on\)**

     In this mode, AWS SSO requires that users with a registered MFA device will be prompted every time they sign in\. You should use this mode if you have organizational or compliance policies that require your users to complete MFA every time they sign in to the user portal\. For example, PCI DSS strongly recommends MFA during every sign\-in to access applications that support high\-risk payment transactions\.
   + **Never \(disabled\)**

     While in this mode, all users will sign in with their standard user name and password only\. Choosing this option disables AWS SSO MFA\.
**Note**  
If you are already using RADIUS MFA with AWS Directory Service, and want to continue using it as your default MFA type, then you can leave the authentication mode as disabled to bypass AWS SSO MFA’s capabilities\. Changing from **Disabled** mode to **Context\-aware** or **Always\-on** mode will override the existing RADIUS MFA settings\. For more information, see [RADIUS MFA](about-radius.md)\.

1. Choose **Save changes**\.
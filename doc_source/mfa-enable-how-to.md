# Enable MFA<a name="mfa-enable-how-to"></a>

Use the following steps to enable MFA using the IAM Identity Center console\. Before you enable MFA, we recommend that you first review details about [MFA types](mfa-types.md)\.

**Note**  
If you’re using an external IdP, you will not see the **Multi\-factor authentication** section\. The external IdP manages MFA settings rather than IAM Identity Center managing them\.

**To enable MFA**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. In the left navigation pane, choose **Settings**\.

1. On the **Settings** page, choose the **Authentication** tab\.

1. In the **Multi\-factor authentication** section, choose **Configure**\.

1. On the **Configure multi\-factor authentication** page, choose one of the following authentication modes based on the level of security that your business needs:
   + **Only when their sign\-in context changes \(context\-aware\)**

     In this mode \(the default\), IAM Identity Center provides users the option to trust their device during sign\-in\. After a user indicates that they want to trust a device, IAM Identity Center prompts the user for MFA once and analyzes the sign\-in context \(such as device, browser, and location\) for the user’s subsequent sign\-ins\. For subsequent sign\-ins, IAM Identity Center determines if the user is signing in with a previously trusted context\. If the user’s sign\-in context changes, IAM Identity Center prompts the user for MFA in addition to their email address and password credentials\.

     This mode provides ease of use for users who frequently sign in from their workplace, so they don’t need to complete MFA on every sign\-in\. They are only prompted for MFA if their sign\-in context changes\.
   + **Every time they sign in \(always\-on\)**

     In this mode, IAM Identity Center requires that users with a registered MFA device will be prompted every time they sign in\. You should use this mode if you have organizational or compliance policies that require your users to complete MFA every time they sign in to the user portal\. For example, PCI DSS strongly recommends MFA during every sign\-in to access applications that support high\-risk payment transactions\.
   + **Never \(disabled\)**

     While in this mode, all users will sign in with their standard user name and password only\. Choosing this option disables IAM Identity Center MFA\.
**Note**  
If you are already using RADIUS MFA with AWS Directory Service, and want to continue using it as your default MFA type, then you can leave the authentication mode as disabled to bypass IAM Identity Center MFA’s capabilities\. Changing from **Disabled** mode to **Context\-aware** or **Always\-on** mode will override the existing RADIUS MFA settings\. For more information, see [RADIUS MFA](about-radius.md)\.

1. Choose **Save changes**\.

   **Related Topics**
   + [Configure MFA types](how-to-configure-mfa-types.md)
   + [Configure MFA device enforcement](how-to-configure-mfa-device-enforcement.md)
   + [Allow users to register their own MFA devices](how-to-allow-user-registration.md)
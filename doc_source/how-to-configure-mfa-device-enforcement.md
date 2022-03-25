# Configure MFA device enforcement<a name="how-to-configure-mfa-device-enforcement"></a>

Use the following procedure to determine whether your users must have a registered MFA device when signing in to the AWS SSO user portal\. 

**To configure MFA device enforcement for your users**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. In the left navigation pane, choose **Settings**\.

1. On the **Settings** page, choose the **Network & security** tab, and then choose **Configure**\.

1. On the **Configure multi\-factor authentication** page, under **If a user does not yet have a registered MFA device** choose one of the following choices based on your business needs:
   + **Require them to register an MFA device at sign in**

     Use this option when you want to require users who do not yet have a registered MFA device, to self\-enroll a device during sign\-in following a successful password authentication\. This allows you to secure your organization’s AWS environments with MFA without having to individually enroll and distribute authentication devices to your users\. During self\-enrollment, your users can register any device from the available [MFA types](mfa-types.md) you've previously enabled\. After completing registration, users have the option to give their newly enrolled MFA device a friendly name, after which AWS SSO redirects the user to their original destination\. If the user’s device is lost or stolen, you can simply remove that device from their account, and AWS SSO will require them to self\-enroll a new device during their next sign\-in\.
   + **Require them to provide a one\-time password sent by email to sign in**

     Use this option when you want to have verification codes sent to users by email\. Because email is not bound to a specific device, this option does not meet the bar for industry\-standard multi\-factor authentication\. But it does improve security over having a password alone\. Email verification will only be requested if a user has not registered an MFA device\. If the **Context\-aware** authentication method has been enabled, the user will have the opportunity to mark the device on which they receive the email as trusted\. Afterward they will not be required to verify an email code on future logins from that device, browser, and IP address combination\.
**Note**  
If you are using Active Directory as your AWS SSO enabled identity source, the email address will always be based on the Active Directory `email` attribute\. Custom Active Directory attribute mappings will not override this behavior\. 
   + **Block their sign\-in**

     Use the **Block Their Sign\-In** option when you want to enforce MFA use by every user before they can sign in to AWS\.
**Important**  
If your authentication method is set to **Context\-aware** a user might select the **This is a trusted device** check box on the sign\-in page\. In that case, that user will not be prompted for MFA even if you have the **Block their sign in** setting enabled\. If you want these users to be prompted, change your authentication method to **Always On**\.
   + **Allow them to sign in**

     The default setting when you first configure AWS SSO MFA\. Use this option to indicate that MFA devices are not required in order for your users to sign in to the user portal\. Users who chose to register MFA devices will still be prompted for MFA\.

1. Choose **Save changes**\.
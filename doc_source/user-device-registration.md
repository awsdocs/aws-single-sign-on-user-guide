# How to register a device for use with multi\-factor authentication<a name="user-device-registration"></a>

Use the following procedure within the user portal to register your new device for multi\-factor authentication \(MFA\)\.

**Note**  
We recommend that you first download the appropriate Authenticator app onto your device before starting the steps in this procedure\. For a list of apps that you can use for MFA devices, see [Authenticator apps](mfa-types-apps.md)\.

**To register your device for use with MFA**

1. Go to your user portal\.

1. Near the top\-right of the page, choose **MFA devices**\.

1. On the **Multi\-factor authentication \(MFA\) devices** page, choose **Register device**\.
**Note**  
If the **Register MFA device** option is grayed out, you will need to contact your administrator for assistance with registering your device\.

1. On the **Register MFA device** page, select one of the following MFA device types, and follow the instructions:
   + **Authenticator app**

     1. On the **Set up the authenticator app** page, you might notice configuration information for the new MFA device, including a QR code graphic\. The graphic is a representation of the secret key that is available for manual entry on devices that do not support QR codes\.

     1. Using the physical MFA device, do the following:

        1. Open a compatible MFA authenticator app\. For a list of tested apps that you can use with MFA devices, see [Authenticator apps](mfa-types-apps.md)\. If the MFA app supports multiple accounts \(multiple MFA devices\), choose the option to create a new account \(a new MFA device\)\.

        1. Determine whether the MFA app supports QR codes, and then do one of the following on the **Set up the authenticator app** page:

           1. Choose **Show QR code**, and then use the app to scan the QR code\. For example, you might choose the camera icon or choose an option similar to **Scan code**\. Then use the device's camera to scan the code\.

           1. Choose **show secret key**, and then enter that secret key into your MFA app\.
**Important**  
When you configure an MFA device for AWS SSO, we recommend that you save a copy of the QR code or secret key *in a secure place*\. This can help if you lose the phone or have to reinstall the MFA authenticator app\. If either of those things happen, you can quickly reconfigure the app to use the same MFA configuration\.

     1. On the **Set up the authenticator app** page, under **Authenticator code**, enter the one\-time password that currently appears on the physical MFA device\.
**Important**  
Submit your request immediately after generating the code\. If you generate the code and then wait too long to submit the request, the MFA device is successfully associated with your user account\. But the MFA device is out of sync\. This happens because time\-based one\-time passwords \(TOTP\) expire after a short period of time\. If this happens, you can resync the device\.

     1. Choose **Assign MFA**\. The MFA device can now start generating one\-time passwords and is now ready for use with AWS\.
   + **Security key** or **Built\-in authenticator**

     1. On the **Register your user's security key** page, follow the instructions given to you by your browser or platform\.
**Note**  
The experience here will vary based on the different operating systems and browsers, so follow the instructions displayed by your browser or platform\. After your device has been successfully registered, you will be given the option to associate a friendly display name to your newly enrolled device\. If you want to change this, choose **Rename**, enter the new name, and then choose **Save**\.
# How to Register a Device for Use with Multi\-Factor Authentication<a name="user-device-registration"></a>

Use the following procedure within the user portal to register your new device for multi\-factor authentication \(MFA\)\.

**Note**  
We recommend that you first download the appropriate Authenticator app onto your device before starting the steps in this procedure\. For a list of apps that you can use for MFA devices, see [Multi\-Factor Authentication](http://aws.amazon.com/iam/details/mfa/)\.

**To register your device for use with MFA**

1. Go to your user portal\.

1. Near the top\-right of the page, choose **My devices**\.

1. On the **My devices** page, choose **Register MFA device**\.
**Note**  
If the **Register MFA device** option is grayed out, you will need to contact your administrator for assistance with registering your device\.

1. On the **Device name** page, enter a friendly name for the new MFA device\. It is helpful to describe the device to make it easy to identify and remove if your device is lost or stolen\. For example, you might enter “My iPhone X\.” Then choose **Next**\. This name will be visible to your administrator\.

1. The **Device configuration** page displays some information for the new MFA device, including an obscured QR code\. Using the physical MFA device, do the following:

   1. Open a compatible MFA authenticator app\. \(For a list of apps that you can use for hosting MFA devices, see [Multi\-Factor Authentication](http://aws.amazon.com/iam/details/mfa/)\.\) If you are not sure which app to download, contact your administrator\. If the MFA app supports multiple accounts \(multiple MFA devices\), choose the option to create a new account \(a new MFA device\)\.

   1. Determine whether the MFA app supports QR codes, and then do one of the following on the **Device configuration** page:

      1. Wait until no one is looking over your shoulder, choose **Show QR code**, and then use the app to scan the QR code\. 

      1. Wait until no one is looking over your shoulder, choose **show secret key**, and then enter that secret key into your MFA app\.

1. On the **Device configuration** page, under **An MFA code will be displayed on your device\. Type that MFA code here\.**, enter the one\-time password that currently appears in the MFA app\.
**Important**  
Submit your request immediately after generating the code\. If you generate the code and then wait too long to submit the request, the MFA device may become out of sync\. This happens because time\-based one\-time passwords \(TOTP\) expire after a short period of time\.

1. Choose **Register MFA device**\. Your new MFA device can now start generating one\-time passwords and is now ready for use with AWS\.
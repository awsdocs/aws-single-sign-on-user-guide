# Signing in to the AWS access portal<a name="howtosignin"></a>

By this time, you should have been provided a specific sign\-in URL to the AWS access portal by an administrator or help desk employee\. Once you have this, you can proceed with the following steps to sign in to the portal\.

**Note**  
Once you have been signed\-in, your AWS access portal session will be valid for 8 hours\.

**To sign in to the AWS access portal**

1. In your browser window, paste in the sign\-in URL that you were provided and press **Enter**\. The URL looks like `d-xxxxxxxxxx.awsapps.com/start` or `your_subdomain.awsapps.com/start`\. We recommend that you bookmark this link to the portal now so that you can quickly access it later\.

1. Sign in using your standard company user name and password\.
**Note**  
If your administrator sent you an email one\-time password \(OTP\) and this is your first time signing in, enter that password\. After you're signed in, you must create a new password for future sign\-ins\.

    If you are prompted for a **Verification code**, check your email and then copy and paste the code into the sign\-in page\.
**Note**  
Verification codes are typically sent through email, but the delivery method can vary\. Check with your administrator for details\.

1. Once signed in, you can access any AWS account and application that appears in the portal\. Simply choose an icon\. 

## Trusted devices<a name="howtosignin-trusted-devices"></a>

After you choose the option **This is a trusted device** from the sign\-in page, IAM Identity Center will consider all future sign\-ins from that device as authorized\. This means that IAM Identity Center will not present an option to enter in an MFA code as long as you are using that trusted device\. However, there are some exceptions\. These include signing in from a new browser or when your device has been issued an unknown IP address\.
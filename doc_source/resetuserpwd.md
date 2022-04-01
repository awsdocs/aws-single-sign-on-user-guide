# Reset a user password<a name="resetuserpwd"></a>

Use the following procedure to reset the password for a user in your AWS SSO identity store\. 

**To reset a user password**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Users**\.

1. Choose the user whose password you want to reset\.

1. On the top right corner of the page, choose **Reset password**\.

1. In the **Reset password** dialog box, select one of the following choices, and then choose **Reset password**:

   1. **Send an email to the user with instructions to reset the password** – This option automatically sends the user an email addressed from Amazon Web Services that walks them through how to reset their password\.
**Warning**  
As a security best practice, verify that the email address for this user is correct prior to selecting this option\. If this password reset email were to be sent to an incorrect or misconfigured email address, a malicious recipient could use it to gain unauthorized access to your AWS environment\.

   1. **Generate a one\-time password and share the password with the user** – This option provides you with the password details that you can manually send to the user from your email address\.
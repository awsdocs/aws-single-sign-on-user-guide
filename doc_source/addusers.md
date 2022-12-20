# Add users<a name="addusers"></a>

Users and groups that you create in your Identity Center directory are available in IAM Identity Center only\. Use the following procedure to add users to your Identity Center directory\. Alternatively, you can call the AWS API operation [CreateUser](https://docs.aws.amazon.com/singlesignon/latest/IdentityStoreAPIReference/API_CreateUser.html) to add users\.

**To add a user**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Users**\.

1. Choose **Add user** and provide the following required information:

   1. **Username** – This user name is required to sign in to the AWS access portal and can't be changed later\. It must be between 1 and 100 characters\.

   1. **Password** – You can either send an email with the password setup instructions \(this is the default option\) or generate a one\-time password\. If you are creating an administrative user and you choose to send an email, make sure that you specify an email address that you can access\.

      1. **Send an email to this user with password setup instructions\.** – This option automatically sends the user an email addressed from Amazon Web Services, with the subject line **Invitation to join AWS Single Sign\-On**\. The email invites the user on behalf of your company to access the IAM Identity Center AWS access portal\.
**Note**  
All emails sent by the IAM Identity Center service will come from either the address [no-reply@signin.aws](no-reply@signin.aws) or [no-reply@login.awsapps.com](no-reply@login.awsapps.com)\. We recommend that you configure your email system so that it accepts emails from these sender email addresses and does not handle them as junk or spam\. 

      1. **Generate a one\-time password that you can share with this user\.** – This option provides you with the AWS access portal URL and password details that you can manually send to the user from your email address\.

   1. **Email address** – The email address must be unique\.

   1. **Confirm email address**

   1. **First name** – You must enter a name here for automatic provisioning to work\. For more information, see [Automatic provisioning](provision-automatically.md)\.

   1. **Last name** – You must enter a name here for automatic provisioning to work\.

   1. **Display name**
**Note**  
\(Optional\) If applicable, you can specify values for additional attributes such as the user's **Microsoft 365 immutable ID** to help provide the user with single sign\-on access to certain business applications\. 

1. Choose **Next**\.

1. If applicable, select one or more groups to which you want to add the user, and choose **Next**\.

1. Review the information that you specified for **Step 1: Specify user details** and **Step 2: Add user to groups \- optional**\. Choose **Edit** by either step to make any changes\. After you confirm that the correct information is specified for both steps, choose **Add user**\.
**Note**  
If you are adding your first administrative user in IAM Identity Center by following the steps to [create a user](get-started-use-identity-center-directory-create-user-in-identity-center.md), return to that procedure and follow the steps to finish activating the user account\.
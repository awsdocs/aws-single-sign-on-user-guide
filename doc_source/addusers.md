# Add Users<a name="addusers"></a>

Users and groups that you create in your AWS SSO store are available in AWS SSO only\. Use the following procedure to add users to your AWS SSO store\. 

**To add a user**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Users**\.

1. Choose **Add user** and provide the following required information:

   1. **Username** – This user name will be required to sign in to the user portal and cannot be changed later\.

   1. **Password** – Choose from one of the following choices to send the user's password\.

      1. **Send an email to the user with password setup instructions** – This option automatically sends the user an email addressed from Amazon Web Services\. The email invites the user on behalf of your company to access the AWS SSO user portal\.

      1. **Generate a one\-time password that you can share with the user** – This option provides you with the user portal URL and password details that you can manually send to the user from your email address\.

   1. **Email address**

   1. **Confirm email address**

   1. **First name** – You must enter a name here for automatic provisioning to work\. For more information, see [Automatic Provisioning](provision-automatically.md)\.

   1. **Last name** – You must enter a name here for automatic provisioning to work\.

   1. **Display name**
**Note**  
\(Optional\) You can provide additional attributes such as **Employee ID** and **Office 365 Immutable ID** to help map the user's identity in AWS SSO with certain business applications that the user needs to use\. 

1. Choose **Next: Groups**\.

1. Select one or more groups that you want the user to be a member of\. Then choose **Add user**\.
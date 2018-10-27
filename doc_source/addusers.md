# Add Users<a name="addusers"></a>

Use the following procedure to add users to your AWS SSO directory\. 

**To add a user**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. From the **Dashboard**, choose **Manage your directory**

1. On the **Directory** page, choose the **Users** tab, and then choose **Add user**\. 

1. On the **Add user** page, provide the following required information:

   1. **Email address**

   1. **Password** – Choose from one of the following choices to send the user's password\.

      1. **Send an email to the user with password setup instructions** – This option automatically sends the user an email addressed from Amazon Web Services and invites the user on behalf of your company to access the AWS SSO user portal\.

      1. **Generate a one\-time password that you can share with the user** – This option provides you with the user portal URL and password details that you can manually send to the user from your email address\.

   1. **First name**

   1. **Last name**

   1. **Display name**
**Note**  
\(Optional\) You can provide additional attributes such as **Employee ID** and **Office 365 Immutable ID** to help map the user's identity in AWS SSO with certain business applications that the user needs to use\. 

1. Choose **Next: Groups**\.

1. Select one or more groups that you want the user to be a member of, and then choose **Add user**\.
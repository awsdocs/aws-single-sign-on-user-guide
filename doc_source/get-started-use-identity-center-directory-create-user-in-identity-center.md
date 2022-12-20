# Use the default directory and create a user in IAM Identity Center<a name="get-started-use-identity-center-directory-create-user-in-identity-center"></a>

When you enable IAM Identity Center for the first time, it is automatically configured with an Identity Center directory as your default identity source\. Complete the following steps to create a user in IAM Identity Center and activate the user account\.

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon) using your AWS account root user credentials\.

1. Follow the steps in [Add users](addusers.md) to create a user\. 

   When you specify the user details, you can either send an email with the password setup instructions \(this is the default option\) or generate a one\-time password\. If you send an email, make sure that you specify an email address that you can access\.

1. After you add the user, return to this procedure\. If you kept the default option to send an email with the password setup instructions, do the following to activate the user account:

   1. You'll receive an email with the subject **Invitation to join AWS Single Sign\-On**\. Open the email and choose **Accept invitation**\.

   1. On the **New user sign up** page, enter and confirm a password, and then choose **Set new password**\.
**Note**  
Make sure to save your password\. You'll need it later to [sign into the AWS access portal using your administrative credentials](get-started-sign-in-access-portal.md)\.

**Next step: Create an administrative permission set** 

At this point, your user doesn't have access to the management account\. You will set up administrative access to this account by creating an administrative permission set and assigning the user to that permission set\. For more information, see [Step 3: Create an administrative permission set](get-started-create-an-administrative-permission-set.md)\.
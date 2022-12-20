# Step 5: Sign in to the AWS access portal with your administrative credentials<a name="get-started-sign-in-access-portal"></a>

Complete the following steps to confirm that you can sign in to the AWS access portal by using the credentials of the administrative user, and that you can access the AWS account\.

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon) using your AWS account root credentials\.

1. In the navigation pane, choose **Dashboard**\.

1. On the **Dashboard** page, under **Settings summary**, copy the AWS access portal URL\.

1. Open a separate browser, paste in the AWS access portal URL that you copied, and press **Enter**\. 

1. Sign in by using either of the following:
   + If you're using Active Directory or an external identity provider \(IdP\) as your identity source, sign in by using the credentials of the Active Directory or IdP user that you assigned to the **AdministratorAccess** permission set in IAM Identity Center\.
   + If you're using the default Identity Center directory as your identity source, sign in by using the user name that you specified when you created the user and the new password that you specified when you activated the user account\. For more information, see [Use the default directory and create a user in IAM Identity Center](get-started-use-identity-center-directory-create-user-in-identity-center.md)\.

1. After you are signed in, an **AWS account** icon appears in the portal\.

1. When you select the **AWS account** icon, the account name, account ID, and email address associated with the account appear\. 

1. Choose the name of the account to display the **AdministratorAccess** permission set, and select the **Management Console** link to the right of **AdministratorAccess**\. 

   When you sign in, the name of the permission set to which the user is assigned appears as an available role in the AWS access portal\. Because you assigned this user to the `AdministratorAccess` permission set, the role will appear in the AWS access portal as: `AdministratorAccess`/*username*

1. If you are redirected to the AWS Management Console, you successfully finished setting up administrative access to the AWS account\. Proceed to step 10\.

1. Switch to the browser that you used to sign into the AWS Management Console and set up IAM Identity Center, and sign out from your AWS account root user\.
**Important**  
We strongly recommend that you use the credentials of the administrative user when you sign in to the AWS access portal\. Safeguard your root user credentials and use them to perform the tasks that only the root user can perform\. To enable other users to access your accounts and applications, and to administer IAM Identity Center, create and assign permission sets only through IAM Identity Center\.
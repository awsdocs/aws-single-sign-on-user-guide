# Use the default Identity Center directory<a name="get-started-use-identity-center-directory"></a>

When you enable IAM Identity Center for the first time, it is automatically configured with an Identity Center directory as your default identity source\. The following topics will help you create a user in IAM Identity Center and assign permissions that provide the user with administrative access to an AWS account\.

**Topics**
+ [Create a user in IAM Identity Center and set up administrative access to an AWS account](#create-admin-user-set-up-account-access-identity-center-directory)
+ [Sign in to the AWS access portal with your administrative credentials](#sign-in-access-portal-identity-center-directory)

## Create a user in IAM Identity Center and set up administrative access to an AWS account<a name="create-admin-user-set-up-account-access-identity-center-directory"></a>

Complete the following steps to create a user and set up AWS account access for the user\. After you create the user, assigning the user to the **AdministratorAccess** permission set grants them administrative access to the AWS account\.

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon) using your AWS account root user credentials\.

1. Follow the steps in [Add users](addusers.md) to create a user\. 

   When you specify the user details, you can either send an email with the password setup instructions \(this is the default option\) or generate a one\-time password\. If you send an email, make sure that you specify an email address that you can access\.

1. After you add the user, return to this procedure and perform the rest of the steps to finish setting up AWS account access\. If you kept the default option to send an email with the password setup instructions, do the following to activate the user account:

   1. You'll receive an email with the subject **Invitation to join AWS Single Sign\-On**\. Open the email and choose **Accept invitation**\.

   1. On the **New user sign up** page, enter and confirm a password, and then choose **Set new password**\.
**Note**  
Make sure to save your password\. You'll need it later to [sign into the AWS access portal using your administrative credentials](#sign-in-access-portal-identity-center-directory)\. At this point, your user doesn't have access to the management account\. You will set up administrative access to this account in the following steps\.

1. Return to the AWS Management Console\. Make sure that you are signed in with your AWS account root user credentials\.

1. In the navigation pane, under **Multi\-account permissions**, choose **AWS accounts**\. 

1. On the **AWS accounts** page, a tree view list of your organization appears\. Select the check box next to the AWS account to which you want to assign single sign\-on access\. If you have multiple accounts in your organization, select the check box next to the management account\.

1. Choose **Assign users or groups**\. 

1. For **Step 1: Select users and groups**, on the **Assign users and groups to "*AWS\-account\-name*"** page, do the following:

   1. On the **Users** tab, select the user that you just created\.

   1. After you confirm that the correct user is selected, choose **Next**\.

1. For **Step 2: Select permission sets**, on the **Assign permission sets to "*AWS\-account\-name*"** page, under **Permission sets**, select the **AdministratorAccess** permission set\.

1. Choose **Next**\.

1. For **Step 3: Review and Submit**, on the **Review and submit assignments to "*AWS\-account\-name*"** page, do the following:

   1. Review the selected user and permission set\.

   1. After you confirm that the correct user is assigned to the **AdministratorAccess** permission set, choose **Submit**\.
**Important**  
The user assignment process might take a few minutes to complete\. Leave this page open until the process successfully completes\.

1. Follow the steps in [Enable MFA](mfa-enable-how-to.md) to enable MFA for IAM Identity Center\.

When you set up account access for the administrative user, IAM Identity Center creates a corresponding IAM role\. This role, which is controlled by IAM Identity Center, is created in the relevant AWS account, and the policies specified in the permission set are attached to the role\. 

## Sign in to the AWS access portal with your administrative credentials<a name="sign-in-access-portal-identity-center-directory"></a>

Complete the following steps to confirm that you can sign in to the AWS access portal by using the credentials of the administrative user that you created, and that you can access the AWS account\. 

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon) using your AWS account root user credentials\.

1. In the navigation pane, choose **Dashboard**\.

1. On the **Dashboard** page, under **Settings summary**, copy the AWS access portal URL\.

1. Open a separate browser, paste in the AWS access portal URL that you copied, and press **Enter**\. 

1. Sign in to the portal by using the credentials of the IAM Identity Center user that you assigned to the **AdministratorAccess** permission set in IAM Identity Center\. The credentials will be the following:
   + The user name that you specified when you created a user \(step 2 in [Create a user in IAM Identity Center and set up administrative access to an AWS account](#create-admin-user-set-up-account-access-identity-center-directory)\)\.
   + The new password that you specified when you activated the user account \(step 3 in [ Create a user in IAM Identity Center and set up administrative access to an AWS accountCreate an administrative user in IAM Identity Center and set up AWS account access  Complete the following steps to create a user and set up AWS account access for the user\. After you create the user, assigning the user to the **AdministratorAccess** permission set grants them administrative access to the AWS account\.  Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon) using your AWS account root user credentials\. Follow the steps in [Add users](addusers.md) to create a user\.  When you specify the user details, you can either send an email with the password setup instructions \(this is the default option\) or generate a one\-time password\. If you send an email, make sure that you specify an email address that you can access\.  After you add the user, return to this procedure and perform the rest of the steps to finish setting up AWS account access\. If you kept the default option to send an email with the password setup instructions, do the following to activate the user account:  You'll receive an email with the subject **Invitation to join AWS Single Sign\-On**\. Open the email and choose **Accept invitation**\. On the **New user sign up** page, enter and confirm a password, and then choose **Set new password**\. Make sure to save your password\. You'll need it later to [sign into the AWS access portal using your administrative credentials](#sign-in-access-portal-identity-center-directory)\. At this point, your user doesn't have access to the management account\. You will set up administrative access to this account in the following steps\.    Return to the AWS Management Console\. Make sure that you are signed in with your AWS account root user credentials\.  In the navigation pane, under **Multi\-account permissions**, choose **AWS accounts**\.    On the **AWS accounts** page, a tree view list of your organization appears\. Select the check box next to the AWS account to which you want to assign single sign\-on access\. If you have multiple accounts in your organization, select the check box next to the management account\.   Choose **Assign users or groups**\.    For **Step 1: Select users and groups**, on the **Assign users and groups to "*AWS\-account\-name*"** page, do the following:   On the **Users** tab, select the user that you just created\.   After you confirm that the correct user is selected, choose **Next**\.     For **Step 2: Select permission sets**, on the **Assign permission sets to "*AWS\-account\-name*"** page, under **Permission sets**, select the **AdministratorAccess** permission set\.  Choose **Next**\.   For **Step 3: Review and Submit**, on the **Review and submit assignments to "*AWS\-account\-name*"** page, do the following:   Review the selected user and permission set\.   After you confirm that the correct user is assigned to the **AdministratorAccess** permission set, choose **Submit**\.  The user assignment process might take a few minutes to complete\. Leave this page open until the process successfully completes\.     Follow the steps in [Enable MFA](mfa-enable-how-to.md) to enable MFA for IAM Identity Center\.  When you set up account access for the administrative user, IAM Identity Center creates a corresponding IAM role\. This role, which is controlled by IAM Identity Center, is created in the relevant AWS account, and the policies specified in the permission set are attached to the role\.  ](#create-admin-user-set-up-account-access-identity-center-directory)\)\.

1. After you are signed in, an **AWS account** icon appears in the portal\.

1. When you select the **AWS account** icon, the account name, account ID, and email address of the administrative user appear\. 

1. Choose the name of the account to display the **AdministratorAccess** permission set, and select the **Management Console** link to the right of **AdministratorAccess**\. 

   When you sign in, the name of the permission set to which the user is assigned appears as an available role in the AWS access portal\. Because you assigned this user to the `AdministratorAccess` permission set, the role will appear in the AWS access portal as: `AdministratorAccess`/*username*

1. If you are redirected to the AWS Management Console, you successfully finished setting up administrative access to the AWS account\. Proceed to step 10\.

1. Switch to the browser that you used to sign into the AWS Management Console and set up IAM Identity Center, and sign out from your AWS account root user\.
**Important**  
We strongly recommend that you adhere to the best practice of using the credentials of the administrative user that you just created when you sign in to the AWS access portal, and that you securely lock away your AWS account root user credentials\.

To enable other users to access your AWS accounts and cloud applications, and to administer IAM Identity Center, create and assign permission sets only through IAM Identity Center\.
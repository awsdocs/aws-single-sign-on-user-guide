# Connect Active Directory or an external IdP<a name="get-started-connect-id-source-ad-idp"></a>

If you're already using Active Directory or an external identity provider \(IdP\), the following topics will help you connect your directory to IAM Identity Center\. You'll also learn how to assign AWS account access to an administrative user in IAM Identity Center\.

You can connect an AWS Managed Microsoft AD directory, a self\-managed directory in Active Directory, or an external IdP with IAM Identity Center\. If you plan to connect an AWS Managed Microsoft AD directory or a self\-managed directory in Active Directory, make sure that your Active Directory configuration meets the prerequisites in [Active Directory or an external IdP](get-started-prereqs-considerations.md#prereqs-active-directory-idp-identity-source)\.

**Note**  
As a security best practice, we strongly recommend that you enable multi\-factor authentication\. If you plan to connect an AWS Managed Microsoft AD directory or a self\-managed directory in Active Directory and you're not using RADIUS MFA with AWS Directory Service, enable MFA in IAM Identity Center\. If you plan to use an external identity provider, note that the external IdP, not IAM Identity Center, manages MFA settings\. MFA in IAM Identity Center is not supported for use by external IdPs\. For more information, see [Enable MFA](mfa-enable-how-to.md)\. 

**AWS Managed Microsoft AD**

1. Review the guidance in [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)\.

1. Follow the steps in [Connect IAM Identity Center to an AWS Managed Microsoft AD directory](connectawsad.md)\.

1. Configure Active Directory to synchronize the user to whom you want to grant administrative permissions into IAM Identity Center\. For more information, see [Provisioning when users come from Active Directory](manage-your-identity-source-ad.md#provision-users-from-ad)\.

**Self\-managed directory in Active Directory**

1. Review the guidance in [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)\.

1. Follow the steps in [Connect IAM Identity Center to a self\-managed directory in Active Directory](connectonpremad.md)\.

1. Configure Active Directory to synchronize the user to whom you want to grant administrative permissions into IAM Identity Center\. For more information, see [Provisioning when users come from Active Directory](manage-your-identity-source-ad.md#provision-users-from-ad)\.

**External IdP**

1. Review the guidance in [Connect to an external identity provider](manage-your-identity-source-idp.md)\.

1. Follow the steps in [How to connect to an external identity provider](manage-your-identity-source-idp.md#how-to-connect-idp)\.

1. 

   Configure your IdP to provision users into IAM Identity Center\. 
**Note**  
Before you set up automatic, group\-based provisioning of all your workforce identities from your IdP into IAM Identity Center, we recommend that you sync the one user to whom you want to grant administrative permissions into IAM Identity Center\.

## Set up AWS account access for an administrative user<a name="assign-account-access-admin-user-ad-idp"></a>

To set up AWS account access for an administrative user in IAM Identity Center, you must assign the user to the **AdministratorAccess** permission set\. 

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon) using your AWS account root user credentials\.

1. In the navigation pane, under **Multi\-account permissions**, choose **AWS accounts**\.

1. On the **AWS accounts** page, a tree view list of your organization appears\. Select the check box next to the AWS account to which you want to assign administrative access\. If you have multiple accounts in your organization, select the check box next to the management account\.

1. Choose **Assign users or groups**\. 

1. For **Step 1: Select users and groups**, on the **Assign users and groups to "*AWS\-account\-name*"** page, do the following:

   1. On the **Users** tab, select the user to whom you want to grant administrative permissions\.

      To filter the results, start typing the name of the user that you want in the search box\.

   1. After you confirm that the correct user is selected, choose **Next**\.

1. For **Step 2: Select permission sets**, on the **Assign permission sets to "*AWS\-account\-name*"** page, under **Permission sets**, select the **AdministratorAccess** permission set\.

1. Choose **Next**\.

1. For **Step 3: Review and Submit**, on the **Review and submit assignments to "*AWS\-account\-name*"** page, do the following:

   1. Review the selected user and permission set\.

   1. After you confirm that the correct user is assigned to the **AdministratorAccess** permission set, choose **Submit**\.
**Important**  
The user assignment process might take a few minutes to complete\. Leave this page open until the process successfully completes\.

When you set up account access for the administrative user, IAM Identity Center creates a corresponding IAM role\. This role, which is controlled by IAM Identity Center, is created in the relevant AWS account, and the policies specified in the permission set are attached to the role\. 

## Sign in to the AWS access portal with your administrative credentials<a name="sign-in-access-portal-ad-idp"></a>

Complete the following steps to confirm that you can sign in to the AWS access portal by using the credentials of the administrative user, and that you can access the AWS account\.

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon) using your AWS account root credentials\.

1. In the navigation pane, choose **Dashboard**\.

1. On the **Dashboard** page, under **Settings summary**, copy the AWS access portal URL\.

1. Open a separate browser, paste in the AWS access portal URL that you copied, and press **Enter**\. 

1. Sign in by using the credentials of the Active Directory or IdP user that you assigned to the **AdministratorAccess** permission set in IAM Identity Center\.

1. After you are signed in, an **AWS account** icon appears in the portal\.

1. When you select the **AWS account** icon, the account name, account ID, and email address associated with the account appear\. 

1. Choose the name of the account to display the **AdministratorAccess** permission set, and select the **Management Console** link to the right of **AdministratorAccess**\. 

   When you sign in, the name of the permission set to which the user is assigned appears as an available role in the AWS access portal\. Because you assigned this user to the `AdministratorAccess` permission set, the role will appear in the AWS access portal as: `AdministratorAccess`/*username*

1. If you are redirected to the AWS Management Console, you successfully finished setting up administrative access to the AWS account\. Proceed to step 10\.

1. Switch to the browser that you used to sign into the AWS Management Console and set up IAM Identity Center, and sign out from your AWS account root user\.
**Important**  
We strongly recommend that you adhere to the best practice of using the credentials of the administrative user when you sign in to the AWS access portal, and that you securely lock away your AWS account root user credentials\.

To enable other users to access your accounts and applications, and to administer IAM Identity Center, create and assign permission sets only through IAM Identity Center\.
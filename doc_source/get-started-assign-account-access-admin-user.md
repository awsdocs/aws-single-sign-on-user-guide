# Step 4: Set up AWS account access for an administrative user<a name="get-started-assign-account-access-admin-user"></a>

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

1. If either of the following applies, follow the steps in [Enable MFA](mfa-enable-how-to.md) to enable MFA for IAM Identity Center:
   + You're using the default Identity Center directory as your identity source\.
   + You're using an AWS Managed Microsoft AD directory or a self\-managed directory in Active Directory as your identity source and you're not using RADIUS MFA with AWS Directory Service\.
**Note**  
If you're using an external identity provider, note that the external IdP, not IAM Identity Center, manages MFA settings\. MFA in IAM Identity Center is not supported for use by external IdPs\. 

When you set up account access for the administrative user, IAM Identity Center creates a corresponding IAM role\. This role, which is controlled by IAM Identity Center, is created in the relevant AWS account, and the policies specified in the permission set are attached to the role\. 
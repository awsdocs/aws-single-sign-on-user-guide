# Single sign\-on access<a name="useraccess"></a>

You can assign users in your connected directory permissions to the management account or member accounts in your AWS Organizations organization based on [common job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html)\. Or you can use custom permissions to meet your specific security requirements\. For example, you can grant database administrators broad permissions to Amazon RDS in development accounts but limit their permissions in production accounts\. AWS SSO configures all the necessary user permissions in your AWS accounts automatically\.

**Note**  
You might need to grant users or groups permissions to operate in the AWS Organizations management account\. Because it is a highly privileged account, additional security restrictions require you to have the [IAMFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/IAMFullAccess) policy or equivalent permissions before you can set this up\. These additional security restrictions are not required for any of the member accounts in your AWS organization\.

## Assign user access<a name="assignusers"></a>

Use the following procedure to assign SSO access to users and groups in your connected directory and use permission sets to determine their level of access\.

**Note**  
To simplify administration of access permissions, we recommended that you assign access directly to groups rather than to individual users\. With groups you can grant or deny permissions to groups of users rather than having to apply those permissions to each individual\. If a user moves to a different organization, you simply move that user to a different group and they automatically receive the permissions that are needed for the new organization\.

**To assign access to users or groups**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the AWS SSO console is using the Region where your AWS Managed Microsoft AD directory is located before you move to the next step\.

1. Choose **AWS accounts**\.

1. On the **AWS Organization** page, a tree view list of your organization appears\. Select the check box next to one or more AWS accounts to which you want to assign SSO access\.
**Note**  
You can select up to 10 AWS accounts at a time per permission set when you assign SSO access to users and groups\. To assign more than 10 AWS accounts to the same set of users and groups, repeat this procedure as required for the additional accounts\. When prompted, select the same users, groups, and permission set\.

1. Choose **Assign users or groups**\. 

1. For **Step 1: Select users and groups**, on the **Assign users and groups to "*AWS\-account\-name*"** page, do the following:

   1. On the **Users** tab, select one or more users to grant SSO access to\.

      To filter the results, start typing the name of the user that you want in the search box\.

   1. On the **Groups **tab, select one or more groups to grant SSO access to\.

      To filter the results, start typing the name of the group that you want in the search box\.

   1. To display the users and groups that you selected, choose the sideways triangle next to **Selected users and groups**\.

   1. After you confirm that the correct users and groups are selected, choose **Next**\.

1. For **Step 2: Select permission sets**, on the **Assign permission sets to "*AWS\-account\-name*"** page, do the following:

   1. Select one or more existing permission sets\. If required, you can create and select new permission sets\.
      + To select one or more existing permission sets, under **Permission sets**, select the permission sets that you want to apply to the users and groups that you selected in the previous step\.
      + To create one or more new permission sets, choose **Create permission set**, and follow the steps in [Create a permission set](howtocreatepermissionset.md)\. After you create the permission sets that you want to apply, in the SSO console, return to **AWS accounts** and follow the instructions until you reach **Step 2: Select permission sets**\. When you reach this step, select the new permission sets that you created, and proceed to the next step in this procedure\.

   1. After you confirm that the correct permission sets are selected, choose **Next**\.

1. For **Step 3: Review and Submit**, on the **Review and submit assignments to "*AWS\-account\-name*"** page, do the following:

   1. Review the selected users, groups, and permission sets\.

   1. After you confirm that the correct users, groups, and permission sets are selected, choose **Submit**\.
**Important**  
The user and group assignment process might take a few minutes to complete\. Leave this page open until the process successfully completes\.
**Note**  
You might need to grant users or groups permissions to operate in the AWS Organizations management account\. Because it is a highly privileged account, additional security restrictions require you to have the [IAMFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/IAMFullAccess) policy or equivalent permissions before you can set this up\. These additional security restrictions are not required for any of the member accounts in your AWS organization\.

## Remove SSO user and group access<a name="howtoremoveaccess"></a>

Use this procedure to remove SSO access to an AWS account for one or more users and groups in your connected directory\.

**To remove SSO user and group access to an AWS account**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. On the **AWS Organization** page, a tree view list of your organization appears\. Select the name of the AWS account that contains the users and groups for whom you want to remove SSO access\.

1. On the **Overview** page for the AWS account, under **Assigned users and groups**, select the name of one or more users or groups, and choose **Remove access**\.

1. In the **Remove access** dialog box, confirm that the names of the users or groups are correct, and choose **Remove access**\. 

## Delegate who can assign SSO access to users and groups in the management account<a name="howtodelegatessoaccess"></a>

Assigning single sign\-on access to the management account using the AWS SSO console is a privileged action\. By default, only an AWS account root user, or a user who has the **AWSSSOMasterAccountAdministrator** and **IAMFullAccess** AWS managed policies attached, can assign SSO access to the management account\. The **AWSSSOMasterAccountAdministrator** and **IAMFullAccess** policies manage SSO access to the management account within an AWS Organizations organization\.

Use the following steps to delegate permissions to manage SSO access to users and groups in your directory\.

**To grant permissions to manage SSO access to users and groups in your directory**

1. Sign in to the AWS SSO console as a root user of the management account or with another IAM user who has IAM administrator permissions to the management account\.

1. Follow the steps in [Create a permission set](howtocreatepermissionset.md) to create a permission set, and then do the following:

   1. On the **Create new permission set** page, select the **Create a custom permission set** check box, and then choose **Next: Details**\.

   1. On the **Create new permission set page**, specify a name for the custom permission set and optionally, a description\. If required, modify the session duration and specify a relay state URL\.

   1. Under **What policies do you want to include in your permission set?**, select the **Attach AWS managed policies** check box\.

   1. In the list of IAM policies, choose both the **AWSSSOMasterAccountAdministrator** and **IAMFullAccess** AWS managed policies\. These policies grant permissions to any user and groups who are assigned access to this permission set in the future\.

   1. Choose **Next: Tags**\.

   1. Under **Add tags \(optional\)**, specify values for **Key** and **Value \(optional\)**, and then choose **Next: Review**\. For more information about tags, see [Tagging AWS Single Sign\-On resources](tagging.md)\.

   1. Review the selections you made, and then choose **Create**\.

1. Follow the steps in [Assign user access](#assignusers) to assign the appropriate users and groups to the permission set that you just created\.

1. Communicate the following to the assigned users: When they sign in to the user portal and select the **AWS Account** icon, they must choose the appropriate role name to be authenticated with the permissions that you just delegated\.
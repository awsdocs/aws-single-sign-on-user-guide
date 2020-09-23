# Single Sign\-On Access<a name="useraccess"></a>

You can assign users in your connected directory permissions to the master account or member accounts in your AWS Organizations organization based on [common job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html)\. Or you can use custom permissions to meet your specific security requirements\. For example, you can grant database administrators broad permissions to Amazon RDS in development accounts but limit their permissions in production accounts\. AWS SSO configures all the necessary user permissions in your AWS accounts automatically\.

**Note**  
If you need to grant users or groups permissions to operate in the AWS Organizations master account, because it is a highly privileged account, there are additional security restrictions which require you to have the [IAMFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/IAMFullAccess) policy or equivalent permissions before you can set this up\. These additional security restrictions are not required for any of the member accounts in your AWS organization\.

## Assign User Access<a name="assignusers"></a>

Use the following procedure to assign SSO access to users and groups in your connected directory and use permission sets to determine their level of access\.

**Note**  
To simplify administration of access permissions, we recommended that you assign access directly to groups rather than to individual users\. With groups you can grant or deny permissions to groups of users rather than having to apply those permissions to each individual\. If a user moves to a different organization, you simply move that user to a different group and they automatically receive the permissions that are needed for the new organization\.

**To assign access to users or groups**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the AWS SSO console is using the Region where your AWS Managed Microsoft AD directory is located before you move to the next step\.

1. Choose **AWS accounts**\.

1. Under the **AWS organization** tab, in the list of AWS accounts, choose one or more accounts to which you want to assign access\.
**Note**  
The AWS SSO Console supports selecting up to 10 AWS accounts at a time per permission set when assigning user access\. If you need to assign more than 10 AWS accounts to the same set of users, repeat this procedure for the additional accounts, selecting the same users and permission set when prompted\.

1. Choose **Assign users**\. 

1. On the **Select users or groups** page, type a user or group name to filter the results\. You can specify multiple users or groups by selecting the applicable accounts as they appear in search results, and then choose **Next: Permission sets**\. 

1. On the **Select permission sets** page, select the permission sets that you want to apply to the user\(s\) or group\(s\) from the table\. Then choose **Finish**\. You can optionally choose to **Create a new permission set** if none of the permissions in the table meets your needs\. For detailed instructions, see [Create Permission Set](howtocreatepermissionset.md)\. 

1. Choose **Finish** to begin the process of configuring your AWS account\.
**Note**  
If this is the first time you have assigned SSO access to this AWS account, this process creates a service\-linked role in the account\. For more information, see [Using Service\-Linked Roles for AWS SSO](using-service-linked-roles.md)\.
**Important**  
The user assignment process may take a few minutes to complete\. It is important that you leave this page open until the process successfully completes\.
**Note**  
If you need to grant users or groups permissions to operate in the AWS Organizations master account, because it is a highly privileged account, there are additional security restrictions which require you to have the [IAMFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/IAMFullAccess) policy or equivalent permissions before you can set this up\. These additional security restrictions are not required for any of the member accounts in your AWS organization\.

## Remove User Access<a name="howtoremoveaccess"></a>

Use this procedure when you need to remove SSO access to an AWS account for a particular user or group in your connected directory\.

**To remove user access from an AWS account**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. In the table, select the AWS account with the user or group whose access you want to remove\.

1. On the **Details** page for the AWS account, under **Assigned users and groups**, locate the user or group in the table\. Then choose **Remove access**\.

1. In the **Remove access** dialog box, confirm the user or group name\. Then choose **Remove access**\. 

## Delegate who can assign SSO access to users in the master account<a name="howtodelegatessoaccess"></a>

Assigning single sign\-on access to the master account using the AWS SSO console is a privileged action\. By default, only an AWS account root user, or a user who has the **AWSSSOMasterAccountAdministrator** and **IAMFullAccess** AWS managed policies attached, can assign SSO access to the master account\. The **AWSSSOMasterAccountAdministrator** and **IAMFullAccess** policies manage SSO access to the master account within an AWS Organizations organization\.

Use the following steps to delegate permissions to manage SSO access to users in your directory\.

**To grant permissions to manage SSO access to users in your directory**

1. Sign in to the AWS SSO console as a root user of the master account or with another IAM user who has IAM administrator permissions to the master account\.

1. Use the procedure [Create Permission Set](howtocreatepermissionset.md) to create a permission set\. When you get to the **Create new permission set** page,, select the **Create a custom permission set** option, choose **Next: Details**, and then select the option **Attach AWS managed policies**\. In the list of IAM policies that appear in the table, choose both the **AWSSSOMasterAccountAdministrator** and **IAMFullAccess** AWS managed policies\. These policies grant permissions to any user who will be assigned access to this permission set in the future\.

1. Use the procedure [Assign User Access](#assignusers) to assign the appropriate users to the permission set that you just created\.

1. Communicate the following to the assigned users: When they sign in to the user portal and select the **AWS Account** icon, they must choose the appropriate IAM role name to be authenticated with the permissions that you just delegated\.
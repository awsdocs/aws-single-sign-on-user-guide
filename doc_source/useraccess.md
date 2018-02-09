# Single Sign\-On Access<a name="useraccess"></a>

You can set up SSO access to one or more AWS accounts in your AWS organization by granting permissions to only those users who require it\. You can assign users permissions to these AWS accounts based on common job functions or use custom permissions to meet your specific security requirements\. For example, you can grant database administrators broad permissions to Amazon RDS in development accounts but limit their permissions in production accounts\. AWS SSO configures all the necessary user permissions in your AWS accounts automatically\.

## Assign User Access<a name="assignusers"></a>

Use the following procedure to assign SSO access to users and groups in your connected directory and use permission sets to determine their level of access\.

**Note**  
To simplify administration of access permissions, we recommended that you assign access directly to groups rather than to individual users\. With groups you can grant or deny permissions to groups of users rather than having to apply those permissions to each individual\. If a user moves to a different organization, you simply move that user to a different group and they automatically receive the permissions that are needed for the new organization\.

**To assign access to users or groups**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the AWS SSO console is using the US East \(N\. Virginia\) \(us\-east\-1\) Region where your AWS Microsoft AD directory is located before you move to the next step\.

1. Choose **AWS accounts**\.

1. Under the **AWS organization** tab, in the list of AWS accounts, choose an account to which you want to assign access\.
**Note**  
If you see a check box in the table that is disabled, this represents the master account for your AWS organization and is by design\. Please see the next step for more details\.

1. On the AWS account details page, choose **Assign users**\. 
**Note**  
If the **Assign users** button is disabled it indicates that this account is the master account for your AWS organization\. You can only assign SSO access to users in member accounts\. For more information about the different account types, see [AWS Organizations Terminology and Concepts](http://docs.aws.amazon.com/organizations/latest/userguide/orgs_getting-started_concepts.html) in the *AWS Organizations User Guide*\. 

1. On the **Select users or groups** page, type a user or group name and choose **Search connected directory**\. Once you have selected all the accounts that you want to assign access to, choose **Next: Permission sets**\. You can specify multiple users or groups by selecting the applicable accounts as they appear in search results\. 

1. On the **Select permission sets** page, select the permission sets that you want to apply to the user or group from the table\. Then choose **Finish**\. You can optionally choose to **Create a new permission set** if none of the permissions in the table meet your needs\. For detailed instructions, see [Create Permission Set](permissionsets.md#howtocreatepermissionset)\. 

1. Choose **Finish** to begin the process of configuring your AWS account\.
**Note**  
If this is the first time you have assigned SSO access to this AWS account, this process creates a service\-linked role in the account\. For more information, see [Using Service\-Linked Roles for AWS SSO](using-service-linked-roles.md)\.
**Important**  
The user assignment process may take a few minutes to complete\. It is important that you leave this page open until the process successfully completes\.

## Remove User Access<a name="howtoremoveaccess"></a>

Use this procedure when you need to remove SSO access to an AWS account for a particular user or group in your connected directory\.

**To remove user access from an AWS account**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. In the table select the AWS account with the user or group whose access you want to remove\.

1. On the **Details** page for the AWS account, under **Assigned users and groups**, locate the user or group in the table\. Then choose **Remove access**\.

1. In the **Remove access** dialog box, confirm the user or group name\. Then choose **Remove access**\. 
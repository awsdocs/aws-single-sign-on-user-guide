# Delete permission sets<a name="howtoremovepermissionset"></a>

Before you can delete a permission set from IAM Identity Center, you must remove it from all AWS accounts that use the permission set\.

**To remove a permission set from an AWS account**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Under **Multi\-account permissions**, choose **AWS accounts**\.

1. On the **AWS accounts** page, a tree view list of your organization appears\. Select the name of the AWS account from which you want to remove the permission set\.

1. On the **Overview** page for the AWS account, choose the **Permission sets** tab\.

1. Select the check box next to the permission set that you want to remove, and then choose **Remove**\.

1. In the **Remove permission set** dialog box, confirm that the correct permission set is selected, type **Delete** to confirm removal, and then choose **Remove access**\.

Use the following procedure to delete one or more permission sets so that they can no longer be used by any AWS account in the organization\.

**Note**  
All users and groups that have been assigned this permission set, regardless of what AWS account is using it, will no longer be able to sign in\.

**To delete a permission set from an AWS account**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Under **Multi\-account permissions**, choose **Permission sets**\.

1. Select the permission set that you want to delete, and then choose **Delete**\.

1. In the **Delete permission set** dialog box, type the name of the permission set to confirm deletion, and then choose **Delete**\. The name is case\-sensitive\.
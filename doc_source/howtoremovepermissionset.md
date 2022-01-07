# Delete permission sets<a name="howtoremovepermissionset"></a>

You must remove permission sets from the provisioned AWS accounts before deleting them from AWS SSO\.

**To remove a permission set from an AWS account**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. Under **AWS organization**, choose the **AWS account** from which you want to remove the permission set\.

1. Choose **Permission sets**\.

1. Choose **Remove** by the permission set that you want to remove\.

1. In the **Remove permission set** dialog box, choose **Remove access**\.

Use the following procedure to delete one or more permission sets so that they can no longer be used by any AWS account in the organization\.

**Note**  
All users and groups that have been assigned this permission set, regardless of what AWS account is using it, will no longer be able to sign in\.

**To delete a permission set from an AWS account**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. Choose the **Permission sets** tab\.

1. Select the permission set you want to delete, and then choose **Delete**\.

1. In the **Delete permission set** dialog box, choose **Delete**\.
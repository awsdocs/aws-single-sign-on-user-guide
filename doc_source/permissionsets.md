# Permission Sets<a name="permissionsets"></a>

Permission sets define the level of access that users and groups have to an AWS account\. Permission sets are stored in AWS SSO and provisioned to the AWS account as IAM roles\. You can assign more than one permission set to a user\. Users who have multiple permission sets must choose one when they sign in to the user portal\. \(Users will see these as IAM roles\)\. For more information, see [Permission Sets](permissionsetsconcept.md)\.

## Create Permission Set<a name="howtocreatepermissionset"></a>

Use this procedure to create a permission set based on a custom permissions policy that you create, or on predefined AWS managed policies that exist in IAM, or both\.

**To create a permission set**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. Select the **Permission sets** tab\.

1. Choose **Create permission set**\.

1. In the **Create new permission set** dialog box, choose from one of the following options, and then follow the instructions provided under that option:
   + **Use an existing job function policy**

     1. Under **Select job function policy**, select one of the default IAM job function policies in the list\. For more information, see [AWS Managed Policies for Job Functions](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html)\.

     1. Choose **Create**\.
   + **Create a custom permission set**

     1. Under **Create a custom permission set**, type a name that will identify this permission set in AWS SSO\. This name will also appear as an IAM role in the user portal for any users who have access to it\.

     1. \(Optional\) You can also type a description\. This description will only appear in the AWS SSO console and will not be visible to users in the user portal\.

     1. Select either **Attach AWS managed policies** or **Create a custom permissions policy**\. Or select both if you need to link more than one policy type to this permission set\.

     1. If you chose **Attach AWS managed policies**, under **Attach AWS Managed policies**, select up to 10 job\-related or service\-specific AWS managed policies from the list\. 

     1. If you chose **Create a custom permissions policy**, under **Create a custom permissions policy**, paste in a policy document with your preferred permissions\. For a list of example policies to use for delegating AWS SSO tasks, see [Customer Managed Policy Examples](iam-auth-access-using-id-policies.md#policyexample)\.

        For more information about the access policy language, see [Overview of Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) in the *IAM User Guide*\. To test the effects of this policy before applying your changes, use the [IAM policy simulator](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_testing-policies.html)\.

     1. Choose **Create**\.

## Delete Permission Sets<a name="howtoremovepermissionset"></a>

Use this procedure to delete one or more permission sets so that they can no longer be used by any AWS account in the organization\.

**Note**  
All users and groups that have been assigned this permission set, regardless of what AWS account is using it, will no longer be able to sign in\.

**To delete a permissions set from an AWS account**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. Choose the **Permission sets** tab\.

1. Select the permission set you want to delete, and then choose **Delete**\.

1. In the **Delete permission set** dialog box, choose **Delete**\.
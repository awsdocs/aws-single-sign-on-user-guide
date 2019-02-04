# Create Permission Set<a name="howtocreatepermissionset"></a>

Use this procedure to create a permission set based on a custom permissions policy that you create, or on predefined AWS managed policies that exist in IAM, or both\.

**To create a permission set**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. Select the **Permission sets** tab\.

1. Choose **Create permission set**\.

1. On the **Create new permission set** page, choose from one of the following options, and then follow the instructions provided under that option:
   + **Use an existing job function policy**

     1. Under **Select job function policy**, select one of the default IAM job function policies in the list\. For more information, see [AWS Managed Policies for Job Functions](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html)\.

     1. Choose **Create**\.
   + **Create a custom permission set**

     1. Under **Create a custom permission set**, type a name that will identify this permission set in AWS SSO\. This name will also appear as an IAM role in the user portal for any users who have access to it\.

     1. \(Optional\) You can also type a description\. This description will only appear in the AWS SSO console and will not be visible to users in the user portal\.

     1. \(Optional\) Specify the value for **Session duration**\. This value is used to determine the length of time a user can be logged on before the console logs them out of their session\. For more information, see [Set Session Duration](howtosessionduration.md)\.

     1. \(Optional\) Specify the value for **Relay state**\. This value is used in the federation process to redirect users within the account\. For more information, see [Set Relay State](howtopermrelaystate.md)\.

     1. Select either **Attach AWS managed policies** or **Create a custom permissions policy**\. Or select both if you need to link more than one policy type to this permission set\.

     1. If you chose **Attach AWS managed policies**, under **Attach AWS Managed policies**, select up to 10 job\-related or service\-specific AWS managed policies from the list\. 

     1. If you chose **Create a custom permissions policy**, under **Create a custom permissions policy**, paste in a policy document with your preferred permissions\. For a list of example policies to use for delegating AWS SSO tasks, see [Customer Managed Policy Examples](iam-auth-access-using-id-policies.md#policyexample)\.

        For more information about the access policy language, see [Overview of Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) in the *IAM User Guide*\. To test the effects of this policy before applying your changes, use the [IAM policy simulator](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_testing-policies.html)\.

     1. Choose **Create**\.
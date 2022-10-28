# Custom permissions<a name="permissionsetcustom"></a>

When you create a permission set with **Custom permissions**, you can combine any of the AWS managed and customer managed policies that you have in AWS Identity and Access Management \(IAM\) with *inline policies*, and a *permissions boundary* that sets the maximum possible permissions that any other policy can grant to users of your permission set\.

For a detailed walkthrough of the process to create a permission set, see [Create and manage permission sets](permissionsets.md)\.

**Policy types that you can attach to your permission set**

**Topics**
+ [Inline policies](#permissionsetsinlineconcept)
+ [AWS managed policies](#permissionsetsampconcept)
+ [Customer managed policies](#permissionsetscmpconcept)
+ [Permissions boundaries](#permissionsetsboundaryconcept)

## Inline policies<a name="permissionsetsinlineconcept"></a>

You can attach an *inline policy* to a permission set\. An inline policy is a block of text formatted as an IAM policy that you add directly to your permission set\. You can paste in a policy, or generate a new one with the policy creation tool in the IAM Identity Center console when you create a new permission set\. You can also create IAM policies with the [AWS Policy Generator](https://awspolicygen.s3.amazonaws.com/policygen.html)\.

When you deploy a permission set with an inline policy, IAM Identity Center creates an IAM policy in the AWS accounts where you assign your permission set\. IAM Identity Center creates the policy when you assign the permission set to the account\. The policy is then attached to the IAM role in your AWS account that your user assumes\.

When you create an inline policy and assign your permission set, IAM Identity Center configures the policies in your AWS accounts for you\. When you build your permission set with [Customer managed policies](#permissionsetscmpconcept), you must create the policies in your AWS accounts yourself before you assign the permission set\.

## AWS managed policies<a name="permissionsetsampconcept"></a>

You can attach *AWS managed policies* to your permission set\. AWS managed policies are IAM policies that AWS maintains\. In contrast, [Customer managed policies](#permissionsetscmpconcept) are IAM policies in your account that you create and maintain\. AWS managed policies address common least privilege use cases in your AWS account\. You can assign an AWS managed policy as permissions for the role that IAM Identity Center creates, or as a [permissions boundary](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_boundaries.html)\.

AWS maintains [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) that assign job\-specific access permissions to your AWS resources\. You can add one job\-function policy when you choose to use **Predefined permissions** with your permission set\. When you choose **Custom permissions**, you can add more than one job\-function policy\.

Your AWS account also contains a large number of AWS managed IAM policies for specific AWS services and combinations of AWS services\. When you create a permission set with **Custom permissions**, you can choose from many additional AWS managed policies to assign to your permission set\.

AWS populates every AWS account with AWS managed policies\. To deploy a permission set with AWS managed policies, you don't need to first create a policy in your AWS accounts\. When you build your permission set with [Customer managed policies](#permissionsetscmpconcept), you must create the policies in your AWS accounts yourself before you assign the permission set\.

For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the IAM User Guide\.

## Customer managed policies<a name="permissionsetscmpconcept"></a>

You can attach *customer managed policies* to your permission set\. Customer managed policies are IAM policies in your account that you create and maintain\. In contrast, [AWS managed policies](#permissionsetsampconcept) are IAM policies in your account that AWS maintains\. You can assign an customer managed policy as permissions for the role that IAM Identity Center creates, or as a [permissions boundary](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_boundaries.html)\.

When you create a permission set with a customer managed policy, you must create an IAM policy with the same name in each AWS account where IAM Identity Center assigns your permission set\. IAM Identity Center attaches the IAM policy to the IAM role that it creates in your AWS account\. As a best practice, apply the same permissions to the policy in each account where you assign the permission set\. For more information, see [Use IAM policies in permission sets](howtocmp.md)\.

For more information, see [Customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies) in the IAM User Guide\.

## Permissions boundaries<a name="permissionsetsboundaryconcept"></a>

You can attach a *permissions boundary* to your permission set\. A permissions boundary is an AWS managed or customer managed IAM policy that sets the maximum permissions that an identity\-based policy can grant to an IAM principal\. When you apply a permissions boundary, your [Inline policies](#permissionsetsinlineconcept), [Customer managed policies](#permissionsetscmpconcept), and [AWS managed policies](#permissionsetsampconcept) can't grant any permissions that exceed the permissions that your permissions boundary grants\. A permissions boundary doesn't grant any permissions, but instead makes it so that IAM ignores all permissions beyond the boundary\.

When you create a permission set with a customer managed policy as a permissions boundary, you must create an IAM policy with the same name in each AWS account where IAM Identity Center assigns your permission set\. IAM Identity Center attaches the IAM policy as a permissions boundary to the IAM role that it creates in your AWS account \.

For more information, see [Permissions boundaries for IAM entities](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_boundaries.html) in the IAM User Guide\.
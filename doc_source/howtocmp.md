# Use IAM policies in permission sets<a name="howtocmp"></a>

In [Create a permission set](howtocreatepermissionset.md), you learned how to add policies, including customer managed policies and permissions boundaries, to a permission set\. When you add customer managed policies and permissions to a permission set, IAM Identity Center doesn't create a policy in any AWS accounts\. You must instead create those policies in advance in each account where you want to assign your permission set, and match them to the name and path specifications of your permission set\. When you assign a permission set to an AWS account in your organization, IAM Identity Center creates an [AWS Identity and Access Management \(IAM\) role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) and attaches your [IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) to that role\. 

**Note**  
Before you assign your permission set with IAM policies, you must prepare your member account\. The name of an IAM policy in your member account must be a case\-sensitive match to name of the policy in your management account\. IAM Identity Center fails to assign the permission set if the policy doesn't exist in your member account\.  
The permissions that the policy grants don't have to be an exact match between accounts\.

# To assign an IAM policy to a permission set

1. Create an IAM policy in each of the AWS accounts where you want to assign the permission set\.

1. Assign permissions to the IAM policy\. You can assign different permissions in different accounts\. For a consistent experience, configure and maintain identical permissions in each policy\. You can use automation resources like AWS CloudFormation StackSets to create copies of an IAM policy with the same name and permissions in each member account\. For more information about CloudFormation StackSets, see [Working with AWS CloudFormation StackSets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/what-is-cfnstacksets.html) in the *AWS CloudFormation User guide*\.

1. Create a permission set in your management account and add your IAM policy under **Customer managed policies** or **Permissions boundary**\. For more details about how to create a permission set, See [Create a permission set](howtocreatepermissionset.md)\.

1. Add any inline policies, AWS managed policies, or additional IAM policies that you have prepared\. 

1. Create and assign your permission set\.
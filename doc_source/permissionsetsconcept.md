# Permission sets<a name="permissionsetsconcept"></a>

A permission set is a template that you create and maintain that defines a collection of one or more [IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)\. Permission sets simplify the assignment of AWS account access for users and groups in your organization\. For example, you can create a *Database Admin* permission set that includes policies for administering AWS RDS, DynamoDB, and Aurora services, and use that single permission set to grant access to a list of target AWS accounts within your [AWS Organization](https://aws.amazon.com/organizations/) for your database administrators\.

IAM Identity Center assigns access to a user or group in one or more AWS accounts with permission sets\. When you assign a permission set, IAM Identity Center creates corresponding IAM Identity Center\-controlled IAM roles in each account, and attaches the policies specified in the permission set to those roles\. IAM Identity Center manages the role, and allows the authorized users you’ve defined to assume the role, by using the IAM Identity Center User Portal or AWS CLI\.  As you modify the permission set, IAM Identity Center ensures that the corresponding IAM policies and roles are updated accordingly\.

You can add [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies), [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies), inline policies, and [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) to your permission sets\. You can also assign an AWS managed policy or a customer managed policy as a [permissions boundary](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_boundaries.html)\.

To create a permission set, see [Create and manage permission sets](permissionsets.md)\.

**Topics**
+ [Predefined permissions](permissionsetpredefined.md)
+ [Custom permissions](permissionsetcustom.md)
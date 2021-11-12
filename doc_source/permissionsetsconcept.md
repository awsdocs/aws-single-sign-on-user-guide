# Permission sets<a name="permissionsetsconcept"></a>

A permission set is a template that you create and maintain that defines a collection of one or more [IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)\. Permission sets simplify the assignment of AWS account access for users and groups in your organization\. For example, you can create a “database admin” permission set that includes policies for administering AWS RDS, DynamoDB, and Aurora services, and use that single permission set to grant access to a list of target AWS accounts within your [AWS Organization](https://aws.amazon.com/organizations/) for your database administrators\.

When you use AWS SSO to assign a user or group access to one or more AWS accounts, you specify a permission set to define the access that those users or groups will have in the selected AWS accounts\. At that time, AWS SSO creates corresponding AWS SSO\-controlled IAM roles in each account, and attaches the policies specified in the permission set to those roles\. AWS SSO manages the role, and allows the authorized users you’ve defined to assume the role, via the AWS SSO User Portal or AWS CLI\.  As you modify the permission set, AWS SSO ensures that the corresponding IAM policies and roles are updated accordingly\.

## Delegating permission set administration<a name="permissionsetdelegation"></a>

AWS SSO enables you to delegate management of permission sets and assignments in accounts by creating [IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) that reference the [Amazon Resource Names \(ARNs\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) of AWS SSO resources\. For example, you can create policies that enable different administrators to manage assignments in specified accounts for permission sets with specific tags\.

You can use any of the following three methods to create these kinds of policies\.
+ \(Recommended\) Create [permission sets](https://docs.aws.amazon.com/en_us/singlesignon/latest/userguide/permissionsets.html) in AWS SSO, each with a different policy, and assign the permission sets to different users or groups\. This enables you to manage administrative permissions for users that sign in using your chosen [AWS SSO identity source](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source.html)\. 
+ Create [custom policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#best-practice-managed-vs-inline) in IAM, and then attach them to IAM roles that your administrators assume\. This enables [IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html) or [IAM federated users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html) to [assume the role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) to get their assigned AWS SSO administrative permissions\.
+ Create [custom policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#best-practice-managed-vs-inline) in IAM, and then attach them to IAM users that you use for AWS SSO administrator purposes\. This enables you to give individual IAM users specific AWS SSO administrative permissions\.

**Important**  
AWS SSO resource ARNs are case sensitive\. 

The following shows the proper case for referencing the AWS SSO permission set and account resource types\.


| Resource Types | ARN | Context Keys | 
| --- | --- | --- | 
| PermissionSet | arn:$\{Partition\}:sso:::permissionSet/$\{InstanceId\}/$\{PermissionSetId\} | aws:ResourceTag/$\{TagKey\} | 
| Account | arn:$\{Partition\}:sso:::account/$\{AccountId\} | Not Applicable | 
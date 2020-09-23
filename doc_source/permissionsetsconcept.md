# Permission Sets<a name="permissionsetsconcept"></a>

A permission set is a collection of administrator\-defined policies that AWS SSO uses to determine a user's effective permissions to access a given AWS account\. Permission sets can contain either [AWS managed policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) or custom policies that are stored in AWS SSO\. Policies are essentially documents that act as containers for one or more permission statements\. These statements represent individual access controls \(allow or deny\) for various tasks that determine what tasks users can or cannot perform within the AWS account\.

Permission sets are stored in AWS SSO and are only used for AWS accounts\. They are not used to manage access to cloud applications\. Permission sets ultimately get created as [IAM roles](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) in a given AWS account, with trust policies that allow users to assume the role through AWS SSO\.

## Delegating Permission Set Administration<a name="permissionsetdelegation"></a>

AWS SSO enables you to delegate management of permission sets and assignments in accounts by creating [IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) that reference the [Amazon Resource Names \(ARNs\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) of AWS SSO resources\. For example, you can create policies that enable different administrators to manage assignments in specified accounts for permission sets with specific tags\.

You can use any of the following three methods to create these kinds of policies\.
+ \(Recommended\) Create permission sets in AWS SSO, each with a different policy, and assign the permission sets to different users or groups\. This enables you to manage administrative permissions for users that sign in using your chosen [AWS SSO identity source](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source.html)\. 
+ Create [custom policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#best-practice-managed-vs-inline) in IAM, and then attach them to IAM roles that your administrators assume\. This enables [IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html) or [IAM federated users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html) to [assume the role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) to get their assigned AWS SSO administrative permissions\.
+ Create [custom policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#best-practice-managed-vs-inline) in IAM, and then attach them to IAM users that you use for AWS SSO administrator purposes\. This enables you to give individual IAM users specific AWS SSO administrative permissions\.

**Important**  
AWS SSO resource ARNs are case sensitive\. 

The following shows the proper case for referencing the AWS SSO permission set and account resource types\.


| Resource Types | ARN | Context Keys | 
| --- | --- | --- | 
| PermissionSet | arn:$\{Partition\}:sso:::permissionSet/$\{InstanceId\}/$\{PermissionSetId\} | aws:ResourceTag/$\{TagKey\} | 
| Account | arn:$\{Partition\}:sso:::account/$\{AccountId\} | Not Applicable | 
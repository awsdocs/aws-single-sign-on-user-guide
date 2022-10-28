# Delegate permission set administration<a name="permissionsetdelegation"></a>

IAM Identity Center enables you to delegate management of permission sets and assignments in accounts by creating [IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) that reference the [Amazon Resource Names \(ARNs\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) of IAM Identity Center resources\. For example, you can create policies that enable different administrators to manage assignments in specified accounts for permission sets with specific tags\.

You can use any of the following three methods to create these kinds of policies\.
+ \(Recommended\) Create [permission sets](https://docs.aws.amazon.com/en_us/singlesignon/latest/userguide/permissionsets.html) in IAM Identity Center, each with a different policy, and assign the permission sets to different users or groups\. This enables you to manage administrative permissions for users that sign in using your chosen [IAM Identity Center identity source](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source.html)\. 
+ Create [custom policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#best-practice-managed-vs-inline) in IAM, and then attach them to IAM roles that your administrators assume\. This enables [IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html) or [IAM federated users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html) to [assume the role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) to get their assigned IAM Identity Center administrative permissions\.
+ Create [custom policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#best-practice-managed-vs-inline) in IAM, and then attach them to IAM users that you use for IAM Identity Center administrator purposes\. This enables you to give individual IAM users specific IAM Identity Center administrative permissions\.

**Important**  
IAM Identity Center resource ARNs are case sensitive\. 

The following shows the proper case for referencing the IAM Identity Center permission set and account resource types\.


| Resource Types | ARN | Context Keys | 
| --- | --- | --- | 
| PermissionSet | arn:$\{Partition\}:sso:::permissionSet/$\{InstanceId\}/$\{PermissionSetId\} | aws:ResourceTag/$\{TagKey\} | 
| Account | arn:$\{Partition\}:sso:::account/$\{AccountId\} | Not Applicable | 
# Overview of managing access permissions to your IAM Identity Center resources<a name="iam-auth-access-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access the resources are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. Some services \(such as AWS Lambda\) also support attaching permissions policies to resources\.

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific actions that you want to allow on those resources\. 

**Topics**
+ [IAM Identity Center resources and operations](#creatingiampolicies)
+ [Understanding resource ownership](#accesscontrolresourceowner)
+ [Managing access to resources](#accesscontrolmanagingaccess)
+ [Specifying policy elements: actions, effects, resources, and principals](#policyactions)
+ [Specifying conditions in a policy](#specifyiampolicyconditions)

## IAM Identity Center resources and operations<a name="creatingiampolicies"></a>

In IAM Identity Center, the primary resources are application instances, profiles, and permission sets\. 

## Understanding resource ownership<a name="accesscontrolresourceowner"></a>

A *resource owner* is the AWS account that created a resource\. That is, the resource owner is the AWS account of the *principal entity* \(the account, an IAM user, or an IAM role\) that authenticates the request that creates the resource\. The following examples illustrate how this works: 
+ If the AWS account root user creates an IAM Identity Center resource, such as an application instance or permission set, your AWS account is the owner of that resource\.
+ If you create an IAM user in your AWS account and grant that user permissions to create IAM Identity Center resources, the user can then create IAM Identity Center resources\. However, your AWS account, to which the user belongs, owns the resources\.
+ If you create an IAM role in your AWS account with permissions to create IAM Identity Center resources, anyone who can assume the role can create IAM Identity Center resources\. Your AWS account, to which the role belongs, owns the IAM Identity Center resources\. 

## Managing access to resources<a name="accesscontrolmanagingaccess"></a>

A *permissions policy* describes who has access to what\. The following section explains the available options for creating permissions policies\.

**Note**  
This section discusses using IAM in the context of IAM Identity Center\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM policy reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies that are attached to an IAM identity are referred to as *identity\-based* policies \(IAM policies\)\. Policies that are attached to a resource are referred to as *resource\-based* policies\. IAM Identity Center supports only identity\-based policies \(IAM policies\)\.

**Topics**
+ [Identity\-based policies \(IAM policies\)](#accesscontrolidentitybased)
+ [Resource\-based policies](#accesscontrolresourcebased)

### Identity\-based policies \(IAM policies\)<a name="accesscontrolidentitybased"></a>

You can attach policies to IAM identities\. For example, you can do the following: 
+ **Attach a permissions policy to a user or a group in your account** – An account administrator can use a permissions policy that is associated with a particular user to grant permissions for that user to add an IAM Identity Center resource, such as a new application\. 
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows: 

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions to resources in Account A\.

  1. Account A administrator attaches a trust policy to the role identifying Account B as the principal who can assume the role\. 

  1. Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. The principal in the trust policy can also be an AWS service principal if you want to grant an AWS service permissions to assume the role\.

   For more information about using IAM to delegate permissions, see [Access management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. 

The following permissions policy grants permissions to a user to run all of the actions that begin with `List`\. These actions show information about an IAM Identity Center resource, such as an application instance or permissions set\. Note that the wildcard character \(\*\) in the `Resource` element indicates that the actions are allowed for all IAM Identity Center resources that are owned by the account\. 

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action":"sso:List*",
 7.          "Resource":"*"
 8.       }
 9.    ]
10. }
```

For more information about using identity\-based policies with IAM Identity Center, see [Identity\-based policy examples for IAM Identity Center](iam-auth-access-using-id-policies.md)\. For more information about users, groups, roles, and permissions, see [Identities \(users, groups, and roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-based policies<a name="accesscontrolresourcebased"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. IAM Identity Center doesn't support resource\-based policies\. 

## Specifying policy elements: actions, effects, resources, and principals<a name="policyactions"></a>

For each IAM Identity Center resource \(see [IAM Identity Center resources and operations](#creatingiampolicies)\), the service defines a set of API operations\.  To grant permissions for these API operations, IAM Identity Center defines a set of actions that you can specify in a policy\. Note that performing an API operation can require permissions for more than one action\. 

The following are the basic policy elements:
+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For IAM Identity Center resources, you always use the wildcard character \(\*\) in IAM policies\. For more information, see [IAM Identity Center resources and operations](#creatingiampolicies)\. 
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, the `sso:DescribePermissionsPolicies` permission allows the user permissions to perform the IAM Identity Center `DescribePermissionsPolicies` operation\. 
+ **Effect** – You specify the effect when the user requests the specific action—this can be either allow or deny\. If you don't explicitly grant access to \(allow\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. For resource\-based policies, you specify the user, account, service, or other entity that you want to receive permissions \(applies to resource\-based policies only\)\. IAM Identity Center doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [AWS IAM policy reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

## Specifying conditions in a policy<a name="specifyiampolicyconditions"></a>

When you grant permissions, you can use the access policy language to specify the conditions that are required for a policy to take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to IAM Identity Center\. However, there are AWS condition keys that you can use as appropriate\. For a complete list of AWS keys, see [Available global condition keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#AvailableKeys) in the *IAM User Guide*\.  
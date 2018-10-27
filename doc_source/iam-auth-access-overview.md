# Overview of Managing Access Permissions to Your AWS SSO Resources<a name="iam-auth-access-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access the resources are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. Some services \(such as AWS Lambda\) also support attaching permissions policies to resources\.

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific actions that you want to allow on those resources\. 

**Topics**
+ [AWS SSO Resources and Operations](#creatingiampolicies)
+ [Understanding Resource Ownership](#accesscontrolresourceowner)
+ [Managing Access to Resources](#accesscontrolmanagingaccess)
+ [Specifying Policy Elements: Actions, Effects, Resources, and Principals](#policyactions)
+ [Specifying Conditions in a Policy](#specifyiampolicyconditions)

## AWS SSO Resources and Operations<a name="creatingiampolicies"></a>

In AWS SSO, the primary resources are application instances, profiles, and permission sets\. 

## Understanding Resource Ownership<a name="accesscontrolresourceowner"></a>

A *resource owner* is the AWS account that created a resource\. That is, the resource owner is the AWS account of the *principal entity* \(the account, an IAM user, or an IAM role\) that authenticates the request that creates the resource\. The following examples illustrate how this works: 
+ If the AWS account root user creates an AWS SSO resource, such as an application instance or permission set, your AWS account is the owner of that resource\.
+ If you create an IAM user in your AWS account and grant that user permissions to create AWS SSO resources, the user can then create AWS SSO resources\. However, your AWS account, to which the user belongs, owns the resources\.
+ If you create an IAM role in your AWS account with permissions to create AWS SSO resources, anyone who can assume the role can create AWS SSO resources\. Your AWS account, to which the role belongs, owns the AWS SSO resources\. 

## Managing Access to Resources<a name="accesscontrolmanagingaccess"></a>

A *permissions policy* describes who has access to what\. The following section explains the available options for creating permissions policies\.

**Note**  
This section discusses using IAM in the context of AWS SSO\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies that are attached to an IAM identity are referred to as *identity\-based* policies \(IAM policies\)\. Policies that are attached to a resource are referred to as *resource\-based* policies\. AWS SSO supports only identity\-based policies \(IAM policies\)\.

**Topics**
+ [Identity\-Based Policies \(IAM Policies\)](#accesscontrolidentitybased)
+ [Resource\-Based Policies](#accesscontrolresourcebased)

### Identity\-Based Policies \(IAM Policies\)<a name="accesscontrolidentitybased"></a>

You can attach policies to IAM identities\. For example, you can do the following: 
+ **Attach a permissions policy to a user or a group in your account** – An account administrator can use a permissions policy that is associated with a particular user to grant permissions for that user to add an AWS SSO resource, such as a new application\. 
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows: 

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions to resources in Account A\.

  1. Account A administrator attaches a trust policy to the role identifying Account B as the principal who can assume the role\. 

  1. Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. The principal in the trust policy can also be an AWS service principal if you want to grant an AWS service permissions to assume the role\.

   For more information about using IAM to delegate permissions, see [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. 

The following permissions policy grants permissions to a user to run all of the actions that begin with `List`\. These actions show information about an AWS SSO resource, such as an application instance or permissions set\. Note that the wildcard character \(\*\) in the `Resource` element indicates that the actions are allowed for all AWS SSO resources that are owned by the account\. 

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

For more information about using identity\-based policies with AWS SSO, see [Using Identity\-Based Policies \(IAM Policies\) for AWS SSO](iam-auth-access-using-id-policies.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-Based Policies<a name="accesscontrolresourcebased"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. AWS SSO doesn't support resource\-based policies\. 

## Specifying Policy Elements: Actions, Effects, Resources, and Principals<a name="policyactions"></a>

For each AWS SSO resource \(see [AWS SSO Resources and Operations](#creatingiampolicies)\), the service defines a set of API operations\.  To grant permissions for these API operations, AWS SSO defines a set of actions that you can specify in a policy\. Note that performing an API operation can require permissions for more than one action\. 

The following are the basic policy elements:
+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For AWS SSO resources, you always use the wildcard character \(\*\) in IAM policies\. For more information, see [AWS SSO Resources and Operations](#creatingiampolicies)\. 
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, the `sso:DescribePermissionsPolicies` permission allows the user permissions to perform the AWS SSO `DescribePermissionsPolicies` operation\. 
+ **Effect** – You specify the effect when the user requests the specific action—this can be either allow or deny\. If you don't explicitly grant access to \(allow\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. For resource\-based policies, you specify the user, account, service, or other entity that you want to receive permissions \(applies to resource\-based policies only\)\. AWS SSO doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

## Specifying Conditions in a Policy<a name="specifyiampolicyconditions"></a>

When you grant permissions, you can use the access policy language to specify the conditions that are required for a policy to take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to AWS SSO\. However, there are AWS condition keys that you can use as appropriate\. For a complete list of AWS keys, see [Available Global Condition Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#AvailableKeys) in the *IAM User Guide*\.  
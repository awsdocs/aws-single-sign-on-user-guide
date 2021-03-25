# Identity and access management for AWS SSO<a name="iam-auth-access"></a>

Access to AWS SSO requires credentials that AWS can use to authenticate your requests\. Those credentials must have permissions to access AWS resources, such as an AWS SSO application\. 

Authentication to the AWS SSO user portal is controlled by the directory that you have connected to AWS SSO\. However, authorization to the AWS accounts that are available to end users from within the user portal is determined by two factors:

1. Who has been assigned access to those AWS accounts in the AWS SSO console\. For more information, see [Single sign\-on access](useraccess.md)\.

1. What level of permissions have been granted to the end users in the AWS SSO console to allow them the appropriate access to those AWS accounts\. For more information, see [Permission sets](permissionsets.md)\.

The following sections explain how you as an administrator can control access to the AWS SSO console or can delegate administrative access for day\-to\-day tasks from the AWS SSO console\. 
+ [Authentication](#authentication)
+ [Access control](#accesscontrol)

## Authentication<a name="authentication"></a>

You can access AWS as any of the following types of identities:
+ **AWS account root user** –  When you first create an AWS account, you begin with a single sign\-in identity that has complete access to all AWS services and resources in the account\. This identity is called the AWS account *root user* and is accessed by signing in with the email address and password that you used to create the account\. We strongly recommend that you do not use the root user for your everyday tasks, even the administrative ones\. Instead, adhere to the [best practice of using the root user only to create your first IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#create-iam-users)\. Then securely lock away the root user credentials and use them to perform only a few account and service management tasks\. 
+ **IAM user** – An [IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html) is an identity within your AWS account that has specific custom permissions \(for example, permissions to create a directory in AWS SSO\)\. You can use an IAM user name and password to sign in to secure AWS webpages like the [AWS Management Console](https://console.aws.amazon.com/), [AWS Discussion Forums](https://forums.aws.amazon.com/), or the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

   

  In addition to a user name and password, you can also generate [access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) for each user\. You can use these keys when you access AWS services programmatically, either through [one of the several SDKs](https://aws.amazon.com/tools/#sdk) or by using the [AWS Command Line Interface \(CLI\)](https://aws.amazon.com/cli/)\. The SDK and CLI tools use the access keys to cryptographically sign your request\. If you don’t use AWS tools, you must sign the request yourself\. AWS SSO supports *Signature Version 4*, a protocol for authenticating inbound API requests\. For more information about authenticating requests, see [Signature Version 4 Signing Process](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html) in the *AWS General Reference*\.

   
+ **IAM role** –  An [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) is an IAM identity that you can create in your account that has specific permissions\. An IAM role is similar to an IAM user in that it is an AWS identity with permissions policies that determine what the identity can and cannot do in AWS\. However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it\. Also, a role does not have standard long\-term credentials such as a password or access keys associated with it\. Instead, when you assume a role, it provides you with temporary security credentials for your role session\. IAM roles with temporary credentials are useful in the following situations:

   
  + **Federated user access** –  Instead of creating an IAM user, you can use existing identities from AWS Directory Service, your enterprise user directory, or a web identity provider\. These are known as *federated users*\. AWS assigns a role to a federated user when access is requested through an [identity provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html)\. For more information about federated users, see [Federated users and roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_access-management.html#intro-access-roles) in the *IAM User Guide*\. 

     
  + **AWS service access** –  A service role is an [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) that a service assumes to perform actions on your behalf\. Service roles provide access only within your account and cannot be used to grant access to services in other accounts\. An IAM administrator can create, modify, and delete a service role from within IAM\. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html) in the *IAM User Guide*\. 

      
  + **Applications running on Amazon EC2** –  You can use an IAM role to manage temporary credentials for applications that are running on an EC2 instance and making AWS CLI or AWS API requests\. This is preferable to storing access keys within the EC2 instance\. To assign an AWS role to an EC2 instance and make it available to all of its applications, you create an instance profile that is attached to the instance\. An instance profile contains the role and enables programs that are running on the EC2 instance to get temporary credentials\. For more information, see [Using an IAM role to grant permissions to applications running on Amazon EC2 instances](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html) in the *IAM User Guide*\. 

    

## Access control<a name="accesscontrol"></a>

You can have valid credentials to authenticate your requests, but unless you have permissions you cannot create or access AWS SSO resources\. For example, you must have permissions to create an AWS SSO connected directory\.

The following sections describe how to manage permissions for AWS SSO\. We recommend that you read the overview first\.

 
+ [Overview of managing access permissions to your AWS SSO resources](iam-auth-access-overview.md)
+  [Using identity\-based policies \(IAM policies\) for AWS SSO](iam-auth-access-using-id-policies.md) 
+  [Using service\-linked roles for AWS SSO](using-service-linked-roles.md) 
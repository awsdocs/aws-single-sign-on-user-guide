# Service\-linked roles<a name="slrconcept"></a>

[Service\-linked roles](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html?icmpid=docs_iam_console#iam-term-service-linked-role) are predefined IAM permissions that allow AWS SSO to delegate and enforce which users have SSO access to specific AWS accounts in your organization in AWS Organizations\. The service enables this functionality by provisioning a service\-linked role in every AWS account within its organization\. The service then allows other AWS services like AWS SSO to leverage those roles to perform service\-related tasks\. For more information, see [AWS Organizations and service\-linked roles](http://docs.aws.amazon.com/organizations/latest/userguide/orgs_integrate_services.html#orgs_integrate_services-using_slrs)\.

During the process to [Enable AWS SSO](step1.md), AWS SSO creates a service\-linked role in all accounts within the organization in AWS Organizations\. AWS SSO also creates the same service\-linked role in every account that is subsequently added to your organization\. This role allows AWS SSO to access each account's resources on your behalf\. For more information, see [Manage SSO access to your AWS accounts](manage-your-accounts.md)\. 

Service\-linked roles that are created in each AWS account are named `AWSServiceRoleForSSO`\. For more information, see [Using service\-linked roles for AWS SSO](using-service-linked-roles.md)\.
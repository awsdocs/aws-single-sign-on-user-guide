# Set Up SSO to Your AWS Accounts<a name="step3"></a>

In this step, you can grant users in your directory with SSO access to one or more AWS consoles for specific AWS accounts in your organization in AWS Organizations\. When you do, AWS SSO uses the [service\-linked role](using-service-linked-roles.md) that was created during enablement to create IAM roles\. Your end users can access their AWS accounts using these new roles\.

Users within these accounts see only the AWS account icon \(for example, Development\) that they've been assigned from within their user portal\. When they choose the icon, they can then choose which IAM role they want to use when signing in to the AWS Management Console for that AWS account\. 

To get started assigning SSO access to your AWS accounts, see [Assign User Access](useraccess.md#assignusers)\.
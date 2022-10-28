# Enable single sign\-on access to your AWS EC2 Windows instances<a name="use-case-ec2"></a>

## <a name="enable-sso-access-ec2"></a>

This use case provides guidance for application administrators who manage users in an AWS IAM Identity Center \(successor to AWS Single Sign\-On\) identity store or supported external identity provider, and need to provide IAM Identity Center access to their EC2 Windows desktops from the AWS Fleet Manager console\.

This allows you to securely access your EC2 Windows instances with existing corporate user names, passwords, and MFA devices\. You are no longer required to share administrator credentials, access credentials multiple times, or configure remote access client software\. You can centrally grant and revoke access to your EC2 Windows instances at scale across multiple AWS accounts\. For example, if you remove an employee from your IAM Identity Center integrated identity source, they automatically lose access to all AWS resources, including EC2 Windows instances\.

For more information, see [ How to enable secure seamless single sign\-on to Amazon EC2 Windows instances with IAM Identity Center](https://aws.amazon.com/blogs/security/how-to-enable-secure-seamless-single-sign-on-to-amazon-ec2-windows-instances-with-aws-sso/)\.

For a demonstration of how to configure IAM Identity Center to enable this capability, see [Enabling Single Sign\-on to EC2 Windows with IAM Identity Center](https://www.youtube.com/watch?v=gUUYLK67L8U)\. 
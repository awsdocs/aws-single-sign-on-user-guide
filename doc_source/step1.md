# Enable AWS SSO<a name="step1"></a>

When you open the AWS SSO console for the first time, you are prompted to enable AWS SSO before you can start managing SSO\. If you have already chosen this option, you can skip this step\. If not, use the procedure below to enable it now\. Once enabled, AWS SSO is granted the necessary permissions to create IAM service\-linked roles in any of the AWS accounts within your AWS organization\. No service\-linked roles are created at this time\. AWS SSO creates these roles later during the process of setting up SSO access to your AWS accounts \(see [Set Up SSO to Your AWS Accounts](step3.md)\)\.

**To enable AWS SSO**

1. Sign in to the AWS Management Console with your AWS Organizations master account credentials\.

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Enable AWS SSO**\.
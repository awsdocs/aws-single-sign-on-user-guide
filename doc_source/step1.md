# Enable AWS SSO<a name="step1"></a>

When you open the AWS SSO console for the first time, you are prompted to enable AWS SSO before you can start managing it\. If you have already chosen this option, you can skip this step\. If not, use the procedure below to enable it now\. Once enabled, AWS SSO creates a [service\-linked role](using-service-linked-roles.md) in all accounts within the organization in AWS Organizations\. AWS SSO also creates the same service\-linked role in every account that is subsequently added to your organization\. This role allows AWS SSO to access each account's resources on your behalf\. 

**Note**  
If you need to grant users or groups permissions to operate in the AWS Organizations master account, because it is a highly privileged account, there are additional security restrictions which require you to have the [IAMFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/IAMFullAccess) policy or equivalent permissions before you can set this up\. These additional security restrictions are not required for any of the member accounts in your AWS organization\.

**To enable AWS SSO**

1. Sign in to the AWS Management Console with your AWS Organizations master account credentials\.

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Enable AWS SSO**\.

1. If you have not yet set up AWS Organizations, you will be prompted to create an organization\. Choose **Create AWS organization** to complete this process\.
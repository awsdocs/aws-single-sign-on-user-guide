# Step 1: Enable IAM Identity Center<a name="get-started-enable-identity-center"></a>

To perform the following steps, you'll sign in to the AWS Management Console as the AWS account root user\. To enhance the security of your root user credentials, make sure that multi\-factor authentication \(MFA\) is activated for your root user before you proceed\. For more information, see [Activate MFA on the AWS account root user](https://docs.aws.amazon.com/accounts/latest/reference/root-user-mfa.html) in the *AWS Account Management Reference Guide*\.

**To enable IAM Identity Center**

1. Sign in to the AWS Management Console with your AWS account root user credentials\. For more information, see [Sign in as the root user](https://docs.aws.amazon.com/IAM/latest/UserGuide/console.html#root-user-sign-in-page)\.

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Under **Enable IAM Identity Center**, choose **Enable**\.

1. IAM Identity Center requires AWS Organizations\. If you haven't set up an organization, you must choose whether to have AWS create one for you\. Choose **Create AWS organization** to complete this process\.

   AWS Organizations automatically sends a verification email to the address that is associated with your management account\. There might be a delay before you receive the verification email\. Verify your email address within 24 hours\. 

**Note**  
If you are using a multi\-account environment, we recommend that you configure delegated administration\. With delegated administration, you can limit the number of people who require access to the management account in AWS Organizations\. For more information, see [Delegated administration](delegated-admin.md)\.
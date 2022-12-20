# Send email OTP for users created from API<a name="userswithoutpwd"></a>

When you create users with the [CreateUser](https://docs.aws.amazon.com/singlesignon/latest/IdentityStoreAPIReference/API_CreateUser.html) API operation, they do not have passwords\. You can change this by electing to send users an email one\-time password \(OTP\) when they're created with the API\. Users receive the email OTP when they first attempt to sign in\. After receiving the email OTP, when a user signs in, they must set a new password\. If you don’t enable this setting, then you must generate and share OTP with the users that you create using the **CreateUser** API\.

**To send email OTP to users created with the **CreateUser** API**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Authentication** tab\.

1. In the **Standard authentication** section, choose **Configure**\.

1. A dialog box appears\. Check the box next to **Send email OTP**\. Then, choose **Save**\. The status updates from **Disabled** to **Enabled**\.
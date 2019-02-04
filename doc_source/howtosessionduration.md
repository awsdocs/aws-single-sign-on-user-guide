# Set Session Duration<a name="howtosessionduration"></a>

For each permission set, you can specify a session duration to control the length of time that a user can be signed in to an AWS account\. When the specified duration has elapsed, AWS logs the user out of the session\. For AWS accounts, AWS SSO uses this setting to set the maximum session duration of the IAM role that you use to generate a user’s session\. The session duration that you specify for a given permission set applies to both the AWS Management Console and the AWS Command Line Interface \(CLI\) session\.

When you create a new permission set, it comes configured with the default session length of 1 hour \(in seconds\)\. The minimum session duration length is 1 hour and can be configured up to 12 hours\. 

**Important**  
As a security best practice, we recommend that you do not set the session duration length longer than is needed to perform the role\.

Once a permission set has been created, you can later update it to apply a new session duration\. When you reapply the permission set to your AWS accounts, the IAM role’s maximum session duration value is updated\. Use the following procedure to modify the session duration length for a given permission set\.

**To set the session duration**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. Choose the **Permission sets** tab\.

1. Choose the name of the permission set that will have the new session duration\.

1. On the **Permissions** tab, next to **Session duration**, choose **Edit**\.

1. On the **Edit session duration** page, next to **New session duration**, choose a new session length value, and then choose **Continue**\.

1. Select the AWS accounts in the list that you want the new session duration value to apply to, and then choose **Reapply permission set**\.
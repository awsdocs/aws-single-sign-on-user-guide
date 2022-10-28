# Configure AWS access portal session duration<a name="configure-user-session"></a>

Use the following procedure to configure the AWS access portal session duration for all your users\.

**Note**  
If you have an external identity provider \(IdP\) connected to IAM Identity Center, the AWS access portal session duration will be the lesser of the session duration you set in your IdP or the session duration you set here\. For example, if your IdP session duration is 24 hours and you set an 18 hour session duration in IAM Identity Center, the users must re\-authenticate in the AWS access portal after 18 hours\. If you set a 72 hour session duration here and your IdP has a session duration of 18 hours, your users must re\-authenticate after 18 hours\.

**Note**  
CLI\-based sessions are not impacted by how you configure AWS access portal sessions and their duration remains at 8 hours\.

**To configure an AWS access portal session duration**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Authentication** tab\.

1. Under **Authentication**, next to **Session settings**, choose **Configure**\. A **Configure session settings** dialog box appears\.

1. In the **Configure session settings** dialog box, choose the maximum session duration in minutes, hours, and days for your users by selecting the drop down arrow\. Choose a the length for the session, and then choose **Save**\. You return to the **Settings** page\.
# Configure AWS access portal session duration<a name="configure-user-session"></a>

Use the following procedure to configure the AWS access portal session duration for all your users\.

If you have an external identity provider \(IdP\) connected to IAM Identity Center, the AWS access portal session duration will be the lesser of the session duration you set in your IdP or the session duration you set here\. For example, if your IdP session duration is 24 hours and you set an 18 hour session duration in IAM Identity Center, the users must re\-authenticate in the AWS access portal after 18 hours\. If you set a 72 hour session duration here and your IdP has a session duration of 18 hours, your users must re\-authenticate after 18 hours\.

The access portal session duration also applies to CLI sessions\. If you refresh your permission set just before the IAM Identity Center session was set to expire and the session duration is set to 20 hours while permission set duration is set to 12 hours, the CLI session runs for the maximum of 20 hours plus 12 hours for a total of 32 hours\. You must update your AWS CLI and SDKs to the minimum supported version to enable IAM Identity Center session management for AWS CLI and SDKs\. To learn the minimum supported version for each SDK, see [Minimum supported versions for CLI and SDKs needed to configure IAM Identity Center session duration](#min-supported-sdks-session-duration)\. For more information about the IAM Identity Center CLI, see [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/reference/identitystore/index.html#cli-aws-identitystore)\. For more information on how to install or update the latest CLI version, see [Installing or updating the latest version of the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)\.

**To configure an AWS access portal session duration**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Authentication** tab\.

1. Under **Authentication**, next to **Session settings**, choose **Configure**\. A **Configure session settings** dialog box appears\.

1. In the **Configure session settings** dialog box, choose the maximum session duration in minutes, hours, and days for your users by selecting the drop down arrow\. Choose a the length for the session, and then choose **Save**\. You return to the **Settings** page\.

## Minimum supported versions for CLI and SDKs needed to configure IAM Identity Center session duration<a name="min-supported-sdks-session-duration"></a>

See the following table for the minimum supported version for the AWS CLI and SDKs that you can use to enable IAM Identity Center session management\.


****  

| SDK | Minimum version | 
| --- | --- | 
| Python | 1\.26\.10 | 
| PHP | 3\.245\.0 | 
| Ruby | aws\-sdk\-core 3\.167\.0 | 
| CLI V1 | 1\.27\.10 | 
| CLI V2 | 2\.9\.0 | 
| Java V2 | AWS SDK for Java v2 \(2\.18\.13\) | 
| Go V2 | Whole SDK: release\-2022\-11\-11 and specific Go modules: credentials/v1\.13\.0, config/v1\.18\.0 | 
| JS V2 | 2\.1253\.0 | 
| JS V3 | v3\.210\.0 | 
| C\+\+ | 1\.9\.372 | 
| \.NET | v3\.7\.400\.0 | 
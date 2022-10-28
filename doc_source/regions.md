# AWS IAM Identity Center \(successor to AWS Single Sign\-On\) Region availability<a name="regions"></a>

IAM Identity Center is available in several commonly used AWS Regions\. This availability makes it easier for you to configure user access to multiple AWS accounts and business applications\. When your users sign in to the AWS access portal, they can select the AWS account to which they have permissions, and then access the AWS Management Console\. For a full list of the Regions that IAM Identity Center supports, see [IAM Identity Center endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/sso.html)\. 

**Note**  
When you create a user or when a user verifies their email while operating in the AWS GovCloud \(US\-East\) Region, AWS GovCloud \(US\-East\) makes cross\-region API calls to send emails to AWS GovCloud \(US\-West\)\. In these cross\-region calls, user attributes include email, directory ID, user ID, user name, first and last name, and account in AWS Organizations\.

## IAM Identity Center Region data<a name="region-data"></a>

When you first enable IAM Identity Center, all the data that you configure in IAM Identity Center is stored in the Region where you configured it\. This data includes directory configurations, permission sets, application instances, and user assignments to AWS account applications\. If you are using the IAM Identity Center identity store, all users and groups that you create in IAM Identity Center are also stored in the same Region\. We recommend that you install IAM Identity Center in a Region that you intend to keep available for users, not a Region that you might need to disable\.

AWS Organizations supports only one AWS Region at a time\. To enable IAM Identity Center in a different Region, you must first delete your current IAM Identity Center configuration\. Switching to a different Region also changes the URL for the AWS access portal, and you must reconfigure all permission sets and assignments\.

### Managing IAM Identity Center in Regions that must be manually enabled<a name="menually-enabled-regions"></a>

Most AWS Regions are enabled for operations in all AWS services by default\. Those Regions are automatically activated for use with IAM Identity Center\. Some Regions, such as the Europe \(Milan\) Region, must be manually enabled\. When you enable IAM Identity Center for a management account in a manually enabled Region, the following IAM Identity Center metadata for any member accounts is stored in the Region\.
+ Account ID
+ Account name
+ Account email
+ Amazon Resource Names \(ARNs\) of the IAM roles that IAM Identity Center creates in the member account

If you disable a Region in which IAM Identity Center is installed, IAM Identity Center is also disabled\. After IAM Identity Center is disabled in a Region, users in that Region won’t have single sign\-on access to AWS accounts and applications\. AWS retains the data in your IAM Identity Center configuration for at least 10 days\. If you re\-enable IAM Identity Center within this time frame, your IAM Identity Center configuration data will still be available in the Region\.

To re\-enable IAM Identity Center in Regions that must be manually enabled, you must re\-enable the Region\. Because IAM Identity Center must reprocess all paused events again, re\-enabling IAM Identity Center might take some time\.

**Note**  
IAM Identity Center can manage access only to the AWS accounts that are enabled for use in a Region\. To manage access across all accounts in your organization, enable IAM Identity Center in the management account in a Region that is automatically activated for use with IAM Identity Center\.

For more information about enabling and disabling AWS Regions, see [Managing AWS Regions](https://docs.aws.amazon.com/general/latest/gr/rande-manage.html) in the *AWS General Reference*\.

### Delete your IAM Identity Center configuration<a name="delete-config"></a>

When an IAM Identity Center configuration is deleted, all the data in that configuration is deleted and can't be recovered\. The following table describes what data is deleted based on the directory type that is currently configured in IAM Identity Center\.


| What data gets deleted |  Connected directory \(AWS Managed Microsoft AD or AD Connector\)  | IAM Identity Center identity store | 
| --- | --- | --- | 
|  All permission sets you have configured for AWS accounts  | X | X | 
|  All applications you have configured in IAM Identity Center  | X | X | 
| All user assignments you have configured for AWS accounts and applications | X | X | 
| All users and groups in the directory or store | N/A | X | 

Use the following procedure when you need to delete your current IAM Identity Center configuration\.

**To delete your IAM Identity Center configuration**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. In the left navigation pane, choose **Settings**\.

1. On the **Settings** page, choose **Delete**\.

1. In the **Delete IAM Identity Center configuration** dialog, select each of the check boxes to acknowledge you understand that your data that will be deleted\. Type **DELETE** in the text box, and then choose **Confirm**\.
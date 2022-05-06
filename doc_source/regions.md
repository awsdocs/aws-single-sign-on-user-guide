# AWS SSO Region availability<a name="regions"></a>

AWS SSO is available in several commonly used AWS Regions\. This availability makes it easier for you to configure user access to multiple AWS accounts and business applications\. When your users sign in to the user portal, they can select the AWS account that they have permission to\. Then they can access the AWS Management Console\. For a full list of the Regions that AWS SSO supports, see [AWS Single Sign\-On endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/sso.html)\. 

**Note**  
When you create a user or when a user verifies their email while operating in the AWS GovCloud \(US\-East\) region, AWS GovCloud \(US\-East\) makes cross\-region API calls to send emails to AWS GovCloud \(US\-West\)\. In these cross\-region calls, user attributes include email, directory ID, user ID, user name, first and last name, and AWS Organization account\.

## AWS SSO Region data<a name="region-data"></a>

When you first enable AWS SSO, all the data that you configure in AWS SSO is stored in the Region where you configured it\. This data includes directory configurations, permission sets, application instances, and user assignments to AWS account applications\. If you are using the AWS SSO identity store, all users and groups that you create in AWS SSO are also stored in the same Region\. 

AWS Organizations only supports one AWS SSO Region at a time\. If you want to make AWS SSO available in a different Region, you must first delete your current AWS SSO configuration\. Switching to a different Region also changes the URL for the user portal\. 

## Delete your AWS SSO configuration<a name="delete-config"></a>

When an AWS SSO configuration is deleted, all the data in that configuration is deleted and cannot be recovered\. The following table describes what data is deleted based on the directory type that you have currently configured in AWS SSO\.


| What data gets deleted |  Connected directory \(AWS Managed Microsoft AD or AD Connector\)  | AWS SSO identity store | 
| --- | --- | --- | 
|  All permission sets you have configured for AWS accounts  | X | X | 
|  All applications you have configured in AWS SSO  | X | X | 
| All user assignments you have configured for AWS accounts and applications | X | X | 
| All users and groups in the directory or store | N/A | X | 

Use the following procedure when you need to delete your current AWS SSO configuration\.

**To delete your AWS SSO configuration**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. In the left navigation pane, choose **Settings**\.

1. On the **Settings** page, choose **Delete**\.

1. In the **Delete AWS SSO configuration** dialog, select each of the check boxes to acknowledge you understand that your data that will be deleted\. Type **DELETE** in the text box, and then choose **Confirm**\.
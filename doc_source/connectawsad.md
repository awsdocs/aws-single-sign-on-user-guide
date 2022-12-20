# Connect a directory in AWS Managed Microsoft AD to IAM Identity Center<a name="connectawsad"></a>

Use the following procedure to connect a directory in AWS Managed Microsoft AD that is managed by AWS Directory Service to IAM Identity Center\. 

**To connect AWS Managed Microsoft AD to IAM Identity Center**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the IAM Identity Center console is using one of the Regions where your AWS Managed Microsoft AD directory is located before you move to the next step\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, and then choose **Actions > Change identity source**\.

1. Under **Choose identity source**, select **Active Directory**, and then choose **Next**\.

1. Under **Connect active directory**, choose a directory in AWS Managed Microsoft AD from the list, and then choose **Next**\.

1. Under **Confirm change**, review the information and when ready type **ACCEPT**, and then choose **Change identity source**\.
**Important**  
To specify a user in Active Directory as an administrative user in IAM Identity Center, you must first synchronize the user to whom you want to grant administrative permissions from Active Directory into IAM Identity Center\. To do so, follow the steps in [Synchronize an administrative user into IAM Identity Center](get-started-connect-id-source-ad-idp-specify-user.md#sync-admin-user-from-ad)\.
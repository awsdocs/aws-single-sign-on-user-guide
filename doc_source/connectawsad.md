# Connect IAM Identity Center to an AWS Managed Microsoft AD directory<a name="connectawsad"></a>

Use the following procedure to connect an AWS Managed Microsoft AD directory that is managed by AWS Directory Service to IAM Identity Center\. 

**To connect IAM Identity Center to AWS Managed Microsoft AD**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the IAM Identity Center console is using one of the Regions where your AWS Managed Microsoft AD directory is located before you move to the next step\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, and then choose **Actions > Change identity source**\.

1. Under **Choose identity source**, select **Active Directory**, and then choose **Next**\.

1. Under **Connect active directory**, choose an existing AWS Managed Microsoft AD directory from the list, and then choose **Next**\.

1. Under **Confirm change**, review the information and when ready type **ACCEPT**, and then choose **Change identity source**\.
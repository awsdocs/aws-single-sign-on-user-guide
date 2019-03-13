# Connect AWS SSO to an AWS Managed Microsoft AD Directory<a name="connectawsad"></a>

Use the following procedure to connect an AWS Managed Microsoft AD directory that is managed by AWS Directory Service to AWS SSO\. 

**To connect AWS SSO to AWS Managed Microsoft AD**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the AWS SSO console is using one of the regions where your AWS Managed Microsoft AD directory is located before you move to the next step\.

1. From the **Dashboard**, choose **Manage your directory**

1. On the **Directory** page, do the following:

   1. Under **Available directories**, select the AWS Managed Microsoft AD directory you want AWS SSO to connect to\.

   1. Under **User portal URL**, type the prefix to use for the user portal sign\-in URL\.

1. Choose **Connect directory**\.
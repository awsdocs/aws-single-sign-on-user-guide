# Identity Center enabled applications<a name="awsapps"></a>

With [Identity Center enabled applications](app-enablement.md), AWS enterprise applications such as Amazon SageMaker or AWS IoT SiteWise, can exist in a child account in your organization but still use your IAM Identity Center identities\. This provides your application end users with an easy sign\-in experience and allows for delegation of administrator of your applications to operators in a child account\. 

## Constraining Identity Center enabled application use in AWS accounts<a name="awsapps-constrain"></a>

If you want to constrain which of your AWS Organizations accounts that an Identity Center enabled application can be used, you can do so using service control policies \(SCPs\)\. You can use SCPs to block access to the IAM Identity Center user and group information and to prevent the application from being started except in designated accounts\.

## Add and configure an Identity Center enabled application<a name="awsapps-add-config-app"></a>

To use Identity Center enabled applications, you must first enable IAM Identity Center to allow them access\. For more information, see [Identity Center enabled applications](app-enablement.md)\.

After they are enabled, Identity Center enabled applications can access user and group information directly from IAM Identity Center\. As a result, you won’t have to manage access in both IAM Identity Center and then again inside the application\. Instead, IAM Identity Center delegates application access to the application administrator\. To add users to Identity Center enabled applications, use the console of the application where you created the application\.

**To add and configure your application**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. Choose **Add application**\.

1. Under **Applications**, search for an application, and select the application from the list\. Choose **Next**\.

1. Under **Configure application**, the **Display name** and **Description** pre\-populates with the application you chose\. You can edit these\. Under **IAM Identity Center metadata**, download or copy any certificate you might need\. Under **Application properties**, optionally fill out the fields\. Under **Application metadata**, fill out all the fields\. Then, choose **Submit**\. You're taken to the details page of the application that you just added\.

## Remove an Identity Center enabled application<a name="awsapps-remove"></a>

To remove an Identity Center enabled application, you can remove the application from the IAM Identity Center console\. This action is irreversible and you might not be able to recover data from the application\.

**Warning**  
Removing an application deletes all user permissions to this application, disconnects the application from IAM Identity Center, and renders the application inaccessible\.

**To remove an AWS application**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. On the **Applications** page, under **Configured applications**, choose the application that you want to remove\.

1. With the application selected, choose **Actions** and in the dropdown, choose **Remove**\.

1. A **Remove application** dialog box appears\. Follow the prompt to type and confirm the application that you want to remove\. Choose **Remove application**\.
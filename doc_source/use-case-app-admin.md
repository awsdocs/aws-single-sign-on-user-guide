# Enable single sign\-on access to your AWS applications \(Application admin role\)<a name="use-case-app-admin"></a>

This use case provides guidance for application administrators who manage [Identity Center enabled applications](awsapps.md) such as Amazon SageMaker or AWS IoT SiteWise, and need to provide single sign\-on access to their end users\. 

Before you get started, consider the following questions:
+ Should you create a test or production environment in your own separate AWS organization?
+ Is IAM Identity Center already enabled in your AWS organization? Do you have permissions to enable IAM Identity Center in the management account of AWS Organizations?

Depending on your specific business needs, review the guidance below\.

## Configure my AWS application in a standalone AWS account<a name="testorg"></a>

If you need to provide single sign\-on access to an AWS application and know that your IT department does not yet use IAM Identity Center, you may need to create a standalone AWS account so that you can get started\. By default, when you create your own AWS account, you'll have the necessary permissions, such as Root user, to create and manage your own AWS organization\. This permission is required to enable IAM Identity Center\. For more information about the permissions necessary to enable IAM Identity Center, see [Identity and access management for IAM Identity Center](iam-auth-access.md)\.

If they are not already enabled, IAM Identity Center and AWS Organizations can be enabled automatically during the process of setting up some AWS applications \(for example Amazon Managed Grafana does this\)\. If your AWS application does not provide the option to enable them, you’ll need to first setup AWS Organizations and IAM Identity Center before you can provide single sign\-on access to your application\. 

## IAM Identity Center is currently not configured in my organization<a name="existingorgwithsso"></a>

In your role as an application admin, you might not be able to enable IAM Identity Center as it requires specific permissions in the AWS Organizations management account\. In this case, you will need to coordinate with your IT or cloud administrators to get IAM Identity Center enabled in the Organizations management account\.

If you do have sufficient permissions to enable IAM Identity Center within your organization, do so first, then proceed with the application setup\. For more information, see [Getting started](getting-started.md)\.

## IAM Identity Center is currently configured in my organization<a name="existingorgwithnosso"></a>

In this scenario, you can continue to deploy your AWS application without any further steps or requirements\. 

**Note**  
If your organization enabled IAM Identity Center in the management account before November 25th, 2019, you must also enable Identity Center enabled applications in the management account and optionally in the member accounts\. If you enable them in the management account only, you can enable them in member accounts later\. To enable these applications, choose **Enable access** in the IAM Identity Center console's **Settings** page in the Identity Center enabled applications section\. For more information, see [Identity Center enabled applications](app-enablement.md)\.
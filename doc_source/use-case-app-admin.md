# Enable SSO access to your AWS applications \(Application admin role\)<a name="use-case-app-admin"></a>

This use case provides guidance for application administrators who manage [AWS SSO\-integrated applications](awsapps.md) such as Amazon SageMaker or AWS IoT SiteWise, and need to provide SSO access to their end users\. 

Before you get started, consider the following questions:
+ Should you create a test or production environment in your own separate AWS organization?
+ Is AWS SSO already enabled in your AWS organization? Do you have permissions to enable AWS SSO in the management account of AWS Organizations?

Depending on your specific business needs, review the guidance below\.

## Configure my AWS application in a standalone AWS account<a name="testorg"></a>

If you need to provide SSO access to an AWS application and know that your IT department does not yet use AWS SSO, you may need to create a standalone AWS account so that you can get started\. By default, when you create your own AWS account, you'll have the necessary permissions, such as Root user, to create and manage your own AWS organization\. This permission is required to enable AWS SSO\. For more information about the permissions necessary to enable AWS SSO, see [Identity and access management for AWS SSO](iam-auth-access.md)\.

If they are not already enabled, AWS SSO and AWS Organizations can be enabled automatically during the process of setting up some AWS applications \(for example Amazon Managed Service for Grafana does this\)\. If your AWS application does not provide the option to enable them, you’ll need to first setup AWS Organizations and AWS SSO before you can provide SSO access to your application\. 

## AWS SSO is currently not configured in my organization<a name="existingorgwithsso"></a>

In your role as an application admin, you may not be able to enable AWS SSO as it requires specific permissions in the AWS Organizations management account\. In this case, you will need to coordinate with your IT or cloud administrators to get AWS SSO enabled in the Organizations management account\.

If you do have sufficient permissions to enable AWS SSO within your AWS organization, do so first, then proceed with the application setup\. For more information, see [Enable AWS SSO](step1.md)\.

## AWS SSO is currently configured in my organization<a name="existingorgwithnosso"></a>

In this scenario, you can continue to deploy your AWS application without any further steps or requirements\. 

**Note**  
If your organization enabled AWS SSO in the management account before November 25th, 2019, you must also enable AWS SSO\-integrated applications in the management account and optionally in the member accounts\. If you enable them in the management account only, you can enable them in member accounts later\. To enable these applications, choose **Enable access** in the AWS SSO console's **Settings** page in the AWS SSO\-integrated applications section\. For more information, see [AWS SSO\-integrated application enablement](app-enablement.md)\.
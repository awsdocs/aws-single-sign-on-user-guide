# AWS SSO\-Integrated Applications<a name="awsapps"></a>

With [AWS SSO\-Integrated Application Enablement](app-enablement.md), AWS enterprise applications can exist in a child account in your organization but still use your AWS SSO identities\. This provides your application end users with an easy sign\-in experience and allows for delegation of administrator of your applications to operators in a child account\. 

## Constraining AWS SSO\-Integrated Application Use in AWS Accounts<a name="awsapps-constrain"></a>

If you want to constrain which of your AWS Organizations accounts that an integrated application can be used, you can do so using service control policies \(SCPs\)\. You can use SCPs to block access to the AWS SSO user and group information and to prevent the application from being started except in designated accounts\.

## Add and Configure an AWS SSO\-Integrated Application<a name="awsapps-add-config-app"></a>

To use AWS SSO\-integrated applications, you must first enable AWS SSO to allow them access\. For more information, see [AWS SSO\-Integrated Application Enablement](app-enablement.md)\.

After they are enabled, integrated applications can access user and group information directly from AWS SSO\. As a result, you won’t have to manage access in both AWS SSO and then again inside the application\. Instead, AWS SSO delegates application access to the application administrator\. To add users to integrated applications, use the console of the application where you created the application\.

## Disable or Enable an AWS SSO\-Integrated Application<a name="awsapps-disable-enable"></a>

If you only want to stop or restart user authentications to your application, use the following procedure to either disable or enable your application\.

**To disable or enable your application**

1. In the AWS SSO console, choose **Applications** in the left navigation pane\.

1. Select the application in the list\.

1. Choose **Actions**, and then choose either **Disable** or **Enable**\.

## Remove an AWS SSO\-Integrated Application<a name="awsapps-remove"></a>

To remove an integrated application, visit the AWS Management Console where you manage your application\. By removing the app this way, the application can gracefully remove resources that you might otherwise pay for\. For emergency purposes only, you can force\-remove an application from the AWS SSO console\. AWS strongly recommends that you avoid this as such an action is irreversible and you might not be able to recover data from the application\.

Before you force\-remove, consider the following options:
+ You can stop user authentications to this application without removing it by using the **Disable** option instead\. For more information, see [Disable or Enable an AWS SSO\-Integrated Application](#awsapps-disable-enable)\.
+ If you want to disconnect the application from AWS SSO permanently, use the AWS Management Console where you created the application and remove it there instead\. This helps to avoid unnecessary application\-related charges that may otherwise appear if you continue with force\-remove\. This process also removes the application from AWS SSO\. 

**Warning**  
Force\-remove should only be used as a last resort\. This operation deletes all user permissions to this application, disconnects the application from AWS SSO, and renders the application inaccessible\.

**To force\-remove an AWS application**

1. In the AWS SSO console, choose **Applications** in the left navigation pane\.

1. Choose the application you want to remove in the list\.

1. On the application **Details** page, under **Remove Application**, choose **force\-remove**\.

1. On the **Force\-remove application** page, review the warning message\. If you agree, enter **remove**, and then choose **Force\-remove**\.
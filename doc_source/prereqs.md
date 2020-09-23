# AWS SSO Prerequisites<a name="prereqs"></a>

Before you can set up AWS SSO, you must:
+ Have first set up the AWS Organizations service and have **All features** set to enabled\. For more information about this setting, see [Enabling All Features in Your Organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org_support-all-features.html) in the *AWS Organizations User Guide*\.
+ Sign in with the AWS Organizations master account credentials before you begin setting up AWS SSO\. These credentials are required to enable AWS SSO\. For more information, see [Creating and Managing an AWS Organization](http://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org.html) in the *AWS Organizations User Guide*\. You cannot set up AWS SSO while signed in with credentials from an Organization’s member account\.
+ Have chosen an identity source to determine which pool of users has SSO access to the user portal\. If you choose to use the default AWS SSO identity source for your user store, no prerequisite tasks are required\. The AWS SSO store is created by default once you enable AWS SSO and is immediately ready for use\. There is no cost for using this store\. Alternatively, you can choose to [Connect to Your External Identity Provider](manage-your-identity-source-idp.md) using Azure Active Directory\. If you choose to connect to an existing Active Directory for your user store, you must have the following:
  + An existing AD Connector or AWS Managed Microsoft AD directory set up in AWS Directory Service, and it must reside within your organization's master account\. You can connect only one AWS Managed Microsoft AD directory at a time\. However, you can change it to a different AWS Managed Microsoft AD directory or change it back to an AWS SSO store at any time\. For more information, see [Create a AWS Managed Microsoft AD Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/create_directory.html) in the *AWS Directory Service Administration Guide*\.
  + You must set up AWS SSO in the Region where your AWS Managed Microsoft AD directory is set up\. AWS SSO stores the assignment data in the same Region as the directory\. To administer AWS SSO, you should switch to the Region where you have setup AWS SSO\. Also, note that AWS SSO’s user portal uses the same [access URL](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/access_url.html) as your connected directory\.
+ If you currently filter access to specific Amazon Web Service \(AWS\) domains or URL endpoints using a web content filtering solution such as next\-generation firewalls \(NGFW\) or secure web gateways \(SWG\), you must add the following domains and/or URL endpoints to you web\-content filtering solution allow\-lists in order for AWS SSO to work properly:

  **Specific DNS domains**
  + \*\.awsapps\.com \(http://awsapps\.com/\)
  + \*\.signin\.aws

  **Specific URL End\-points**
  + https://\[yourdirectory\]\.awsapps\.com/start
  + https://\[yourdirectory\]\.awsapps\.com/login
  + https://\[yourregion\]\.signin\.aws/platform/login

We highly recommend that before you enable AWS SSO that you first check to see if your AWS account is approaching the quota limit for IAM roles\. For more information, see [IAM Object Quotas](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_iam-quotas.html#reference_iam-quotas-entities)\. If you are nearing the quota limit, you should consider increasing the quota, otherwise you may have issues with AWS SSO as you provision permission sets to accounts that have exceeded the IAM role limit\.
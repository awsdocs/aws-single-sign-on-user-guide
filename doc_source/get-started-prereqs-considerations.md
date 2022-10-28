# Prerequisites and considerations<a name="get-started-prereqs-considerations"></a>

The following topics provide information about prerequisites and other considerations for setting up IAM Identity Center\.

**Topics**
+ [Are you new to AWS?](#get-started-newuser)
+ [Prerequisites and considerations for specific environments](#additional-prerequisites-considerations)

## Are you new to AWS?<a name="get-started-newuser"></a>

If you don't have an AWS account, [sign up for one](https://docs.aws.amazon.com/accounts/latest/reference/welcome-first-time-user.html#getting-started)\. After you create an AWS account, proceed to [Step 1: Enable IAM Identity Center](get-started-enable-identity-center.md)\. 

## Prerequisites and considerations for specific environments<a name="additional-prerequisites-considerations"></a>

The following topics provide guidance for setting up IAM Identity Center for specific environments\. Review the guidance that applies to your environment before you proceed to [Step 1: Enable IAM Identity Center](get-started-enable-identity-center.md)\.

**Topics**
+ [Active Directory or an external IdP](#prereqs-active-directory-idp-identity-source)
+ [AWS Organizations](#prereqs-organizations)
+ [IAM roles](#prereqs-iam-roles)
+ [Next\-generation firewalls and secure web gateways](#prereqs-next-generation-firewalls-secure-web-gateways)

### Active Directory or an external IdP<a name="prereqs-active-directory-idp-identity-source"></a>

If you're already managing users and groups in Active Directory or an external IdP, we recommend that you consider connecting this identity source when you enable IAM Identity Center and choose your identity source\. Doing this before you create any users and groups in the default Identity Center directory will help you avoid the additional configuration that is required if you change your identity source later\. 

If you want to use Active Directory as your identity source, your configuration must meet the following prerequisites:
+ You must have an existing AD Connector or AWS Managed Microsoft AD directory set up in AWS Directory Service, and it must reside within your AWS Organizations management account\. You can connect only one AWS Managed Microsoft AD directory at a time\. For more information, see:
  + [Connect IAM Identity Center to an AWS Managed Microsoft AD directory](connectawsad.md)
  + [Connect IAM Identity Center to a self\-managed directory in Active Directory](connectonpremad.md)
+ If you're using AWS Managed Microsoft AD, you must enable IAM Identity Center in the same AWS Region where your AWS Managed Microsoft AD directory is set up\. IAM Identity Center stores the assignment data in the same Region as the directory\. To administer IAM Identity Center, you might need to switch to the Region where IAM Identity Center is configured\. Also, note that the AWS access portal uses the same access URL as your directory\.

### AWS Organizations<a name="prereqs-organizations"></a>

Your AWS account must be managed by AWS Organizations\. If you haven't set up an organization, you don't have to\. When you enable IAM Identity Center, you will choose whether to have AWS create an organization for you\. 

If you've already set up AWS Organizations, make sure that all features are enabled\. For more information, see [Enabling All Features in Your Organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org_support-all-features.html) in the *AWS Organizations User Guide*\.

To enable IAM Identity Center, you must sign in to the AWS Management Console by using the credentials of your AWS Organizations management account\. You can't enable IAM Identity Center while signed in with credentials from an AWS Organizations member account\. For more information, see [Creating and Managing an AWS Organization](http://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org.html) in the *AWS Organizations User Guide*\.

### IAM roles<a name="prereqs-iam-roles"></a>

If you've already configured IAM roles in your AWS account, we recommend that you check whether your account is approaching the quota for IAM roles\. For more information, see [IAM object quotas](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_iam-quotas.html#reference_iam-quotas-entities)\. 

If you're nearing the quota, consider requesting a quota increase\. Otherwise, you might experience problems with IAM Identity Center when you provision permission sets to accounts that have exceeded the IAM role quota\. For information about how to request a quota increase, see [Requesting a Quota Increase](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html) in the *Service Quotas User Guide*\.

### Next\-generation firewalls and secure web gateways<a name="prereqs-next-generation-firewalls-secure-web-gateways"></a>

If you filter access to specific AWS domains or URL endpoints by using a web content filtering solution such as NGFWs or SWGs, you must add the following domains or URL endpoints to your web\-content filtering solution allow\-lists\. Doing so enables IAM Identity Center to function correctly\.

**Specific DNS domains**
+ \*\.awsapps\.com \(http://awsapps\.com/\)
+ \*\.signin\.aws

**Specific URL endpoints**
+ https://*\[yourdirectory\]*\.awsapps\.com/start
+ https://*\[yourdirectory\]*\.awsapps\.com/login
+ https://*\[yourregion\]*\.signin\.aws/platform/login
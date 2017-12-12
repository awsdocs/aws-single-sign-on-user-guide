# AWS SSO Prerequisites<a name="prereqs"></a>

Before you can set up AWS SSO, you must meet the following requirements:

+ You must have first set up the AWS Organizations service and have **All features** set to enabled\. You must also have access to the AWS Organizations master account credentials\. These credentials are required to enable AWS SSO\. For more information, see [Creating and Managing an AWS Organizations](http://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org.html) in the *AWS Organizations User Guide*\.

+ You must have an existing Microsoft Active Directory \(AD\) set up in AWS Directory Service that you can connect to AWS SSO\. This AWS Microsoft AD directory determines which pool of users has SSO access to the user portal\. You can connect only one AWS Microsoft AD directory at a time\. However, you can change it to a different AWS Microsoft AD directory at any time\. For more information, see [Create a Microsoft AD Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/create_directory.html) in the *AWS Directory Service Administration Guide*\.

+ Your connected directory must be in the US East \(N\. Virginia\) \(us\-east\-1\) Region where AWS SSO is also available\. AWS SSO stores the assignment data in the same region as the directory\. To administer AWS SSO, you must be in the us\-east\-1 region\. Also, note that AWS SSO’s user portal uses the same [access URL](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/access_url.html) as your connected directory\.
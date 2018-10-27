# AWS SSO Prerequisites<a name="prereqs"></a>

Before you can set up AWS SSO, you must meet the following requirements:
+ You must have first set up the AWS Organizations service and have **All features** set to enabled\. 

   
+ You must sign in with the AWS Organizations master account credentials before you begin setting up AWS SSO\. These credentials are required to enable AWS SSO\. For more information, see [Creating and Managing an AWS Organization](http://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org.html) in the *AWS Organizations User Guide*\. You cannot set up AWS SSO while signed in with credentials from an Organization’s member account\.

   
+ You must choose a directory store to determine which pool of users has SSO access to the user portal\. 

   
  + If you choose to use the default AWS SSO directory for your user store, no prerequisite tasks are required\. The AWS SSO directory is created by default once you enable AWS SSO and is immediately ready for use\. There is no cost for using this directory type\.

     
  + Connecting to an existing Active Directory for your user store requires the following:

     
    + You must have an existing AWS Managed Microsoft AD directory set up in AWS Directory Service, and it must reside within your organization's master account\. You can connect only one AWS Managed Microsoft AD directory at a time\. However, you can change it to a different AWS Managed Microsoft AD directory or change it back to an AWS SSO directory at any time\. For more information, see [Create a AWS Managed Microsoft AD Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/create_directory.html) in the *AWS Directory Service Administration Guide*\.

       
    + Your AWS Managed Microsoft AD directory must be in the US East \(N\. Virginia\) \(us\-east\-1\) Region where AWS SSO is also available\. AWS SSO stores the assignment data in the same region as the directory\. To administer AWS SSO, you must be in the us\-east\-1 region\. Also, note that AWS SSO’s user portal uses the same [access URL](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/access_url.html) as your connected directory\.
# Connect AWS SSO to an On\-Premises Active Directory<a name="connectonpremad"></a>

Users in your on\-premises Active Directory can also have SSO access to AWS accounts and cloud applications in the AWS SSO user portal\. To do that, AWS Directory Service has the following two options available:
+ **Create a two\-way trust relationship** – When two\-way trust relationships are created between AWS Managed Microsoft AD and an on\-premises Active Directory, on\-premises users can sign in with their corporate credentials to various AWS services and business applications\. One\-way trusts do not work with AWS SSO\. For more information about setting up a two\-way trust, see [When to Create a Trust Relationship](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/setup_trust.html) in the *AWS Directory Service Administration Guide*\.
+ **Create an AD Connector** – AD Connector is a directory gateway that can redirect directory requests to your on\-premises Active Directory without caching any information in the cloud\. For more information, see [Connect to a Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_ad_connector.html) in the *AWS Directory Service Administration Guide*\.
**Note**  
If you are connecting AWS SSO to an AD Connector directory, any future user password resets must be done from within Active Directory\. This means that users will not be able to reset their passwords from the user portal\.
**Note**  
AWS SSO does not work with SAMBA4\-based Simple AD directories\.
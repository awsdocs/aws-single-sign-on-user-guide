# Connect AWS SSO to a Self\-Managed Active Directory<a name="connectonpremad"></a>

Users in your self\-managed Active Directory \(AD\) can also have SSO access to AWS accounts and cloud applications in the AWS SSO user portal\. To do that, AWS Directory Service has the following two options available:
+ **Create a two\-way trust relationship** – When two\-way trust relationships are created between AWS Managed Microsoft AD and a self\-managed AD, users in your self\-managed AD can sign in with their corporate credentials to various AWS services and business applications\. One\-way trusts do not work with AWS SSO\. For more information about setting up a two\-way trust, see [When to Create a Trust Relationship](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/setup_trust.html) in the *AWS Directory Service Administration Guide*\.
+ **Create an AD Connector** – AD Connector is a directory gateway that can redirect directory requests to your self\-managed AD without caching any information in the cloud\. For more information, see [Connect to a Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_ad_connector.html) in the *AWS Directory Service Administration Guide*\.
**Note**  
If you are connecting AWS SSO to an AD Connector directory, any future user password resets must be done from within AD\. This means that users will not be able to reset their passwords from the user portal\.
**Note**  
AWS SSO does not work with SAMBA4\-based Simple AD directories\.
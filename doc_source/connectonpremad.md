# Connect AWS SSO to a self\-managed directory in Active Directory<a name="connectonpremad"></a>

Users in your self\-managed directory in Active Directory \(AD\) can also have SSO access to AWS accounts and cloud applications in the AWS SSO user portal\. To do that, AWS Directory Service has the following two options available:
+ **Create a two\-way trust relationship** – When two\-way trust relationships are created between AWS Managed Microsoft AD and a self\-managed directory in AD, users in your self\-managed directory in AD can sign in with their corporate credentials to various AWS services and business applications\. One\-way trusts do not work with AWS SSO\.

  AWS Single Sign\-On requires a two\-way trust so that it has permissions to read user and group information from your domain to synchronize user and group metadata\. AWS SSO uses this metadata when assigning access to permission sets or applications\. User and group metadata is also used by applications for collaboration, like when you share a dashboard with another user or group\. The trust from AWS Directory Service for Microsoft Active Directory to your domain permits AWS SSO to trust your domain for authentication\. The trust in the opposite direction grants AWS permissions to read user and group metadata\. 

  For more information about setting up a two\-way trust, see [When to Create a Trust Relationship](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/setup_trust.html) in the *AWS Directory Service Administration Guide*\.
+ **Create an AD Connector** – AD Connector is a directory gateway that can redirect directory requests to your self\-managed AD without caching any information in the cloud\. For more information, see [Connect to a Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_ad_connector.html) in the *AWS Directory Service Administration Guide*\.
**Note**  
If you are connecting AWS SSO to an AD Connector directory, any future user password resets must be done from within AD\. This means that users will not be able to reset their passwords from the user portal\.  
If you use AD Connector to connect your Active Directory Domain Service to AWS SSO, AWS SSO only has access to the users and groups of the single domain to which AD Connector attaches\. If you need to support multiple domains or forests, use AWS Directory Service for Microsoft Active Directory\.
**Note**  
AWS SSO does not work with SAMBA4\-based Simple AD directories\.
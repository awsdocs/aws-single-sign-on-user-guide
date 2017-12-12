# Connect AWS SSO to an On\-Premises Active Directory \(Optional\)<a name="connectawsad"></a>

If you want users in your on\-premises Active Directory to also have SSO access to AWS accounts and cloud applications in the AWS SSO user portal, AWS Directory Service has the following two options available:

+ **Create a trust relationship** – Trust relationships created between AWS Microsoft AD and an on\-premises Active Directory enable on\-premises users to sign in with their corporate credentials to various AWS services\. For more information, see [When to Create a Trust Relationship](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/setup_trust.html) in the *AWS Directory Service Administration Guide*\.

+ **Create an AD Connector** – AD Connector is a directory gateway that can redirect directory requests to your on\-premises Active Directory without caching any information in the cloud\. For more information, see [Connect to a Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/connect_directory.html) in the *AWS Directory Service Administration Guide*\.
**Note**  
AWS SSO does not work with SAMBA4\-based Simple AD directories\.
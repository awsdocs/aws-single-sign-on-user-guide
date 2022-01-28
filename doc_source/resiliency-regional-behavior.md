# Resiliency design and regional behavior<a name="resiliency-regional-behavior"></a>

The AWS SSO service is fully managed and uses highly available and durable AWS services, such as Amazon S3 and Amazon EC2\. To ensure availability in the event of an availability zone disruption, AWS SSO operates across multiple availability zones\.

You enable AWS SSO in your AWS Organizations management account\. This is required so that AWS SSO can provision, de\-provision, and update roles across all your AWS accounts\. When you enable AWS SSO, you must select a single AWS Region in which to deploy the service\. This primary Region can be the same or different Region than your AWS Organizations primary Region\. 

**Note**  
AWS SSO controls access to its permission sets and applications from its primary Region only\. We recommend that you consider the risks associated with access control when AWS SSO operates in a single Region\.

Although AWS SSO determines access from the Region in which you enable the service, AWS accounts are global\. This means that after users sign in to AWS SSO, they can operate in any Region when they access AWS accounts through AWS SSO\. Most AWS SSO\-integrated applications such as Amazon SageMaker, however, must be installed in the same Region as AWS SSO for users to authenticate and assign access to these applications\. For information about regional constraints when using an application with AWS SSO, see the documentation for the application\.

You can also use AWS SSO to authenticate and authorize access to SAML\-based applications that are reachable through a public URL, regardless of the platform or cloud on which the application is built\.
# Resiliency design and Regional behavior<a name="resiliency-regional-behavior"></a>

The IAM Identity Center service is fully managed and uses highly available and durable AWS services, such as Amazon S3 and Amazon EC2\. To ensure availability in the event of an availability zone disruption, IAM Identity Center operates across multiple availability zones\.

You enable IAM Identity Center in your AWS Organizations management account\. This is required so that IAM Identity Center can provision, de\-provision, and update roles across all your AWS accounts\. When you enable IAM Identity Center, it is deployed to the AWS Region that is currently selected\. If you want to deploy to a specific AWS Region, change the region selection before enabling IAM Identity Center\. 

**Note**  
IAM Identity Center controls access to its permission sets and applications from its primary Region only\. We recommend that you consider the risks associated with access control when IAM Identity Center operates in a single Region\.

Although IAM Identity Center determines access from the Region in which you enable the service, AWS accounts are global\. This means that after users sign in to IAM Identity Center, they can operate in any Region when they access AWS accounts through IAM Identity Center\. Most Identity Center enabled applications such as Amazon SageMaker, however, must be installed in the same Region as IAM Identity Center for users to authenticate and assign access to these applications\. For information about Regional constraints when using an application with IAM Identity Center, see the documentation for the application\.

You can also use IAM Identity Center to authenticate and authorize access to SAML\-based applications that are reachable through a public URL, regardless of the platform or cloud on which the application is built\.
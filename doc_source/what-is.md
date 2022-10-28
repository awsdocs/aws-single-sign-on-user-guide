# What is IAM Identity Center?<a name="what-is"></a>

AWS IAM Identity Center \(successor to AWS Single Sign\-On\) expands the capabilities of AWS Identity and Access Management \(IAM\) to provide a central place that brings together administration of users and their access to AWS accounts and cloud applications\. Although the service name AWS Single Sign\-On has been retired, the term *single sign\-on* is still used throughout this guide to describe the authentication scheme that allows users to sign in one time to access multiple applications and websites\.

With IAM Identity Center you can manage **sign\-in security for your workforce by creating or connecting your users and groups to AWS in one place\. With *multi\-account permissions* you can assign your *workforce identities* access to AWS accounts\. You can use *application assignments* to assign your users access to software as a service \(SaaS\) applications\. With a single click, IAM Identity Center enabled application admins can assign access to your workforce users, and can also use application assignments to assign your users access to software as a service \(SaaS\) applications\.

## IAM Identity Center features<a name="features"></a>

IAM Identity Center includes the following core features:

**Workforce identities**  
Human users that are members of your organization are also known as workforce identities or *workforce users*\. You can create workforce users and groups in IAM Identity Center, or connect and synchronize to an existing set of users and groups in your own identity source for use across all your AWS accounts and applications\. Supported identity sources include Microsoft Active Directory Domain Services, and external identity providers such as Okta Universal Directory or Microsoft Azure AD\.

**Application assignments for SAML applications**  
With application assignments, you can grant your workforce users in IAM Identity Center single sign\-on access to SAML 2\.0 applications, such as Salesforce and Microsoft 365\. Your users can access these applications in a single place, without the need for you to set up separate federation\.

**Identity Center enabled applications**  
AWS applications and services, such as Amazon Managed Grafana, Amazon Monitron, and Amazon SageMaker Studio Notebooks, discover and connect to IAM Identity Center automatically to receive sign\-in and user directory services\. This provides users with a consistent single sign\-on experience to these applications with no additional configuration of the applications\. Because the applications share a common view of users, groups, and group membership, users also have a consistent experience when sharing application resources with others\.

**Multi\-account permissions**  
With multi\-account permissions you can plan for and centrally implement IAM permissions across multiple AWS accounts at one time without needing to configure each of your accounts manually\. You can create fine\-grained permissions based on common job functions or define custom permissions that meet your security needs\. You can then assign those permissions to workforce users to control their access over specific accounts\.

**AWS access portal**  
The AWS access portal provides your workforce users with one\-click access to all their assigned AWS accounts and cloud applications through a simple web portal\.

## IAM Identity Center rename<a name="renamed"></a>

On July 26, 2022, AWS Single Sign\-On was renamed to AWS IAM Identity Center \(successor to AWS Single Sign\-On\)\. For existing customers, the following table is meant to describe some of the more common term changes that have been updated throughout this guide as a result of the rename\.


| **Legacy term** | **Current term** | 
| --- | --- | 
| AWS SSO user or SSO user | workforce user or user | 
| AWS SSO user portal or user portal | AWS access portal | 
| AWS SSO\-integrated applications | Identity Center enabled applications | 
| AWS SSO directory | Identity Center directory | 
| AWS SSO store or AWS SSO identity store | identity store used by IAM Identity Center | 

The following table describes the applicable user, developer and API reference guide name changes that also took place as a result of this rename\. 


| **Legacy guide** | **Current guide** | 
| --- | --- | 
| AWS Single Sign\-On User Guide | [IAM Identity Center User Guide](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html) | 
| AWS Single Sign\-On SCIM Implementation Developer Guide | [IAM Identity Center SCIM Implementation Developer Guide](https://docs.aws.amazon.com/singlesignon/latest/developerguide/what-is-scim.html) | 
| AWS Single Sign\-On API Reference Guide | [IAM Identity Center API Reference](https://docs.aws.amazon.com/singlesignon/latest/APIReference/welcome.html) | 
| AWS Single Sign\-On Identity Store API Reference Guide | [Identity Store API Reference](https://docs.aws.amazon.com/singlesignon/latest/developerguide/what-is-scim.html) | 
| AWS Single Sign\-On OIDC API Reference Guide | [IAM Identity Center OIDC API Reference](https://docs.aws.amazon.com/singlesignon/latest/OIDCAPIReference/Welcome.html) | 
| AWS Single Sign\-On Portal API Reference Guide | [IAM Identity Center Portal API Reference](https://docs.aws.amazon.com/singlesignon/latest/PortalAPIReference/Welcome.html) | 

### Legacy namespaces remain the same<a name="legacy-namespaces"></a>



The `sso` and `identitystore` API namespaces along with the following related namespaces **remain unchanged** for backward compatibility purposes\.


+ CLI commands
  + [https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html)
  + [https://awscli.amazonaws.com/v2/documentation/api/latest/reference/identitystore/index.html](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/identitystore/index.html)
  + [https://awscli.amazonaws.com/v2/documentation/api/latest/reference/sso/index.html](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/sso/index.html)
  + [https://awscli.amazonaws.com/v2/documentation/api/latest/reference/sso-admin/index.html](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/sso-admin/index.html)
  + [https://awscli.amazonaws.com/v2/documentation/api/latest/reference/sso-oidc/index.html](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/sso-oidc/index.html)
+ [Managed policies](https://docs.aws.amazon.com/singlesignon/latest/userguide/security-iam-awsmanpol.html) containing `AWSSSO` and `AWSIdentitySync` prefixes
+ [Service endpoints](https://docs.aws.amazon.com/general/latest/gr/sso.html#sso_region) containing `sso` and `identitystore`
+ [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_SSO.html) resources containing `AWS::SSO` prefixes
+ [Service\-linked role](https://docs.aws.amazon.com/singlesignon/latest/userguide/using-service-linked-roles.html#slr-permissions) containing `AWSServiceRoleForSSO`
+ Console URLs containing `sso` and `singlesignon`
+ Documentation URLs containing `singlesignon`
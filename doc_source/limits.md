# AWS Single Sign\-On Quotas<a name="limits"></a>

The following tables describe quotas within AWS SSO\. 

## Application Quotas<a name="applicationlimits"></a>


| Resource | Default Quota | Can be increased | 
| --- | --- | --- | 
|  File size of service provider SAML certificates \(in PEM format\)  | 2 kb | No | 

## AWS Account Quotas<a name="awsaccountlimits"></a>


| Resource | Default Quota | Can be increased | 
| --- | --- | --- | 
| Maximum number of permission sets in AWS SSO | 500 | Yes | 
| Number of permission sets allowed per AWS account | 50 | Yes | 
|  Number of references to AWS managed policies per permission set  | 10 | Yes | 
| Number of inline policies per permission set | 1 | No | 
| Maximum size of inline policy per permission set | 10,000 bytes | No | 
|  Number of IAM roles in the AWS account that can be repaired at a time \*  | 1 | No | 
|  Number of directories that you can have at a time  | 1 | No | 

\* Permission sets are provisioned in an AWS account as IAM roles\. For more information, see [Permission Sets](permissionsetsconcept.md)\.

## Connected Directory Quotas<a name="connecteddirectorylimits"></a>


| Resource | Default Quota | Can be increased | 
| --- | --- | --- | 
|  Number of unique Active Directory groups that can be assigned \*  | 2500 | Yes | 
|  Number of connected directories that you can have at a time  | 1 | No | 

\* Users within their Active Directory can belong to many directory groups\. However within AWS SSO, they can have up to 2500 of their Active Directory groups assigned for using applications\.

## Additional Quotas<a name="additionallimits"></a>


| Resource | Default Quota | Can be increased | 
| --- | --- | --- | 
|  Total number of AWS accounts or applications that can be configured \*  | 500 | Yes | 
|  Maximum number of unique groups that can be used to evaluate the permissions for a user \*\*  | 500 | No | 

\* Only 500 AWS accounts or applications \(total combined\) are supported\. For example, you might configure 275 accounts and 225 applications, resulting in a total of 500 accounts and applications\.

\*\* Before displaying the user’s available AWS accounts and application icons in the user portal, AWS SSO evaluates the user’s effective permissions by evaluating their group memberships\. Only 500 unique groups can be used to determine a user’s effective permissions\.

## AWS SSO Identity Store Quotas<a name="ssodirectorylimits"></a>


| Resource | Default Quota | 
| --- | --- | 
|  Number of unique groups that can be assigned \*  | 100 | 
|  Number of AWS SSO stores that you can have at a time  | 1 | 
|  Maximum number of users supported in AWS SSO  | 50000 | 
| Maximum number of groups supported in AWS SSO | 10000 | 

\* Users within an AWS SSO store can have up to 100 of their groups assigned for using applications\.
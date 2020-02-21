# Limits in AWS SSO<a name="limits"></a>

The following tables describe limits within AWS SSO\. 

## Application Limits<a name="applicationlimits"></a>


| Resource | Default Limit | 
| --- | --- | 
|  File size of service provider SAML certificates \(in PEM format\)  | 2 kb | 

## AWS Account Limits<a name="awsaccountlimits"></a>


| Resource | Default Limit | 
| --- | --- | 
| Maximum number of permission sets in AWS SSO | 500 | 
| Number of permission sets allowed per AWS account | 50 | 
|  Number of references to AWS managed policies per permission set  | 10 | 
| Number of inline policies per permission set | 1 | 
| Maximum size of inline policy per permission set | 10,000 bytes | 
|  Number of IAM roles in the AWS account that can be repaired at a time \*  | 1 | 
|  Number of directories that you can have at a time  | 1 | 

\* Permission sets are provisioned in an AWS account as IAM roles\. For more information, see [Permission Sets](permissionsetsconcept.md)\.

## Connected Directory Limits<a name="connecteddirectorylimits"></a>


| Resource | Default Limit | 
| --- | --- | 
|  Number of unique Active Directory groups that can be assigned \*  | 1500 | 
|  Number of connected directories that you can have at a time  | 1 | 

\* Users within their Active Directory can belong to many directory groups\. However within AWS SSO, they can have up to 1500 of their Active Directory groups assigned for using applications\.

## AWS SSO Identity Store Limits<a name="ssodirectorylimits"></a>


| Resource | Default Limit | 
| --- | --- | 
|  Number of unique groups that can be assigned \*  | 100 | 
|  Number of AWS SSO stores that you can have at a time  | 1 | 
|  Maximum number of users supported in AWS SSO  | 50000 | 
| Maximum number of groups supported in AWS SSO | 10000 | 

\* Users within an AWS SSO store can have up to 100 of their groups assigned for using applications\.

## Additional Limits<a name="additionallimits"></a>


| Resource | Default Limit | 
| --- | --- | 
|  Total number of AWS accounts or applications that can be configured \*  | 500 | 
|  Maximum number of unique groups that can be used to evaluate the permissions for a user \*\*  | 500 | 

\* Only 500 AWS accounts or applications \(total combined\) are supported\. For example, you might configure 275 accounts and 225 applications, resulting in a total of 500 accounts and applications\.

\*\* Before displaying the user’s available AWS accounts and application icons in the user portal, AWS SSO evaluates the user’s effective permissions by evaluating their group memberships\. Only 500 unique groups can be used to determine a user’s effective permissions\.
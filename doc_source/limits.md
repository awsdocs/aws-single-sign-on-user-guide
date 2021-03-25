# AWS Single Sign\-On quotas<a name="limits"></a>

The following tables describe quotas within AWS SSO\. 

## Application quotas<a name="applicationlimits"></a>


| Resource | Default quota | Can be increased | 
| --- | --- | --- | 
|  File size of service provider SAML certificates \(in PEM format\)  | 2 KB | No | 

## AWS account quotas<a name="awsaccountlimits"></a>


| Resource | Default quota | Can be increased | 
| --- | --- | --- | 
| Number of permission sets allowed in AWS SSO | 500 | Yes | 
| Number of permission sets allowed per AWS account | 50 | Yes | 
| Number of inline policies per permission set | 1 | No | 
| Maximum size of inline policy per permission set | 10,000 bytes | No | 
|  Number of IAM roles in the AWS account that can be repaired at a time  | 1 | No | 

**Note**  
[Permission sets](permissionsetsconcept.md) are provisioned in AWS accounts as IAM roles and therefore follow IAM quotas\. For more information about IAM quotas, see [IAM and STS quotas](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_iam-quotas.html)\. 

## Active Directory quotas<a name="connecteddirectorylimits"></a>


| Resource | Default quota | Can be increased | 
| --- | --- | --- | 
|  Number of unique directory groups that can be assigned \*  | 2500 | Yes | 
|  Number of connected directories that you can have at a time  | 1 | No | 

\* Users can belong to many directory groups, and a directory may contain many groups \(see [AWS SSO identity store quotas](#ssodirectorylimits)\)\. Within AWS SSO, a maximum of 2500 of these groups can be assigned for using accounts and applications\.

## AWS SSO identity store quotas<a name="ssodirectorylimits"></a>


| Resource | Default quota | 
| --- | --- | 
|  Number of unique groups that can be assigned \*  | 100 | 
|  Number of users supported in AWS SSO  | 50000 | 
| Number of groups supported in AWS SSO | 10000 | 

\* Users within an AWS SSO store can have up to 100 of their groups assigned for using applications\.

## Additional quotas<a name="additionallimits"></a>


| Resource | Default quota | Can be increased | 
| --- | --- | --- | 
|  Total number of AWS accounts or applications that can be configured \*  | 500 | Yes | 
|  Number of unique groups that can be used to evaluate the permissions for a user \*\*  | 500 | No | 

\* Only 500 AWS accounts or applications \(total combined\) are supported\. For example, you might configure 275 accounts and 225 applications, resulting in a total of 500 accounts and applications\.

\*\* Before displaying the user’s available AWS accounts and application icons in the user portal, AWS SSO evaluates the user’s effective permissions by evaluating their group memberships\. Only 500 unique groups can be used to determine a user’s effective permissions\.
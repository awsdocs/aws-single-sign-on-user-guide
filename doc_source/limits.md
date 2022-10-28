# AWS IAM Identity Center \(successor to AWS Single Sign\-On\) quotas<a name="limits"></a>

The following tables describe quotas within IAM Identity Center\. To increase a quota, see [Requesting a quota increase](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html)\.

**Note**  
 We recommend using the AWS CLI and APIs if you have more than 50,000 users, 10,000 groups, or 500 permission sets\. For more information about the CLI, see [Integrating AWS CLI with IAM Identity Center](integrating-aws-cli.md)\. For more information about APIs, see [Welcome to the IAM Identity Center API Reference](https://docs.aws.amazon.com/singlesignon/latest/APIReference/welcome.html)\.

## Application quotas<a name="applicationlimits"></a>


| Resource | Default quota | Can be increased | 
| --- | --- | --- | 
|  File size of service provider SAML certificates \(in PEM format\)  | 2 KB | No | 
| File size limit of the IdP certificate uploaded to SSO | 2500 \(UTF\-8\) characters | No | 

## AWS account quotas<a name="awsaccountlimits"></a>


| Resource | Default quota | Can be increased | 
| --- | --- | --- | 
| Number of permission sets allowed in IAM Identity Center | 2000 | Yes | 
| Number of permission sets allowed per AWS account  | 50 | Yes | 
| Number of inline policies per permission set | 1 | No | 
| Number of AWS managed and customer managed policies per permission set | 201 | No | 
| Maximum size of inline policy per permission set | 10,240 bytes | No | 
|  Number of IAM roles \(permission sets\) in the AWS account that can be updated at a time  | 1 | No | 

1AWS Identity and Access Management \(IAM\) sets a quota of 10 managed policies per role\. To take advantage of this quota, request an increase to the IAM quota *Managed policies attached to an IAM role* in the Service Quotas console for each AWS account where you want to deploy the permission set\. 

**Note**  
[Permission sets](permissionsetsconcept.md) are provisioned in AWS accounts as IAM roles, or use existing IAM roles in AWS accounts, and therefore follow IAM quotas\. For more information about quotas that are associated with IAM roles, see [IAM and STS quotas](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_iam-quotas.html)\. 

## Active Directory quotas<a name="connecteddirectorylimits"></a>


| Resource | Default quota | Can be increased | 
| --- | --- | --- | 
|  Number of connected directories that you can have at a time  | 1 | No | 

## IAM Identity Center identity store quotas<a name="ssodirectorylimits"></a>


| Resource | Default quota | Can be increased | 
| --- | --- | --- | 
|  Number of users supported in IAM Identity Center  | 100000 | Yes | 
| Number of groups supported in IAM Identity Center | 100000 | No | 

## IAM Identity Center throttle limits<a name="ssothrottlelimits"></a>


| Resource | Default quota | 
| --- | --- | 
| IAM Identity Center APIs | [IAM Identity Center APIs](https://docs.aws.amazon.com/singlesignon/latest/APIReference/API_Operations.html) have a collective throttle maximum of 20 transactions per second \(TPS\)\. The [CreateAccountAssignment](https://docs.aws.amazon.com/singlesignon/latest/APIReference/API_CreateAccountAssignment.html) has a maximum rate of 10 outstanding async calls\. These quotas cannot be changed\. | 

## Additional quotas<a name="additionallimits"></a>


| Resource | Default quota | Can be increased | 
| --- | --- | --- | 
|  Total number of AWS accounts or applications that can be configured \*  | 3000 | Yes | 

\* Up to 3000 AWS accounts or applications \(total combined\) are supported\. For example, you might configure 2750 accounts and 250 applications, resulting in a total of 3000 accounts and applications\. 
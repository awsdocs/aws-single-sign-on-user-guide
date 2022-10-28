# Connect to a Microsoft AD directory<a name="manage-your-identity-source-ad"></a>

With AWS IAM Identity Center \(successor to AWS Single Sign\-On\), you can connect a self\-managed directory in Active Directory \(AD\) or a AWS Managed Microsoft AD directory by using AWS Directory Service\. This Microsoft AD directory defines the pool of identities that administrators can pull from when using the IAM Identity Center console to assign single sign\-on access\. After connecting your corporate directory to IAM Identity Center, you can then grant your AD users or groups access to AWS accounts, cloud applications, or both\. 

AWS Directory Service helps you to set up and run a standalone AWS Managed Microsoft AD directory hosted in the AWS Cloud\. You can also use AWS Directory Service to connect your AWS resources with an existing self\-managed AD\. To configure AWS Directory Service to work with your self\-managed AD, you must first set up trust relationships to extend authentication to the cloud\.

IAM Identity Center uses the connection provided by AWS Directory Service to perform pass\-through authentication to the source AD instance, leveraging the Kerberos protocol\. When you use AWS Managed Microsoft AD as your identity source, IAM Identity Center can work with users from AWS Managed Microsoft AD or from any domain connected through an AD trust\. If you want to locate your users in four or more domains, users must use the `DOMAIN\user` syntax as their user name when performing sign\-ins to IAM Identity Center\.

**Notes**  
As a prerequisite step, make sure your AD Connector or AWS Managed Microsoft AD directory in AWS Directory Service resides within your AWS Organizations management account\. For more information, see [Active Directory or an external IdP](get-started-prereqs-considerations.md#prereqs-active-directory-idp-identity-source)\.
IAM Identity Center does not support SAMBA 4\-based Simple AD as a connected directory\.

## Provisioning when users come from Active Directory<a name="provision-users-from-ad"></a>

IAM Identity Center uses the connection provided by the AWS Directory Service to synchronize user, group, and membership information from your source directory in Active Directory to the IAM Identity Center identity store\. No password information is synchronized to IAM Identity Center, since user authentication takes place directly from the source directory in Active Directory\. This identity data is used by IAM Identity Center enabled applications to facilitate in\-app lookup, authorization, and collaboration scenarios without passing LDAP activity back to the source directory in Active Directory\.

For more information above provisioning, see [User and group provisioning](users-groups-provisioning.md#user-group-provision)\.

**Topics**
+ [Provisioning when users come from Active Directory](#provision-users-from-ad)
+ [Connect IAM Identity Center to an AWS Managed Microsoft AD directory](connectawsad.md)
+ [Connect IAM Identity Center to a self\-managed directory in Active Directory](connectonpremad.md)
+ [Attribute mappings](attributemappingsconcept.md)
+ [Provision users and groups from Active Directory](provision-users-groups-AD.md)
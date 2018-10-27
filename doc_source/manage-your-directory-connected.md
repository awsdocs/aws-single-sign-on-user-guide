# Connect to Your Microsoft AD Directory<a name="manage-your-directory-connected"></a>

AWS Single Sign\-On enables administrators to connect their on\-premises Active Directory \(AD\) or their AWS Managed Microsoft AD directory using AWS Directory Service\. This Microsoft AD directory defines the pool of identities that administrators can pull from when using the AWS SSO console to assign single sign\-on \(SSO\) access\. After connecting their corporate directory to AWS SSO, administrators can then grant their AD users or groups access to AWS accounts, cloud applications, or both\. 

AWS Directory Service helps you to set up and run a standalone AWS Managed Microsoft AD directory hosted in the AWS Cloud\. You can also use AWS Directory Service to connect your AWS resources with an existing on\-premises Microsoft Active Directory\. To configure AWS Directory Service to work with your on\-premises Active Directory, you must first set up trust relationships to extend authentication from on\-premises to the cloud\.

**Note**  
AWS SSO does not support SAMBA4\-based Simple AD as a connected directory\.

**Topics**
+ [Connect AWS SSO to an AWS Managed Microsoft AD Directory](connectawsad.md)
+ [Connect AWS SSO to an On\-Premises Active Directory](connectonpremad.md)
+ [Attribute Mappings](attributemappingsconcept.md)
# Manage Your Connected Directory<a name="manage-connected-directory"></a>

AWS Single Sign\-On enables administrators to connect their on\-premises Active Directory \(AD\) or their AWS Microsoft AD directory using AWS Directory Service\. This connected directory defines the pool of identities that administrators can pull from when using the AWS SSO console to assign single sign\-on \(SSO\) access\. After connecting their corporate directory to AWS SSO, administrators can then grant their AD users or groups access to AWS accounts, cloud applications, or both\. 

AWS Directory Service makes it easy for you to set up and run a standalone Microsoft AD directory hosted in the AWS Cloud, or to connect your AWS resources with an existing on\-premises Microsoft Active Directory\. To configure AWS Directory Service to work with your on\-premises Active Directory, you first need to set up trust relationships to extend authentication from on\-premises to the cloud\.

**Note**  
AWS SSO does not support SAMBA4\-based Simple AD as a connected directory\.


+ [Connect AWS SSO to an AWS Microsoft AD Directory](connectonpremad.md)
+ [Connect AWS SSO to an On\-Premises Active Directory \(Optional\)](connectawsad.md)
+ [Map Attributes in AWS SSO to Attributes in Your Connected Directory \(Optional\)](mapssoattributestocdattributes.md)
+ [Disconnect a Directory](howtodisconnectdirectory.md)
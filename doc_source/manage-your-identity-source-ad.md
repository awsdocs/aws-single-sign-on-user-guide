# Connect to Your Microsoft AD Directory<a name="manage-your-identity-source-ad"></a>

AWS Single Sign\-On enables administrators to connect their self\-managed Active Directory \(AD\) or their AWS Managed Microsoft AD directory using AWS Directory Service\. This Microsoft AD directory defines the pool of identities that administrators can pull from when using the AWS SSO console to assign single sign\-on \(SSO\) access\. After connecting their corporate directory to AWS SSO, administrators can then grant their AD users or groups access to AWS accounts, cloud applications, or both\. 

AWS Directory Service helps you to set up and run a standalone AWS Managed Microsoft AD directory hosted in the AWS Cloud\. You can also use AWS Directory Service to connect your AWS resources with an existing self\-managed AD\. To configure AWS Directory Service to work with your self\-managed AD, you must first set up trust relationships to extend authentication to the cloud\.

**Note**  
AWS SSO does not support SAMBA4\-based Simple AD as a connected directory\.

## Provisioning When Users Come from Active Directory<a name="provision-users-from-ad"></a>

Because assigning permissions is a low\-frequency activity, AWS SSO has the ability to access user information directly from Active Directory\. AWS SSO connects to your directory through AWS Managed Microsoft AD or AD Connector\. For more information about how to do this, see [Connect AWS SSO to an AWS Managed Microsoft AD Directory](connectawsad.md)\.

AWS SSO requires low\-latency, high performance access to user information in the cloud\. To accommodate this need, AWS SSO provisions user information into AWS SSO automatically each time a user signs in using just\-in\-time \(JIT\) provisioning\. This process updates user information each time a user signs in so that attribute information is current\. JIT provisioning is for users only\.

If you delete a user from your Active Directory, the user can no longer sign\-in to AWS SSO, AWS accounts, or any assigned applications\. However, AWS SSO does not remove the provisioned user automatically\. These JIT\-provisioned users remain in AWS SSO and are visible to AWS SSO integrated applications until you remove them manually\. Removing a JIT provisioned user has no effect in Active Directory\. JIT provisioning is a one\-way operation\. Hence, if you accidentally remove a JIT provisioned user who is still in your Active Directory, AWS SSO reprovisions them automatically the next time they sign into AWS SSO\. While removed, the user is unavailable for reference by AWS SSO\-integrated applications\.

For more information above provisioning, see [User and group provisioning](users-groups-provisioning.md#user-group-provision)\.

**Topics**
+ [Provisioning When Users Come from Active Directory](#provision-users-from-ad)
+ [Connect AWS SSO to an AWS Managed Microsoft AD Directory](connectawsad.md)
+ [Connect AWS SSO to a Self\-Managed Active Directory](connectonpremad.md)
+ [Attribute Mappings](attributemappingsconcept.md)
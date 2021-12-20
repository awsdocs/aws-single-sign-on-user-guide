# Connect to your Microsoft AD directory<a name="manage-your-identity-source-ad"></a>

With AWS Single Sign\-On, administrators can connect their self\-managed Active Directory \(AD\) or their AWS Managed Microsoft AD directory using AWS Directory Service\. This Microsoft AD directory defines the pool of identities that administrators can pull from when using the AWS SSO console to assign single sign\-on \(SSO\) access\. After connecting their corporate directory to AWS SSO, administrators can then grant their AD users or groups access to AWS accounts, cloud applications, or both\. 

AWS Directory Service helps you to set up and run a standalone AWS Managed Microsoft AD directory hosted in the AWS Cloud\. You can also use AWS Directory Service to connect your AWS resources with an existing self\-managed AD\. To configure AWS Directory Service to work with your self\-managed AD, you must first set up trust relationships to extend authentication to the cloud\.

AWS SSO uses the connection provided by AWS Directory Service to perform pass\-through authentication to the source AD instance, leveraging the Kerberos protocol\. When you use AWS Managed Microsoft AD as your identity source, AWS SSO can work with users from AWS Managed Microsoft AD or from any domain connected through an AD trust\. If you want to locate your users in four or more domains, users must use the `DOMAIN\user` syntax as their user name when performing sign\-ins to AWS SSO\.

**Notes**  
As a prerequisite step, make sure your AD Connector or AWS Managed Microsoft AD directory in AWS Directory Service resides within your AWS Organizations management account\. For more information, see [AWS SSO prerequisites](prereqs.md)\.
AWS SSO does not support SAMBA 4\-based Simple AD as a connected directory\.

## Provisioning when users come from Active Directory<a name="provision-users-from-ad"></a>

AWS SSO uses the connection provided by the AWS Directory Service to synchronize user, group, and membership information from your source AD to the AWS SSO identity store\. No password information is synchronized to AWS SSO, since user authentication takes place directly from the source AD\. This identity data is used by AWS SSO integrated applications to facilitate in\-app lookup, authorization and collaboration scenarios without passing LDAP activity all the way back to the source AD\.

### How It Works<a name="provision-users-from-ad-how-it-works"></a>

AWS SSO refreshes the AD\-based identity data in the identity store using the following process\. 

#### Creation<a name="how-it-works-creation"></a>

When users or groups are assigned to AWS resources or applications using the AWS console or entitlement API calls, the users, groups and membership information are periodically synchronized into the AWS SSO identity store\. Users or groups added to AWS SSO assignments will usually appear in the AWS identity store within two hours, but may take longer based on the amount of data being synchronized\. Only users and groups that are directly assigned access, or are members of a group that is assigned access, are synchronized\. 

Groups that are members of assigned groups \(called nested groups\) are also written to the identity store\. Users that are members of nested groups are “flattened,” meaning they are added to the parent group in the AWS SSO identity store\. This allows AWS SSO administrators to use only the parent group for authorization\. 

If a user accesses AWS SSO before their user object has been synchronized for the first time, that user’s identity store object is created on demand using just\-in\-time \(JIT\) provisioning\. Users created by JIT provisioning are not synchronized unless they have directly assigned or group\-based AWS SSO entitlements\. Group memberships for JIT\-provisioned users are unavailable until after synchronization\.

#### Update<a name="how-it-works-update"></a>

The identity data in the AWS SSO identity store stays fresh by periodically reading data from the source AD\. Identity data changed in AD will usually appear in the AWS identity store within four hours, but may take longer based on the amount of data being synchronized\. 

User and group objects and their memberships are created or updated in AWS SSO to map to the corresponding objects in the source AD\. For user attributes, only the subset of attributes listed in the Attribute Mapping section of the AWS SSO console are updated in AWS SSO\. In addition, user attributes are updated with each user authentication event\.

#### Deletion<a name="how-it-works-deletion"></a>

Users and groups are deleted from the AWS SSO identity store when the corresponding user or group objects are deleted from the source AD\. 

For more information above provisioning, see [User and group provisioning](users-groups-provisioning.md#user-group-provision)\.

**Topics**
+ [Provisioning when users come from Active Directory](#provision-users-from-ad)
+ [Connect AWS SSO to an AWS Managed Microsoft AD directory](connectawsad.md)
+ [Connect AWS SSO to a self\-managed Active Directory](connectonpremad.md)
+ [Attribute mappings](attributemappingsconcept.md)
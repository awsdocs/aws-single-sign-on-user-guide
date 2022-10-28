# IAM Identity Center AD sync<a name="provision-users-from-ad-ADsync"></a>

With IAM Identity Center AD sync, you use IAM Identity Center to assign users and groups in Active Directory access to AWS accounts and to applications AWS accounts and applications \[Identity Center enabled applications, cloud applications, or custom Security Assertion Markup Language \(SAML 2\.0\) applications\]\. All identities with assignments are automatically synced into IAM Identity Center\.

## How IAM Identity Center AD sync works<a name="provision-users-from-ad-how-it-works-ADsync"></a>

IAM Identity Center refreshes the AD\-based identity data in the identity store using the following process\. 

### Creation<a name="how-it-works-creation-ADsync"></a>

When you assign users or groups to AWS accounts or applications by using the AWS console or the assignment API calls, information about the users, groups, and membership is periodically synchronized into the IAM Identity Center identity store\. Users or groups that are added to IAM Identity Center assignments usually appear in the AWS identity store within two hours\. Depending on the amount of data being synchronized, this process might take longer\. Only users and groups that are directly assigned access, or are members of a group that is assigned access, are synchronized\. 

Groups that are members of other groups \(called nested groups\) are also written to the identity store\. The nested groups are “flattened,” that is, users in the nested groups are added to the parent group in the IAM Identity Center identity store\. This allows you to use only the parent group for authorization\. 

If a user accesses IAM Identity Center before their user object has been synchronized for the first time, that user’s identity store object is created on demand using just\-in\-time \(JIT\) provisioning\. Users created by JIT provisioning are not synchronized unless they have directly assigned or group\-based IAM Identity Center entitlements\. Group memberships for JIT\-provisioned users are unavailable until after synchronization\.

### Update<a name="how-it-works-update-ADsync"></a>

The identity data in the IAM Identity Center identity store stays fresh by periodically reading data from the source directory in Active Directory\. Identity data that is changed in Active Directory will usually appear in the AWS identity store within four hours\. Depending on the amount of data being synchronized, this process might take longer\. 

User and group objects and their memberships are created or updated in IAM Identity Center to map to the corresponding objects in the source directory in Active Directory\. For user attributes, only the subset of attributes listed in the **Attribute Mapping** section of the IAM Identity Center console is updated in IAM Identity Center\. In addition, user attributes are updated with each user authentication event\.

### Deletion<a name="how-it-works-deletion-ADsync"></a>

Users and groups are deleted from the IAM Identity Center identity store when the corresponding user or group objects are deleted from the source directory in Active Directory\. 
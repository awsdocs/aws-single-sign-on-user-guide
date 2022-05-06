# AWS SSO configurable AD sync<a name="provision-users-from-ad-configurable-ADsync"></a>

AWS SSO configurable Active Directory \(AD\) sync enables you to explicitly configure the identities in Microsoft Active Directory that are automatically synchronized into AWS SSO and control the synchronization process\.

The following topics provide information to enable you to configure and administer configurable AD sync\.

**Topics**
+ [Prerequisites and considerations](#prerequisites-configurable-ADsync)
+ [How configurable AD sync works](#how-it-works-configurable-ADsync)
+ [Configure and manage your sync scope](#manage-sync-configurable-ADsync)

## Prerequisites and considerations<a name="prerequisites-configurable-ADsync"></a>

Before you use configurable AD sync, be aware of the following prerequisites and considerations:
+ **Specifying users and groups in Active Directory to sync**

  Before you can use AWS SSO to assign new users and groups access to AWS accounts and to applications \[AWS SSO\-integrated applications, cloud applications, or custom Security Assertion Markup Language \(SAML 2\.0\) applications\], you must specify the users and groups in Active Directory to sync, and then sync them into AWS SSO\.

  With AD sync, when you make assignments for new users and groups by using the AWS SSO console or related assignment API actions, AWS SSO searches the domain controller directly for the specified users or groups, completes the assignment, and then periodically syncs the user or group metadata into AWS SSO\.

  With configurable AD sync, AWS SSO doesn't search your domain controller directly for users and groups\. Instead, you must first specify the list of users and groups to sync\. You can configure this list, also known as the *sync scope*, in one of the following ways, depending on whether you have users and groups that are already synced into AWS SSO, or you have new users and groups that you are syncing for the first time by using configurable AD sync\.
  + Existing users and groups: If you have users and groups that are already synced into AWS SSO, the sync scope in configurable AD sync is prepopulated with a list of those users and groups\. To assign new users or groups, you must specifically add them to the sync scope\.
  + New users and groups: If you are assigning new users and groups access to AWS accounts and to applications, you must specify which users and groups to add to the sync scope in configurable AD sync before you can use AWS SSO to make the assignment\.
+ **Making assignments to nested groups in Active Directory**

  Using configurable AD sync to make assignments to a group in Active Directory that contains other groups \(nested groups\) might increase the scope of users who have access to AWS accounts or to applications\.

  With AD sync, when you make assignments to a group in Active Directory that contains other groups \(nested groups\), only the direct members of the group can access the account\. For example, if you assign access to Group A, and Group B is a member of Group A, only the direct members of Group A can access the account\. No members of Group B inherit the access\.

  With configurable AD sync, when you make assignments to a group in Active Directory that contains nested groups, the assignment applies to all users, including those in nested groups\. For example, if you assign access to Group A, and Group B is a member of Group A, members of Group B also inherit this access\.
+ **Updating automated workflows**

  If you have automated workflows that use the AWS SSO identity store API actions and AWS SSO assignment API actions to assign new users and groups access to accounts and to applications, and to sync them into AWS SSO, you must adjust those workflows by April 15, 2022 so that they function as expected with configurable AD sync\. Configurable AD sync changes the order in which user and group assignment and provisioning occur, and the way in which queries are performed\.

  With AD sync, the process of assignments occurs first\. You assign users and groups access to AWS accounts and to applications\. After the users and groups are assigned access, they are automatically provisioned \(synced into AWS SSO\)\. If you have an automated workflow, this means that when you add a new user to Active Directory, your automated workflow can query Active Directory for the user by using the identity store `ListUser` API action, and then assign the user access by using the AWS SSO assignment API actions\. Because the user has an assignment, that user is automatically provisioned into AWS SSO\.

  With configurable AD sync, provisioning occurs first, and it is not automatically performed\. Instead, you must first explicitly add users and groups to the identity store by adding them to your sync scope\. For information about the recommended steps for automating your sync configuration for configurable AD sync, see [Automate your sync configuration for configurable AD sync](#automate-sync-configuration-configurable-ADsync)\. 

## How configurable AD sync works<a name="how-it-works-configurable-ADsync"></a>

AWS SSO refreshes the AD\-based identity data in the identity store by using the following process\. 

### Creation<a name="how-it-works-creation-configurable-ADsync"></a>

After you connect your self\-managed directory in Active Directory or your AWS Managed Microsoft AD directory that is managed by AWS Directory Service to AWS SSO, you can explicitly configure the Active Directory users and groups that you want to sync into the AWS SSO identity store\. The identities that you choose will be synchronized every three hours or so into the AWS SSO identity store\. Depending on the size of your directory, the sync process might take longer\.

Groups that are members of other groups \(called nested groups or child groups\) are also written to the identity store\. The nested groups are *flattened*, that is, users in the nested groups are added to the parent group in the AWS SSO identity store\. This allows you to use the parent group for authorization\. Any access that you assign to the parent group applies to all users in the parent group and the users in nested \(child\) groups\. 

You can only assign access to new users or groups after they are synchronized into the AWS SSO identity store\. 

### Update<a name="how-it-works-update-configurable-ADsync"></a>

The identity data in the AWS SSO identity store stays fresh by periodically reading data from the source directory in Active Directory\. Identity data changed in AD usually appears in the AWS identity store within four hours, but might take longer based on the amount of data being synchronized\. 

User and group objects that are in the sync scope and their memberships are created or updated in AWS SSO to map to the corresponding objects in the source directory in Active Directory\. For user attributes, only the subset of attributes listed in the **Attribute Mapping** section of the AWS SSO console are updated in AWS SSO\.

You can also update the subset of users and groups that you synchronize into the AWS SSO identity store\. You can choose to add new users or groups to this subset, or remove them\. Any identities that you add are synchronized at the next scheduled sync\. Identities that you remove from the subset will stop being updated in the AWS SSO identity store\. Any user who isn't synchronized for more than 28 days will be disabled in the AWS SSO identity store\. The corresponding user objects will be automatically disabled in the AWS SSO identity store during the next sync cycle, unless they are part of another group that is still part of the sync scope\. 

### Deletion<a name="how-it-works-deletion-configurable-ADsync"></a>

Users and groups are deleted from the AWS SSO identity store when the corresponding user or group objects are deleted from the source directory in Active Directory\. Alternatively, you can explicitly delete user objects from the AWS SSO identity store by using the AWS SSO console\. If you use the AWS SSO console, you must also remove the users from the sync scope to ensure that they aren't re\-synced back into AWS SSO during the next sync cycle\.

You can also pause and restart synchronization at any time\. If you pause synchronization for more than 28 days, all your users will be disabled\.

## Configure and manage your sync scope<a name="manage-sync-configurable-ADsync"></a>

You can configure your sync scope in either of the following ways:
+ Guided setup: If you are synchronizing your users and groups from Active Directory into AWS SSO for the first time, follow the steps in [Guided setup](#manage-sync-guided-setup-configurable-ADsync) to configure your sync scope\. After you complete the guided setup, you can modify your sync scope at any time by following the other procedures in this section\.
+ If you already have users and groups that are synchronized into AWS SSO or you don't want to follow the guided setup, choose **Manage sync**\. Skip the guided setup procedure and follow the other procedures in this section as required to configure and manage your sync scope\.

**Topics**
+ [Guided setup](#manage-sync-guided-setup-configurable-ADsync)
+ [Add users and groups to your sync scope](#manage-sync-add-users-groups-configurable-ADsync)
+ [Remove users and groups from your sync scope](#manage-sync-remove-users-groups-configurable-ADsync)
+ [Pause and resume your sync](#manage-sync-pause-resume-sync-configurable-ADsync)
+ [Configure attribute mappings for your sync](#manage-sync-configure-attribute-mapping-configurable-ADsync)
+ [Automate your sync configuration for configurable AD sync](#automate-sync-configuration-configurable-ADsync)

### Guided setup<a name="manage-sync-guided-setup-configurable-ADsync"></a>

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the AWS SSO console is using one of the AWS Regions where your AWS Managed Microsoft AD directory is located before you move to the next step\.

1. Choose **Settings**\.

1. At the top of the page, in the notification message, choose **Start guided setup**\.

1. In **Step 1 – *optional*: Configure attribute mappings**, review the default user and group attribute mappings\. If no changes are required, choose **Next**\. If changes are required, make the changes, and then choose **Save changes**\.

1. In **Step 2 – *optional*: Configure sync scope**, choose the **Users** tab\. Then, enter the exact username of the user that you want to add to your sync scope and choose **Add**\. Next, choose the **Groups** tab\. Enter the exact group name of the group that you want to add to your sync scope and choose **Add**\. Then, choose **Next**\. If you want to add users and groups to your sync scope later, make no changes and choose **Next**\.

1. In **Step 3: Review and save configuration**, confirm your **Attribute mappings** in **Step 1: Attribute mappings** and your **Users and groups** in **Step 2: Sync scope**\. Choose **Save configuration**\. This takes you to the **Manage Sync** page\.

### Add users and groups to your sync scope<a name="manage-sync-add-users-groups-configurable-ADsync"></a>

**To add users**

1. Open the [AWS SSO console\.](https://console.aws.amazon.com/singlesignon)

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, choose **Actions**, and then choose **Manage Sync**\.

1. On the **Manage Sync** page, choose the **Users** tab, and then choose **Add users and groups**\.

1. Choose the **Users** tab\. Under **User**, enter the exact user name and choose **Add**\.

1. Under **Selected Users and Groups**, review the users that you want to add\.

   1. To remove a user from this list, select the check box beside the entry and choose **Remove**\.

1. Choose **Submit**\.

**To add groups**

1. Open the [AWS SSO console\.](https://console.aws.amazon.com/singlesignon)

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, choose **Actions**, and then choose **Manage Sync**\.

1. On the **Manage Sync** page, choose the **Groups** tab, and then choose **Add users and groups**\.

1. Choose the **Groups** tab\. Under **Group**, enter the exact group name and choose **Add**\.

1. Under **Selected Users and Groups**, review the groups that you want to add\.

   1. To remove a group from this list, select the check box beside the entry and choose **Remove**\.

1. Choose **Submit**\.

### Remove users and groups from your sync scope<a name="manage-sync-remove-users-groups-configurable-ADsync"></a>

For more information about what happens when you remove users and groups from your sync scope, see [How configurable AD sync works](#how-it-works-configurable-ADsync)\.

**To remove users**

1. Open the [AWS SSO console\.](https://console.aws.amazon.com/singlesignon)

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, choose **Actions**, and then choose **Manage Sync**\.

1. Choose the **Users** tab\.

1. Under **Users in sync scope**, select the check box beside the user that you want to delete\. To delete all users, select the check box beside **Username**\.

1. Choose **Remove**\.

**To remove groups**

1. Open the [AWS SSO console\.](https://console.aws.amazon.com/singlesignon)

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, choose **Actions**, and then choose **Manage Sync**\.

1. Choose the **Groups** tab\.

1. Under **Groups in sync scope**, select the check box beside the user that you want to delete\. To delete all groups, select the check box beside **Group name**\.

1. Choose **Remove**\.

### Pause and resume your sync<a name="manage-sync-pause-resume-sync-configurable-ADsync"></a>

Pausing your sync pauses all future sync cycles and prevents any changes that you make to users and groups in Active Directory from being reflected in AWS SSO\. After you resume the sync, the sync cycle picks up these changes from the next scheduled sync\.

**To pause your sync**

1. Open the [AWS SSO console\.](https://console.aws.amazon.com/singlesignon)

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, choose **Actions**, and then choose **Manage Sync**\.

1. Under **Manage Sync**, choose **Pause sync**\.

**To resume your sync**

1. Open the [AWS SSO console\.](https://console.aws.amazon.com/singlesignon)

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, choose **Actions**, and then choose **Manage Sync**\.

1. Under **Manage Sync**, choose **Resume sync**\.
**Note**  
If you see **Pause sync** instead of **Resume sync**, the sync from Active Directory to AWS SSO has already resumed\.

### Configure attribute mappings for your sync<a name="manage-sync-configure-attribute-mapping-configurable-ADsync"></a>

For more information about available attributes, see [Attribute mappings](attributemappingsconcept.md)\.

**To configure attribute mappings in AWS SSO to your directory**

1. Open the [AWS SSO console\.](https://console.aws.amazon.com/singlesignon)

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, choose **Actions**, and then choose **Manage Sync**\.

1. Under **Manage Sync**, choose **View attribute mapping**\.

1. Under **Active Directory user attributes**, configure **AWS SSO identity store attributes** and **Active Directory user attributes**\. For example, you might want to map the AWS SSO identity store attribute `email` to the Active Directory user directory attribute `${objectguid}`\.
**Note**  
Under **Group attributes**, **AWS SSO identity store attributes** and **Active Directory group attributes** can't be changed\.

1. Choose **Save changes**\. This returns you to the **Manage Sync** page\.

### Automate your sync configuration for configurable AD sync<a name="automate-sync-configuration-configurable-ADsync"></a>

To ensure that your automated workflow works as expected with configurable AD sync, we recommend that you perform the following steps to automate your sync configuration\.

**To automate your sync configuration for configurable AD sync**

1. In Active Directory, create a *parent sync group* to contain all users and groups that you want to sync into AWS SSO\. For example, you can name the group *AllAWSSSOUsersAndGroups*\.

1. In AWS SSO, add the parent sync group to your configurable sync list\. AWS SSO will synchronize all users, groups, sub\-groups, and members of all groups contained within the parent sync group\.

1. Use the Active Directory user and group management API actions provided by Microsoft to add or remove users and groups from the parent sync group\.
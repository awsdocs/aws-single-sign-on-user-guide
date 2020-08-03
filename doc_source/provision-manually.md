# Manual Provisioning<a name="provision-manually"></a>

Some IdPs do not have System for Cross\-domain Identity Management \(SCIM\) support or have an incompatible SCIM implementation\. In those cases, you can manually provision users through the AWS SSO console\. When you add users to AWS SSO, ensure that you set the user name to be identical to the user name that you have in your IdP\. At a minimum, you must have a unique email address and user name\. For more information, see [User name and email address uniqueness](users-groups-provisioning.md#username-email-unique)\.

You must also manage all groups manually in AWS SSO\. To do this, you create the groups and add them using the AWS SSO console\. For more information, see [Groups](users-groups-provisioning.md#groups-concept)\.
# Considerations for changing your identity source<a name="manage-your-identity-source-considerations"></a>

Although you can change your identity source at any time, we recommend that you consider how this change might affect your current deployment\. If you're already managing users and groups in one identity source, changing to a different identity source might remove all user and group assignments that you configured in IAM Identity Center\. If this occurs, all users, including the administrative user in IAM Identity Center, will lose single sign\-on access to their AWS accounts and applications\.

Before you change the identity source for IAM Identity Center, review the following considerations before you proceed\. If you want to proceed with changing your identity source, see [Change your identity source](manage-your-identity-source-change.md) for more information\.

## Changing between IAM Identity Center and Active Directory<a name="changing-between-sso-and-active-directory"></a>

If you're already managing users and groups in Active Directory, we recommend that you consider connecting your directory when you enable IAM Identity Center and choose your identity source\. This should be done before you create any users and groups in the default Identity Center directory and make any assignments\. If you're already managing users and groups in the default Identity Center directory, changing your identity source to Active Directory deletes your users and groups from the Identity Center directory\. This change also removes your assignments\. In this case, after you change to Active Directory, you must synchronize your users and groups from Active Directory into the Identity Center directory, and then reapply their assignments\. If you choose to not use Active Directory, you must create your users and groups in the Identity Center directory, and then make assignments\. 

For information about how IAM Identity Center provisions users and groups, see [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)\.

## Changing between IAM Identity Center and an external identity provider \(IdP\)<a name="changing-between-sso-and-azure-active-directory"></a>

If you change your identity source from IAM Identity Center to an external IdP, IAM Identity Center preserves all your assignments\. However, these assignments will work only if the user names and groups in IAM Identity Center match those in the external IdP\. Any user names and groups that don't match are unusable\. If you change from an external IdP to IAM Identity Center, IAM Identity Center preserves all users, groups, and assignments\. Users who had passwords in IAM Identity Center can continue signing in with their old passwords\. For users who were in the external IdP and weren't in IAM Identity Center, you must force a password reset\.

For information about how IAM Identity Center provisions users and groups, see [Connect to an external identity provider](manage-your-identity-source-idp.md)\.

## Changing from one external IdP to an external IdP<a name="changing-from-one-idp-to-another-idp"></a>

If you're already using an external IdP as your identity source for IAM Identity Center and you change to a different external IdP, IAM Identity Center preserves all of your assignments\. The user assignments, group assignments, and group memberships will continue to work as long as the new IdP sends the correct assertions \(for example, SAML nameIDs\)\. These assertions must match the user names in IAM Identity Center when your users authenticate through the new external IdP\. If you are using SCIM for provisioning into IAM Identity Center, we recommend that you review the IdP\-specific information in this guide and the documentation provided by the IdP to ensure that the new provider will match users and groups correctly when SCIM is enabled\.

For information about how IAM Identity Center provisions users and groups, see [Connect to an external identity provider](manage-your-identity-source-idp.md)\.

## Changing between Active Directory and an external IdP<a name="changing-between-microsoft-ad-and-azure-active-directory"></a>

If you change your identity source from an external IdP to Active Directory, or from Active Directory to an external IdP, all users, groups, and assignments are deleted from IAM Identity Center\. No user or group information is affected in either the external IdP or Active Directory\. If you change to an external IdP, you must configure IAM Identity Center to provision your users\. Alternatively, you must manually provision the users and groups for the external IdP before you can configure assignments\. If you change to Active Directory, you must create assignments with the users and groups that are in your directory in Active Directory\.

For information about how IAM Identity Center provisions users and groups, see [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)\.
# Considerations for changing your identity source<a name="manage-your-identity-source-considerations"></a>

Before you proceed with the steps in [Change your identity source](manage-your-identity-source-change.md), we recommend that you first review the following important information\. This information can help you understand how the process of switching your identity source might affect your current deployment\.

## Changing between AWS SSO and Active Directory<a name="changing-between-sso-and-active-directory"></a>

Whether you switch from Microsoft AD to AWS SSO or from AWS SSO to Microsoft AD, the conversion deletes all users, groups, and assignments \(entitlements\)\. If you switch to AWS SSO, you must create your users, groups, and entitlements\. If you switch to Microsoft AD, you must create entitlements with the users and groups that are in your Microsoft AD\.

For information about how AWS SSO provisions users and groups, see [Connect to your Microsoft AD directory](manage-your-identity-source-ad.md)\.

## Changing between AWS SSO and an external identity provider \(IdP\)<a name="changing-between-sso-and-azure-active-directory"></a>

If you switch to an external IdP, AWS SSO preserves all entitlements you had\. The user and group entitlements will work if the AWS SSO user names and groups match those that you have in the external IdP\. Any unmatched users and groups are unusable\. If you switch from an external IdP to AWS SSO, AWS SSO preserves all users, groups, and entitlements\. If any of the users previously had passwords in AWS SSO, then those users can continue signing in with their old passwords\. The administrator must force a password reset for users that came from the external IdP and that did not previously exist in AWS SSO\.

For information about how AWS SSO provisions users and groups, see [Connect to your external identity provider](manage-your-identity-source-idp.md)\.

## Changing from one external IdP to another external IdP<a name="changing-from-one-idp-to-another-idp"></a>

If you are already using an external IdP in AWS SSO and switch to a different external IdP, AWS SSO preserves all entitlements you had\. The user entitlements, group entitlements, and group memberships will continue to work as long as the new IdP sends the correct assertions \(e\.g\., SAML nameIDs\)\. These assertions must match the usernames in AWS SSO when your users authenticate through the new external IdP\. Note that if you are using SCIM for provisioning into AWS SSO, you will want to review the IdP\-specific information in this guide and/or the IdP’s documentation to ensure that the new provider will match users and groups correctly when SCIM is enabled\.

For information about how AWS SSO provisions users and groups, see [Connect to your external identity provider](manage-your-identity-source-idp.md)\.

## Changing between Microsoft AD and an external IdP<a name="changing-between-microsoft-ad-and-azure-active-directory"></a>

Whether you switch from an external IdP to Microsoft AD, or from Microsoft AD to an external IdP, the conversion deletes all users, groups, and entitlements in AWS SSO\. No user or group information is affected in either the external IdP or Microsoft AD\. If you switch to an external IdP, you must configure AWS SSO to provision your users\. Or you must manually provision your external IdP users and groups before you can configure entitlements\. If you switch to Microsoft AD, you must create entitlements with the users and groups that are in your Microsoft AD\.

For information about how AWS SSO provisions users and groups, see [Connect to your Microsoft AD directory](manage-your-identity-source-ad.md)\.
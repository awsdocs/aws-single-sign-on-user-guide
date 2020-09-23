# Considerations for Changing Your Identity Source<a name="manage-your-identity-source-considerations"></a>

Before you proceed with the steps in [Change Your Identity Source](manage-your-identity-source-change.md), we recommend that you first review the following important information\. This information can help you understand how the process of switching your identity source might affect your current deployment\.

## Changing Between AWS SSO and Active Directory<a name="changing-between-sso-and-active-directory"></a>

Whether you switch from Microsoft AD to AWS SSO or from AWS SSO to Microsoft AD, the conversion deletes all users, groups, and assignments \(entitlements\)\. If you switch to AWS SSO, you must create your users, groups, and entitlements\. If you switch to Microsoft AD, you must create entitlements with the users and groups that are in your Microsoft AD\.

## Changing Between AWS SSO and an External Identity Provider<a name="changing-between-sso-and-azure-active-directory"></a>

If you switch to an external IdP, AWS SSO preserves all entitlements you had\. The user and group entitlements will work if the AWS SSO user names and groups match those that you have in the external IdP\. Any unmatched users and groups are unusable\. If you switch from an external IdP to AWS SSO, AWS SSO preserves all users, groups, and entitlements\. If any of the users previously had passwords in AWS SSO, then those users can continue signing in with their old passwords\. The administrator must force a password reset for users that came from the external IdP and that did not previously exist in AWS SSO\.

## Changing Between Microsoft AD and an External Identity Provider<a name="changing-between-microsoft-ad-and-azure-active-directory"></a>

Whether you switch from an external IdP to Microsoft AD, or from Microsoft AD to an external IdP, the conversion deletes all users, groups, and entitlements in AWS SSO\. No user or group information is affected in either the external IdP or Microsoft AD\. If you switch to an external IdP, you must configure AWS SSO to provision your users\. Or you must manually provision your external IdP users and groups before you can configure entitlements\. If you switch to Microsoft AD, you must create entitlements with the users and groups that are in your Microsoft AD\.
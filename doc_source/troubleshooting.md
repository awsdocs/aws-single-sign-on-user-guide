# Troubleshooting AWS SSO issues<a name="troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter while setting up or using the AWS SSO console\.

## Issues regarding contents of SAML assertions created by AWS SSO<a name="issue1"></a>

AWS SSO provides a web\-based debug experience for the SAML assertions created and sent by AWS SSO, including attributes within these assertions, when accessing AWS accounts and SAML applications from the user portal\. To see the details of a SAML assertion that AWS SSO generates, use the following steps\.

1. Sign in to the AWS SSO user portal\.

1. While you are signed into the portal, hold the **Shift** key down, choose the application tile, and then release the **Shift** key\. If accessing an AWS account, hold the **Shift** key down while choosing the **Management console** link for the desired account and permission set\.

1. Examine the information on the page titled **You are now in administrator mode**\. To keep this information for future reference, choose **Copy XML**, and paste the contents elsewhere\.

1. Choose **Send to <application>** to continue\. This option sends the assertion to the service provider\.

**Note**  
Some browser configurations and operating systems may not support this procedure\. This procedure has been tested on Windows 10 using Firefox, Chrome, and Edge browsers\.

## Specific users fail to synchronize into AWS SSO from an external SCIM provider<a name="issue2"></a>

If SCIM synchronization succeeds for a subset of users configured in your IdP for provisioning into AWS SSO but fails for others, you might see an error similar to `'Request is unparsable, syntactically incorrect, or violates schema'` from your identity provider\. You may also see detailed provisioning failure messages in AWS CloudTrail\.

This issue often indicates that the user in your IdP is configured in a way that AWS SSO does not support\. Full details of the AWS SSO SCIM implementation, including the specifications of required, optional, and forbidden parameters and operations for user objects, can be found in the [AWS SSO SCIM Implementation Developer Guide](https://docs.aws.amazon.com/singlesignon/latest/developerguide/what-is-scim.html)\. The *SCIM Developer Guide* should be considered authoritative for information around SCIM requirements\. However, the following are a couple of common reasons for this error:

1. The user object in the IdP lacks a first \(given\) name, a last \(family\) name, and/or a display name\.

   1. **Solution:** Add a first \(given\), last \(family\), and display name for the user object\. In addition, ensure that the SCIM provisioning mappings for user objects at your IdP are configured to send nonempty values for all of these attributes\.

1. More than one value for a single attribute is being sent for the user \(also known as “multi\-value attributes”\)\. For example, the user may have both a work and a home phone number specified in the IdP, or multiple emails or physical addresses, and your IdP is configured to try to synchronize multiple or all values for that attribute\. 

   1. **Solution options:**

     1. Update your SCIM provisioning mappings for user objects at your IdP to send only a single value for a given attribute\. For example, configure a mapping that sends only the work phone number for each user\. 

     1. If the additional attributes can safely be removed from the user object at the IdP, you can remove the additional values, leaving either one or zero values set for that attribute for the user\.

     1. If the attribute is not needed for any actions in AWS, remove the mapping for that attribute from the SCIM provisioning mappings for user objects at your IdP\.

1. Your IdP is trying to match users in the target \(AWS SSO, in this case\) based on multiple attributes\. Since user names are guaranteed unique within a given AWS SSO instance, you only need to specify `username` as the attribute used for matching\. 

   1. **Solution:** Ensure that your SCIM configuration in your IdP is using only a single attribute for matching with users in AWS SSO\. For example, mapping `username` or `userPrincipalName` in the IdP to the `userName` attribute in SCIM for provisioning to AWS SSO will be correct and sufficient for most implementations\.

## Users can’t sign in when their user name is in UPN format<a name="issue3"></a>

Users might not be able to sign in to the user portal based on the format they use to enter in their user name on the sign in page\. For the most part, users can sign in to the user portal using either their plain user name, their down\-level logon name \(DOMAIN\\UserName\) or their UPN logon name \([UserName@Corp\.Example\.com](mailto:UserName@Corp.Example.com)\)\. The exception to this is when AWS SSO is using a connected directory that has been enabled with MFA and the verification mode has been set to either **Context\-aware** or **Always\-on**\. In this scenario, users must sign in with their down\-level logon name \(DOMAIN\\UserName\)\. For more information, see [Multi\-factor authentication](enable-mfa.md)\. For general information about user name formats used to sign in to Active Directory, see [User Name Formats](https://docs.microsoft.com/en-us/windows/desktop/secauthn/user-name-formats) on the Microsoft documentation website\.

## I get a ‘Cannot perform the operation on the protected role' error when modifying an IAM role<a name="issue4"></a>

When reviewing IAM Roles in an account, you may notice role names beginning with ‘AWSReservedSSO\_’\. These are the roles which the AWS SSO service has created in the account, and they came from assigning a permission set to the account\. Attempting to modify these roles from within the IAM console will result in the following error:

```
'Cannot perform the operation on the protected role 'AWSReservedSSO_RoleName_Here' - this role is only modifiable by AWS'
```

These roles can only be modified from the AWS SSO Administrator console, which is in the management account of AWS Organizations\. Once modified, you can then push the changes down to the AWS accounts that it is assigned to\.

## Directory users cannot reset their password<a name="issue5"></a>

When a directory user resets their password using the **Forgot Password?** option during sign\-in of the user portal, their new password must adhere to the default password policy as described in [Password requirements when managing identities in AWS SSO](password-requirements.md)\. 

If a user enters a password that adheres to the policy and then receives the error `We couldn't update your password`, check to see if AWS CloudTrail recorded the failure\. This can be done by searching in the Event History console of CloudTrail using the following filter:

```
"UpdatePassword"
```

If the message states the following, then you may need to contact support:

```
"errorCode": "InternalFailure",
      "errorMessage": "An unknown error occurred“
```

Another possible cause of this issue is in the naming convention that was applied to the user name value\. Naming conventions must follow specific patterns such as 'surname\.givenName'\. However, some user names can be quite long, or contain special characters, and this can cause characters to be dropped in the API call, thereby resulting in an error\. You may want to attempt a password reset with a test user in the same manner to verify if this is the case\.

If the issue persists, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## My user is referenced in a permission set but can’t access the assigned accounts or applications<a name="issue6"></a>

This issue can occur if you’re using System for Cross\-domain Identity Management \(SCIM\) for Automatic Provisioning with an external identity provider\. Specifically, when a user, or the group the user was a member of, is deleted then re\-created using the same user name \(for users\) or name \(for groups\) in the identity provider, a new unique internal identifier is created for the new user or group in AWS SSO\. However, AWS SSO still has a reference to the old identifier in its permission database, such that the name of the user or group still appears in the UI, but access fails\. This is because the underlying user or group ID to which the UI refers no longer exists\.

To restore AWS account access in this case, you can remove access for the old user or group from the AWS account\(s\) where it was originally assigned, and then reassign access back to the user or group\. This updates the permission set with the correct identifier for the new user or group\. Similarly, to restore application access, you can remove access for the user or group from the assigned users list for that application, then add the user or group back again\.

You can also check to see if AWS CloudTrail recorded the failure by searching your CloudTrail logs for SCIM synchronization events that reference the name of the user or group in question\.

## I cannot get my cloud application configured correctly<a name="issue7"></a>

Each service provider of a preintegrated cloud application in AWS SSO has its own detailed instruction manual\. You can access the manual from the **Configuration** tab for that application in the AWS SSO console\.

If the problem is related to setting up the trust between the service provider's application and AWS SSO, make sure to check the instruction manual for troubleshooting steps\.

## Error 'An unexpected error has occurred' when a user tries to sign in using an external identity provider<a name="issue8"></a>

This error may occur for multiple reasons, but one common reason is a mis\-match between the user information carried in the SAML request, and the information for the user in AWS SSO\.

In order for an AWS SSO user to sign in successfully when using an external IdP as the identity source, the following must be true:
+ The SAML nameID format \(configured at your identity provider\) must be ‘email’
+ The nameID value must be a properly \(RFC2822\)\-formatted string \(user@domain\.com\)
+ The nameID value must exactly match the user name of an existing user in AWS SSO \(it doesn’t matter if the email address in AWS SSO matches or not – the inbound match is based on username\)
+ The following statements apply if [Attributes for access control](attributesforaccesscontrol.md) is enabled in your AWS SSO account:
  + The number of attributes mapped in the SAML request must be 50 or less\.
  + The SAML request must not contain multi\-valued attributes\.
  + The SAML request must not contain multiple attributes with the same name\.
  + The attribute must not contain structured XML as the value\.
  + The Name format must be a SAML specified format, not generic format\.

**Note**  
AWS SSO does not perform “just in time” creation of users or groups for new users or groups via SAML federation\. This means that the user must be pre\-created in AWS SSO, either manually or via automatic provisioning, in order to sign in to AWS SSO\.

This error can also occur when the Assertion Consumer Service \(ACS\) endpoint configured in your identity provider does not match the ACS URL provided by your AWS SSO instance\. Ensure that these two values match exactly\.

Additionally, you can troubleshoot external identity provider sign\-in failures further by going to AWS CloudTrail and filtering on the event name **ExternalIdPDirectoryLogin**\.

## Error 'Attributes for access control failed to enable'<a name="issue9"></a>

This error may occur if the user enabling ABAC does not have the `iam:UpdateAssumeRolePolicy` permissions required to enable [Attributes for access control](attributesforaccesscontrol.md)\.

## I get a 'Browser not supported' message when I attempt to register a device for MFA<a name="issue10"></a>

WebAuthn is currently supported in Google Chrome, Mozilla Firefox, Microsoft Edge and Apple Safari web browsers, as well as Windows 10 and Android platforms\. Some components of WebAuthn support may be varied, such as platform authenticator support across macOS and iOS browsers\. If users attempt to register WebAuthn devices on an unsupported browser or platform, they will see certain options greyed out that are not supported, or they will receive an error that all supported methods are not supported\. In these cases, please refer to [FIDO2: Web Authentication \(WebAuthn\)](https://fidoalliance.org/fido2/fido2-web-authentication-webauthn/) for more information about browser/platform support\. For more information about WebAuthn in AWS SSO, see [Security keys and built\-in authenticators](mfa-types-keys.md)\.

## Active Directory “Domain Users” group does not properly sync into AWS SSO<a name="issue11"></a>

The Active Directory Domain Users group is the default “primary group” for AD user objects\. Active Directory primary groups and their memberships cannot be read by AWS SSO\. When assigning access to AWS SSO resources or applications, use groups other than the Domain Users group \(or other groups assigned as primary groups\) to have group membership properly reflected in the AWS SSO identity store\.

## Invalid MFA credentials error<a name="issue12"></a>

This error can occur when a user attempts to sign in to AWS SSO using an account from an external identity provider \(for example, Okta or Azure AD\) before their user account has been fully provisioned to AWS SSO using the SCIM protocol\. Once the user account has been provisioned to AWS SSO, this issue should be resolved\. Confirm that the user account has been provisioned to AWS SSO and, if not, check the provisioning logs in the external identity provider\.

## I get a 'An unexpected error has occurred' message when I attempt to register or sign in using an authenticator app<a name="issue13"></a>

Time\-based one\-time password \(TOTP\) systems, such as those used by AWS SSO in combination with code\-based authenticator apps, rely on time synchronization between the client and the server\. Ensure that the device where your authenticator app is installed is correctly synchronized to a reliable time source, or manually set the time on your device to match a reliable source, such as NIST \([https://www\.time\.gov/](https://www.time.gov/)\) or other local/regional equivalents\.

## My users are not receiving emails from AWS SSO<a name="issue14"></a>

All emails sent by the AWS SSO service will come from either the address [no-reply@signin.aws](no-reply@signin.aws) or [no-reply@login.awsapps.com](no-reply@login.awsapps.com)\. Your mail system must be configured so that it accepts emails from these sender email addresses and does not handle them as junk or spam\.
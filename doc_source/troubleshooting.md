# Troubleshooting AWS SSO Issues<a name="troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter while setting up or using the AWS SSO console\.

## I cannot get my cloud application configured correctly<a name="issue1"></a>

Each service provider of a preintegrated cloud application in AWS SSO has its own detailed instruction manual\. You can access the manual from the **Configuration** tab for that application in the AWS SSO console\.

If the problem is related to setting up the trust between the service provider's application and AWS SSO, make sure to check the instruction manual for troubleshooting steps\.

## I don't know what data is in my SAML assertion that would be passed to the service provider<a name="issue2"></a>

Use the following steps in the user portal to view what data in the SAML assertion will be sent to the application's service provider for the currently signed\-in user\. This procedure displays the contents in the browser window before sending it to the provider\.

1. While you are signed into the portal, hold the **Shift** key and then choose the application\.

1. Examine the information on the page titled **You are now in administrator mode**\. 

1. If the information looks good, you can choose **Send to <application>** to send the assertion to the service provider and review the outcome of the response\.

## Users can’t sign in when their user name is in UPN format<a name="issue3"></a>

Users might not be able to sign in to the user portal based on the format they use to enter in their user name on the sign in page\. For the most part, users can sign in to the user portal using either their plain user name, their down\-level logon name \(DOMAIN\\UserName\) or their UPN logon name \([UserName@Corp\.Example\.com](mailto:UserName@Corp.Example.com)\)\. The exception to this is when AWS SSO is using a connected directory that has been enabled with MFA and the verification mode has been set to either **Context\-aware** or **Always\-on**\. In this scenario, users must sign in with their down\-level logon name \(DOMAIN\\UserName\)\. For more information, see [Enable Multi\-Factor Authentication](enable-mfa.md)\. For general information about user name formats used to sign in to Active Directory, see [User Name Formats](https://docs.microsoft.com/en-us/windows/desktop/secauthn/user-name-formats) on the Microsoft documentation website\.

## I get a ‘Cannot perform the operation on the protected role' error when modifying an IAM role<a name="issue4"></a>

When reviewing IAM Roles in an account, you may notice role names beginning with ‘AWSReservedSSO\_’\. These are the roles which the AWS SSO service has created in the account, and they came from assigning a permission set to the account\. Attempting to modify these roles from within the IAM console will result in the following error:

```
'Cannot perform the operation on the protected role 'AWSReservedSSO_RoleName_Here' - this role is only modifiable by AWS'
```

These roles can only be modified from the AWS SSO Administrator console, which is in the master account of AWS Organizations\. Once modified, you can then push the changes down to the AWS accounts that it is assigned to\.

## Directory users cannot reset their password<a name="issue5"></a>

When a directory user resets their password using the **Forgot Password?** option during sign\-in of the user portal, their new password must adhere to the default password policy as described in [Password Requirements for the AWS SSO Identity Store](password-requirements.md)\. 

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

This issue can occur if you’re using System for Cross\-domain Identity Management \(SCIM\) for Automatic Provisioning with an external identity provider\. Specifically, when a user, or the group the user was a member of, is deleted then re\-created using the same username \(for users\) or name \(for groups\) in the identity provider, a new unique internal identifier is created for the new user or group in AWS SSO\. However, AWS SSO still has a reference to the old identifier in its permission database, such that the name of the user or group still appears in the UI, but access fails\. This is because the underlying user or group ID to which the UI refers no longer exists\.

To restore AWS account access in this case, you can remove access for the old user or group from the AWS account\(s\) where it was originally assigned, and then reassign access back to the user or group\. This updates the permission set with the correct identifier for the new user or group\. Similarly, to restore application access, you can remove access for the user or group from the assigned users list for that application, then add the user or group back again\.

You can also check to see if AWS CloudTrail recorded the failure by searching your CloudTrail logs for SCIM synchronization events that reference the name of the user or group in question\.

## Error 'An unexpected error has occurred' when an SSO user tries to sign in using an external identity provider<a name="issue7"></a>

This error may occur for multiple reasons, but one common reason is a mis\-match between the user information carried in the SAML request, and the information for the user in AWS SSO\.

In order for an AWS SSO user to sign in successfully when using an external IdP as the identity source, the following must be true:
+ The SAML nameID format \(configured at your identity provider\) must be ‘email’
+ The nameID value must be a properly \(RFC2822\)\-formatted string \(user@domain\.com\)
+ The nameID value must exactly match the username of an existing user in AWS SSO \(it doesn’t matter if the email address in AWS SSO matches or not – the inbound match is based on username\)

Note that AWS SSO does not perform “just in time” creation of users or groups for new users or groups via SAML federation\. This means that the user must be pre\-created in AWS SSO, either manually or via automatic provisioning, in order to sign in to AWS SSO\.
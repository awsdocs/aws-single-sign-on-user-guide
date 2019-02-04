# Troubleshooting AWS SSO Issues<a name="troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter while setting up or using the AWS SSO console\.

## Users can’t sign in when their user name is in UPN format<a name="issue3.title"></a>

Users might not be able to sign in to the user portal based on the format they use to enter in their user name on the sign in page\. For the most part, users can sign in to the user portal using either their plain user name, their down\-level logon name \(DOMAIN\\UserName\) or their UPN logon name \([UserName@Corp\.Example\.com](mailto:UserName@Corp.Example.com)\)\. The exception to this is when AWS SSO is using a connected directory that has been enabled with two\-step verification and the verification mode has been set to either **Context\-aware** or **Always\-on** \. In this scenario, users must sign in with their down\-level logon name \(DOMAIN\\UserName\)\. For more information, see [Verification Modes](http://nickpi.aka.corp.amazon.com/docs/Peregrine/mfa/enable-two-step-verification.html#two-step-modes)\. For general information about user name formats used to sign in to Active Directory, see [User Name Formats](https://docs.microsoft.com/en-us/windows/desktop/secauthn/user-name-formats) on the Microsoft documentation website\.

## I cannot get my cloud application configured correctly<a name="issue1"></a>

Each service provider of a preintegrated cloud application in AWS SSO has its own detailed instruction manual\. You can access the manual from the **Configuration** tab for that application in the AWS SSO console\.

If the problem is related to setting up the trust between the service provider's application and AWS SSO, make sure to check the instruction manual for troubleshooting steps\.

## I don't know what data is in my SAML assertion that would be passed to the service provider<a name="issue2"></a>

Use the following steps in the user portal to view what data in the SAML assertion will be sent to the application's service provider for the currently signed\-in user\. This procedure displays the contents in the browser window before sending it to the provider\.

1. While you are signed into the portal, hold the **Shift** key and then choose the application\.

1. Examine the information on the page titled **You are now in administrator mode**\. 

1. If the information looks good, you can choose **Send to <application>** to send the assertion to the service provider and review the outcome of the response\.
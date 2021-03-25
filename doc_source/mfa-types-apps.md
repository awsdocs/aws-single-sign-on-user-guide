# Authenticator apps<a name="mfa-types-apps"></a>

Authenticator apps are essentially one\-time password \(OTP\)–based third party\-authenticators\. Users can use an authenticator application installed on their mobile device or tablet as an authorized MFA device\. The third\-party authenticator application must be compliant with RFC 6238, which is a standards\-based TOTP \(time\-based one\-time password\) algorithm capable of generating six\-digit authentication codes\. 

When prompted for MFA, users must enter a valid code from their authenticator app within the input box presented\. Each MFA device assigned to a user must be unique\. Two authenticator apps can be registered for any given user\.

## Tested authenticator apps<a name="mfa-types-apps-tested"></a>

Although any TOTP\-compliant application will work with AWS SSO MFA, the following table lists well\-known third\-party authenticator apps to choose from\.


| Operating system | Tested authenticator app | 
| --- | --- | 
| Android | [Authy](https://play.google.com/store/apps/details?id=com.authy.authy), [Duo Mobile](https://play.google.com/store/apps/details?id=com.duosecurity.duomobile), [LastPass Authenticator](https://play.google.com/store/apps/details?id=com.lastpass.authenticator), [Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator), [Google Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2) | 
| iOS | [Authy](https://apps.apple.com/us/app/authy/id494168017), [Duo Mobile](https://apps.apple.com/us/app/duo-mobile/id422663827), [LastPass Authenticator](https://apps.apple.com/us/app/lastpass-authenticator/id1079110004), [Microsoft Authenticator](https://apps.apple.com/us/app/microsoft-authenticator/id983156458), [Google Authenticator](https://apps.apple.com/us/app/google-authenticator/id388497605) | 
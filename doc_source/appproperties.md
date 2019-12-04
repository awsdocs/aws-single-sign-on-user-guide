# Application Properties<a name="appproperties"></a>

In AWS SSO you can customize the user experience by configuring the following additional application properties\. 

## Application Start URL<a name="starturl"></a>

You use an application start URL to start the federation process with your application\. The typical use is for an application that supports only service provider \(SP\)\-initiated binding\.

The following steps and diagram illustrate the application start URL authentication workflow when a user chooses an application in the user portal:

1. The user’s browser redirects the authentication request using the value for the application start URL \(in this case https://example\.com\)\.

1. The application sends an `HTML` `POST` with a `SAMLRequest` to AWS SSO\.

1. AWS SSO then sends an `HTML` `POST` with a `SAMLResponse` back to the application\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/singlesignon/latest/userguide/images/app_properties_start_url.png)

## Relay State<a name="relaystate"></a>

During the federation authentication process, the relay state redirects users within the application\. For SAML 2\.0, this value is passed, unmodified, to the application\. After the application properties are configured, AWS SSO sends the relay state value along with a SAML response to the application\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/singlesignon/latest/userguide/images/app_properties_relay_state.png)

## Session Duration<a name="sessionduration"></a>

Session duration is the length of time that the application user sessions are valid for\. For SAML 2\.0, this is used to set the `NotOnOrAfter` date of the SAML assertion's elements; `saml2:SubjectConfirmationData` and `saml2:Conditions`\. 

Session duration can be interpreted by applications in any of the following ways:
+ Applications can use it to determine how long the SAML assertion is valid\. Applications do not consider session duration when deciding the time allowed for the user\. 
+ Applications can use it to determine the maximum time that is allowed for the user's session\. Applications might generate a user session with a shorter duration\. This can happen when the application only supports user sessions with a duration that is shorter than the configured session length\.
+ Applications can use it as the exact duration and might not allow administrators to configure the value\. This can happen when the application only supports a specific session length\.

For more information about how session duration is used, see your specific application’s documentation\.
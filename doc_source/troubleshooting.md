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
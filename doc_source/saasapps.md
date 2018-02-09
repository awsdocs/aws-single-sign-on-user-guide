# Cloud Applications<a name="saasapps"></a>

AWS SSO has built\-in support for commonly used cloud applications, such as Adobe Creative Cloud, AppDynamics, Box, Confluence, Domo, Dropbox, G Suite, GitHub, GoToMeeting, Jira, NewRelic, Office 365, PagerDuty, Salesforce, ServiceNow, Slack, SumoLogic, Tableau, Workplace by Facebook, ZenDesk, and Zoom\.

Most cloud applications come with detailed instructions on how to set up the trust between AWS SSO and the application's service provider\. You can find these instructions on the cloud applications configuration page during the setup process and after the application has been set up\. Once the application has been configured, you can then assign access to the groups or users that require it\.

## Add and Configure a Cloud Application<a name="addconfigsaasapp"></a>

Use this procedure when you need to set up a SAML trust relationship between AWS SSO and your cloud application's service provider\. Before you begin this procedure, make sure you have the service provider's metadata exchange file so that you can more efficiently set up the trust\. If you do not have this file, you can still use this procedure to configure it manually\.

**To add and configure a cloud application**

1. In the AWS SSO console, choose **Applications** in the left nav, and then choose **Add a new application**\.

1. In the **Select an application** dialog box, select the application you want to add from the list, and then choose **Add**\. 

1. On the **Configure <application name>** page, under **Details**, type a **Display name** for the application\. For example, **Salesforce**\.

1. Under **AWS SSO metadata**, do the following:

   1. Next to **AWS SSO SAML metadata****file**, choose **Download** to download the identity provider metadata\.

   1. Next to **AWS SSO certificate**, choose **Download certificate** to download the identity provider certificate\.
**Note**  
You will need these files later when you set up the cloud application from the service provider's website\. Follow the instructions from that provider\. 

1. Under **Application metadata**, next to **Application certificate**, choose **Browse** to upload the service provider's certificate\. This certificate is required to establish a secure connection between AWS SSO and the service provider\.

1. Choose **Save changes** to save the configuration\.
# Cloud Applications<a name="saasapps"></a>

You can use the AWS SSO application configuration wizard to include built\-in SAML integrations to many popular cloud applications, such as Salesforce, Box, and Office 365\. For a complete list of applications that you can add from the wizard, see [Supported Applications](#saasapps-supported)\.

Most cloud applications come with detailed instructions on how to set up the trust between AWS SSO and the application's service provider\. You can find these instructions on the cloud applications configuration page during the setup process and after the application has been set up\. Once the application has been configured, you can then assign access to the groups or users that require it\.

## Supported Applications<a name="saasapps-supported"></a>

AWS SSO has built\-in support for the following commonly used cloud applications\.


****  

|  |  |  |  | 
| --- |--- |--- |--- |
|  Adobe Creative Cloud  | DruvalnSync | NewRelic | Syncplicity | 
|  AppDynamics  | Egnyte | Office 365 | Tableau | 
| BambooHR | Engagedly | OpsGenie | TalentLMS | 
| Bonusly | Expensify | PagerDuty | Trello | 
| Box | Freshdesk | ProdPad | UserEcho | 
| Citrix ShareFile | G Suite | PurelyHR | UserVoice | 
| ClickTime | GitHub | Salesforce | WeekDone | 
| Convo | GoToMeeting | Samanage | Workplace by Facebook | 
| Deputy | IdeaScale | ScreenSteps | ZenDesk | 
| Deskpro | Igloo | ServiceNow | Zoho | 
| DigiCert | Jitbit | Slack | Zoom | 
| DocuSign | Keeper Security | Sli\.do | 4me | 
| Dome9 | Kudos | SmartSheet |  | 
| Domo | LiquidFiles | SugarCRM |  | 
| Dropbox | Lucidchart | SumoLogic |  | 

## Add and Configure a Cloud Application<a name="saasapps-addconfigapp"></a>

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
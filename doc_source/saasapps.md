# Cloud Applications<a name="saasapps"></a>

You can use the AWS SSO application configuration wizard to include built\-in SAML integrations to many popular cloud applications, such as Salesforce, Box, and Office 365\. For a complete list of applications that you can add from the wizard, see [Supported Applications](#saasapps-supported)\.

Most cloud applications come with detailed instructions on how to set up the trust between AWS SSO and the application's service provider\. You can find these instructions on the cloud applications configuration page during the setup process and after the application has been set up\. Once the application has been configured, you can then assign access to the groups or users that require it\.

## Supported Applications<a name="saasapps-supported"></a>

AWS SSO has built\-in support for the following commonly used cloud applications\.


****  

|  |  |  |  | 
| --- |--- |--- |--- |
| Adobe Creative Cloud | Dropbox | Lucidchart | UserEcho | 
| Aha | DruvalnSync | MangoApps | UserVoice | 
| AnswerHub | EduBrite | NewRelic | Velpic | 
| AppDynamics | Egnyte | Office 365 | VictorOps | 
| Assembla | eLeaP | OpsGenie | WeekDone | 
| Atlassian | Engagedly | PagerDuty | WhosOnLocation | 
| BambooHR | Envoy | Panopta | Workplace by Facebook | 
| BenSelect | Evernote | ProdPad | Workstars | 
| Bitglass | Expensify | PurelyHR | xMatters | 
| BMCRemedyforce | EZOfficeInventory | RingCentral | Zendesk | 
| Bonusly | Freshdesk | Salesforce | Zoho | 
| Box | FreshService | Samanage | Zoom | 
| BugSnag | Front | ScaleFT |  | 
| CakeHR | G Suite | ScreenSteps |  | 
| CiscoMeraki | GitHub | ServiceNow |  | 
| CiscoUmbrella | GitLab | Slack |  | 
| Citrix ShareFile | GoToMeeting | Sli\.do |  | 
| Clarizen | Grovo | Smartsheet |  | 
| ClickTime | Humanity | SnapEngage |  | 
| CloudPassage | IdeaScale | SugarCRM |  | 
| Convo | Igloo | SumoLogic |  | 
| DataDog | JamaSoftware | SurveyMonkey |  | 
| Deputy | JFrog Artifactory | Syncplicity |  | 
| Deskpro | Jitbit | Tableau |  | 
| DigiCert | join\.me | TalentLMS |  | 
| Dmarcian | Keeper Security | TargetProcess |  | 
| Docebo | Klipfolio | TextMagic |  | 
| DocuSign | Kudos | ThousandEyes |  | 
| Dome9 | LiquidFiles | TitanFile |  | 
| Domo | LogMeInRescue | Trello |  | 

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

1. Under **Application properties**, you can optionally specify additional properties for the **Application start URL**, **Relay State**, and **Session Duration**\. For more information, see [Application Properties](appproperties.md)\.

1. Under **Application metadata**, provide the **Application ACS URL** and **Application SAML audience** values\.

1. Choose **Save changes** to save the configuration\.
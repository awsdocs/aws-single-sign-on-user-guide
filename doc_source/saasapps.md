# Cloud Applications<a name="saasapps"></a>

You can use the AWS SSO application configuration wizard to include built\-in SAML integrations to many popular cloud applications\. Examples include Salesforce, Box, and Office 365\. For a complete list of applications that you can add from the wizard, see [Supported Applications](#saasapps-supported)\.

Most cloud applications come with detailed instructions on how to set up the trust between AWS SSO and the application's service provider\. You can find these instructions on the cloud applications configuration page during the setup process and after the application has been set up\. After the application has been configured, you can assign access to the groups or users that require it\.

## Supported Applications<a name="saasapps-supported"></a>

AWS SSO has built\-in support for the following commonly used cloud applications\.

**Note**  
AWS Support engineers can assist customers who have Business and Enterprise support plans with some integration tasks that involve third\-party software\. For a current list of supported platforms and applications, see [Third\-Party Software Support](https://aws.amazon.com/premiumsupport/faqs/#what3rdParty) on the *AWS Support Features* page\.


|  |  |  |  |  | 
| --- |--- |--- |--- |--- |
| 10000ft | Deputy | Heap | Peakon | TalentLMS | 
| 4me | Deskpro | Help Scout | Pipedrive | Targetprocess | 
| 7Geese | Deskradar | Honey | Pivotal Tracker | TextMagic | 
| Accredible | DigiCert | Hosted Graphite | ProdPad | ThousandEyes | 
| Adobe Creative Cloud | dmarcian | Humanity | Proto\.io | Tinfoil Security | 
| Aha | Docebo | IdeaScale | Proxyclick | TitanFile | 
| AlertOps | DocuSign | Igloo | PurelyHR | Trakdesk | 
| AnswerHub | Dome9 | Image Relay | Recognize | Trello | 
| AppDynamics | Domo | iSpring | RescueAssist | Uptime | 
| AppFollow | Drift | IT Glue | RingCentral | Uptrends | 
| Asana | Dropbox | Jama Software | Robin | UserEcho | 
| Assembla | Druva inSync | JFrog Artifactory | Rollbar | UserVoice | 
| Atlassian | Duo | Jira | Salesforce | Velpic | 
| BambooHR | EduBrite | Jitbit | Samanage | VictorOps | 
| BenSelect | Egnyte | join\.me | ScaleFT | Vtiger | 
| BitaBIZ | eLeaP | Kanbanize | ScreenSteps | Way We Do | 
| Bitglass | Engagedly | Keeper Security | ServiceNow | Weekdone | 
| BlueJeans | Envoy | Kintone | Slack | WhosOnLocation | 
| BMC Remedyforce | Evernote | Klipfolio | Slemma | Workplace by Facebook | 
| Bonusly | Expensify | KnowledgeOwl | Sli\.do | Workstars | 
| Box | Expiration Reminder | Kudos | Small Improvements | Wrike | 
| Bugsnag | EZOfficeInventory | LiquidFiles | Smartsheet | xMatters | 
| Buildkite | EZRentOut | LiquidPlanner | SnapEngage | Yodeck | 
| CakeHR | Fastly | Litmos | Split\.io | Zendesk | 
| Chartio | Flock | LiveChat | Spotinst | Ziflow | 
| Circonus | Formstack | LogMeInRescue | SproutVideo | Zillable | 
| Cisco Webex | Freshdesk | Lucidchart | Stackify | Zoho | 
| Cisco Meraki | Freshservice | ManageEngine | Status Hero | Zoom | 
| Cisco Umbrella | Front | MangoApps | StatusCast |  | 
| Citrix ShareFile | G Suite | Miro | StatusDashboard |  | 
| Clarizen | Github | MockFlow | StatusHub |  | 
| ClickTime | Gitlab | New Relic | Statuspage |  | 
| CloudAMQP | Glasscubes | Nuclino | StoriesOnBoard |  | 
| CloudPassage | GorillaStack | Office 365 | Stormboard |  | 
| CMNTY | GoToMeeting | Opsgenie | SugarCRM |  | 
| Confluence | GoToTraining | Pacific Timesheet | Sumo Logic |  | 
| Convo | GoToWebinar | PagerDuty | SurveyGizmo |  | 
| Coralogix | Grovo | Panopta | SurveyMonkey |  | 
| Datadog | HackerOne | Panorama9 | Syncplicity |  | 
| Declaree | HackerRank | ParkMyCloud | Tableau |  | 

## Add and Configure a Cloud Application<a name="saasapps-addconfigapp"></a>

Use this procedure when you need to set up a SAML trust relationship between AWS SSO and your cloud application's service provider\. Before you begin this procedure, make sure you have the service provider's metadata exchange file so that you can more efficiently set up the trust\. If you do not have this file, you can still use this procedure to configure it manually\.

**To add and configure a cloud application**

1. In the AWS SSO console, choose **Applications** in the left navigation pane\. Then choose **Add a new application**\.

1. In the **Select an application** dialog box, select the application you want to add from the list\. Then choose **Add**\. 

1. On the **Configure <application name>** page, under **Details**, type a **Display name** for the application, such as **Salesforce**\.

1. Under **AWS SSO metadata**, do the following:

   1. Next to **AWS SSO SAML metadata****file**, choose **Download** to download the identity provider metadata\.

   1. Next to **AWS SSO certificate**, choose **Download certificate** to download the identity provider certificate\.
**Note**  
You will need these files later when you set up the cloud application from the service provider's website\. Follow the instructions from that provider\. 

1. \(Optional\) Under **Application properties**, you can specify additional properties for the **Application start URL**, **Relay State**, and **Session Duration**\. For more information, see [Application Properties](appproperties.md)\.

1. Under **Application metadata**, provide the **Application ACS URL** and **Application SAML audience** values\.

1. Choose **Save changes** to save the configuration\.
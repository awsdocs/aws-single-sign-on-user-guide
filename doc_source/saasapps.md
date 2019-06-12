# Cloud Applications<a name="saasapps"></a>

You can use the AWS SSO application configuration wizard to include built\-in SAML integrations to many popular cloud applications\. Examples include Salesforce, Box, and Office 365\. For a complete list of applications that you can add from the wizard, see [Supported Applications](#saasapps-supported)\.

Most cloud applications come with detailed instructions on how to set up the trust between AWS SSO and the application's service provider\. You can find these instructions on the cloud applications configuration page during the setup process and after the application has been set up\. After the application has been configured, you can assign access to the groups or users that require it\.

## Supported Applications<a name="saasapps-supported"></a>

AWS SSO has built\-in support for the following commonly used cloud applications\.

**Note**  
AWS Support engineers can assist customers who have Business and Enterprise support plans with some integration tasks that involve third\-party software\. For a current list of supported platforms and applications, see [Third\-Party Software Support](https://aws.amazon.com/premiumsupport/faqs/#what3rdParty) on the *AWS Support Features* page\.


|  |  |  |  |  | 
| --- |--- |--- |--- |--- |
| 10000ft | DigiCert | Image Relay | Robin | Vtiger | 
| 4me | dmarcian | iSpring | Rollbar | Way We Do | 
| 7Geese | Docebo | IT Glue | Room Booking System | Weekdone | 
| Accredible | DocuSign | Jama Software | Salesforce | WhosOnLocation | 
| Adobe Creative Cloud | Dome9 | Jamf | Samanage | Workplace by Facebook | 
| Aha | Domo | JFrog Artifactory | ScaleFT | Workstars | 
| AlertOps | Drift | Jira | ScreenSteps | Wrike | 
| AnswerHub | Dropbox | Jitbit | ServiceNow | xMatters | 
| AppDynamics | Druva inSync | join\.me | Slack | Yodeck | 
| AppFollow | Duo | Kanbanize | Slemma | Zendesk | 
| Asana | EduBrite | Keeper Security | Sli\.do | Ziflow | 
| Assembla | Egnyte | Kintone | Small Improvements | Zillable | 
| Atlassian | eLeaP | Klipfolio | Smartsheet | Zoho | 
| BambooHR | Engagedly | KnowledgeOwl | SnapEngage | Zoom | 
| BenSelect | Envoy | Kudos | Split\.io |  | 
| BitaBIZ | Evernote | LiquidFiles | Spotinst |  | 
| Bitglass | Expensify | LiquidPlanner | SproutVideo |  | 
| BlueJeans | Expiration Reminder | Litmos | Stackify |  | 
| BMC Remedyforce | EZOfficeInventory | LiveChat | Status Hero |  | 
| Bonusly | EZRentOut | LogMeInRescue | StatusCast |  | 
| Box | Fastly | Lucidchart | StatusDashboard |  | 
| Breezy HR | FileCloud Online | ManageEngine | StatusHub |  | 
| Buddy Punch | Flock | MangoApps | Statuspage |  | 
| Bugsnag | Formstack | Miro | StoriesOnBoard |  | 
| Buildkite | Freshdesk | MockFlow | Stormboard |  | 
| CakeHR | Freshservice | New Relic | SugarCRM |  | 
| Chartio | Front | Nuclino | Sumo Logic |  | 
| Circonus | G Suite | Office 365 | SurveyGizmo |  | 
| Cisco Webex | Github | Opsgenie | SurveyMonkey |  | 
| Cisco Meraki | Gitlab | Pacific Timesheet | Syncplicity |  | 
| Cisco Umbrella | Glasscubes | PagerDuty | Tableau |  | 
| Citrix ShareFile | GorillaStack | Panopta | TalentLMS |  | 
| Clarizen | GoToMeeting | Panorama9 | Targetprocess |  | 
| ClickTime | GoToTraining | ParkMyCloud | TextMagic |  | 
| CloudAMQP | GoToWebinar | Peakon | ThousandEyes |  | 
| CloudPassage | Grovo | PhraseApp | Tinfoil Security |  | 
| CMNTY | HackerOne | Pipedrive | TitanFile |  | 
| Confluence | HackerRank | Pivotal Tracker | Trakdesk |  | 
| Convo | Heap | ProdPad | Trello |  | 
| Coralogix | Help Scout | Proto\.io | Uptime\.com |  | 
| Datadog | Honey | Proxyclick | Uptrends |  | 
| Declaree | Hosted Graphite | PurelyHR | UserEcho |  | 
| Deputy | Humanity | Recognize | UserVoice |  | 
| Deskpro | IdeaScale | RescueAssist | Velpic |  | 
| Deskradar | Igloo | RingCentral | VictorOps |  | 

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
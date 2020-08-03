# Cloud Applications<a name="saasapps"></a>

You can use the AWS SSO application configuration wizard to include built\-in SAML integrations to many popular cloud applications\. Examples include Salesforce, Box, and Office 365\. For a complete list of applications that you can add from the wizard, see [Supported Applications](#saasapps-supported)\.

Most cloud applications come with detailed instructions on how to set up the trust between AWS SSO and the application's service provider\. You can find these instructions on the cloud applications configuration page during the setup process and after the application has been set up\. After the application has been configured, you can assign access to the groups or users that require it\.

## Supported Applications<a name="saasapps-supported"></a>

AWS SSO has built\-in support for the following commonly used cloud applications\.

**Note**  
AWS Support engineers can assist customers who have Business and Enterprise support plans with some integration tasks that involve third\-party software\. For a current list of supported platforms and applications, see [Third\-Party Software Support](https://aws.amazon.com/premiumsupport/faqs/#what3rdParty) on the *AWS Support Features* page\.


|  |  |  |  |  | 
| --- |--- |--- |--- |--- |
| 10000ft | Cybozu Mailwise | HelloSign | PlanMyLeave | Stackify | 
| 4me | Cybozu Office | Helpdocs\.io | PolicyIQ | Status Hero | 
| 7Geese | Cybozu\.com | HelpScout | ProcessPlan | StatusCast | 
| Abstract | Dashlane | HighGear | ProdPad | StatusDashboard | 
| Accredible | Databricks | Hightail | Proto\.io | StatusHub | 
| Adobe Connect | Datadog | Honey | Proxyclick | Statuspage | 
| Adobe Creative Cloud | Declaree | Honeycomb\.io | PurelyHR | StoriesOnBoard | 
| Adobe Sign | Deputy | HostedGraphite | Quip | Stormboard | 
| Aha | DeskPro | HubSpot | Rapid7 Insight products | SugarCRM | 
| Airbrake | Deskradar | Humanity | Recognize | SumoLogic | 
| AlertOps | Detectify | IdeaScale | Redash\.io | SurveyGizmo | 
| AlertSite | Digicert | Igloo | Redlock | SurveyMonkey | 
| Amazon Business | Dmarcian | ImageRelay | RescueAssist | Syncplicity | 
| Amazon WorkLink | Docebo | iSpring | RingCentral | Tableau | 
| Andfrankly | DocuSign | IT Glue | Roadmunk | Tableau Server | 
| AnswerHub | Dome9 | JamaSoftware | Robin | TalentLMS | 
| AppDynamics | Domo | Jamf | Rollbar | TargetProcess | 
| AppFollow | Drift | Jenkins | Room Booking System | TeamSupport | 
| Area 1 | Dropbox | JFrog Artifactory | Salesforce | Tenable\.io | 
| Asana | DruvaInSync | Jira | Salesforce Service Cloud | TextMagic | 
| Assembla | Duo | Jitbit | Samanage | ThousandEyes | 
| Atlassian | Dynatrace | Jive | SAP BW | TinfoilSecurity | 
| Automox | EduBrite | join\.me | SAP Cloud Platform | TitanFile | 
| BambooHR | Egnyte | Kanbanize | SAP CRM ABAP | TOPdesk Operator | 
| BenSelect | eLeaP | Keeper Security | SAP CRM Java | TOPdesk Self Service Desk | 
| BitaBIZ | Engagedly | Kentik | SAP Enterprise Portal Java | Trakdesk | 
| Bitglass | Envoy | Kintone | SAP ERP ABAP | Trello | 
| BlueJeans | Evernote | Klipfolio | SAP EWM ABAP | Trend Micro Deep Security | 
| BMCRemedyforce | ExpenseIn | KnowledgeOwl | SAP Fiori ABAP | Uptime\.com | 
| Bonusly | Expensify | Kudos | SAP GRC Access Control ABAP | Uptrends | 
| Box | Expiration Reminder | LiquidFiles | SAP LMS | UserEcho | 
| Brandfolder | External AWS Account | LiquidPlanner | SAP Netweaver ABAP | UserVoice | 
| Breezy HR | EZOfficeInventory | Litmos | SAP Netweaver Java | Velpic | 
| Buddy Punch | EZRentOut | LiveChat | SAP S4 ABAP | Veracode | 
| Bugsee | Fastly | LogMeInRescue | SAP Solution Manager ABAP | VictorOps | 
| BugSnag | Federated Directory | Lucidchart | SAP Solution Manager Java | vtiger | 
| Buildkite | FileCloud | ManageEngine | SAP SRM ABAP | WayWeDo | 
| Bynder | FireHydrant | MangoApps | SAP xMII Java | WeekDone | 
| CakeHR | Fivetran | Marketo | ScaleFT | WhosOnLocation | 
| Canvas | Flock | Metricly | Scalyr | Wordbee | 
| Chartio | FogBugz | Miro | ScreenSteps | Workable | 
| Chatwork | Formstack | MockFlow | Seeit | Workfront | 
| Circonus | Fossa | Mode Analytics | Sentry\.io | Workplace by Facebook | 
| Cisco Webex | Freedcamp | MongoDB | ServiceNow | Workstars | 
| CiscoMeraki | Freshdesk | Moodle | SimpleMDM | Wrike | 
| CiscoUmbrella | FreshService | MuleSoft Anypoint | Skeddly | xMatters | 
| CitrixShareFile | Front | MyWebTimeSheets | Skilljar | XperienceHR | 
| Clari | G Suite | N2F Expense Reports | Slack | Yodeck | 
| Clarizen | GitBook | NewRelic | Slemma | Zendesk | 
| ClickTime | Github | Nuclino | Sli\.do | Zephyr | 
| Cloud CMS | GitLab | Office365 | Small Improvements | Ziflow | 
| Cloud Conformity | Glasscubes | OnDMARC | Smartsheet | Zillable | 
| CloudAMQP | GlassFrog | OpenVoice | SnapEngage | Zoho | 
| CloudCheckr | GorillaStack | OpsGenie | Snowflake | Zoho One | 
| CloudEndure | GoToAssist | Pacific Timesheet | SonarQube | Zoom | 
| CloudHealth | GoToMeeting | PagerDuty | SparkPost |  | 
| CloudPassage | GoToTraining | Panopta | Spinnaker |  | 
| CMNTY | GoToWebinar | Panorama9 | Split\.io |  | 
| CoderPad | Grovo | ParkMyCloud | Splunk Cloud |  | 
| Confluence | HackerOne | Peakon | Splunk Enterprise |  | 
| Convo | HackerRank | PhraseApp | Spotinst |  | 
| Coralogix | HappyFox | PipeDrive | SproutVideo |  | 
| Cybozu Garoon | Heap | Pivotal Tracker | Squadcast |  | 

## Add and Configure a Cloud Application<a name="saasapps-addconfigapp"></a>

Use this procedure when you need to set up a SAML trust relationship between AWS SSO and your cloud application's service provider\. Before you begin this procedure, make sure you have the service provider's metadata exchange file so that you can more efficiently set up the trust\. If you do not have this file, you can still use this procedure to configure it manually\.

**To add and configure a cloud application**

1. In the AWS SSO console, choose **Applications** in the left navigation pane\. Then choose **Add a new application**\.

1. In the **Select an application** dialog box, select the application you want to add from the list\. Then choose **Add**\. 

1. On the **Configure <application name>** page, under **Details**, enter a **Display name** for the application, such as **Salesforce**\.

1. Under **AWS SSO metadata**, do the following:

   1. Next to **AWS SSO SAML metadata****file**, choose **Download** to download the identity provider metadata\.

   1. Next to **AWS SSO certificate**, choose **Download certificate** to download the identity provider certificate\.
**Note**  
You will need these files later when you set up the cloud application from the service provider's website\. Follow the instructions from that provider\. 

1. \(Optional\) Under **Application properties**, you can specify additional properties for the **Application start URL**, **Relay State**, and **Session Duration**\. For more information, see [Application Properties](appproperties.md)\.

1. Under **Application metadata**, provide the **Application ACS URL** and **Application SAML audience** values\.

1. Choose **Save changes** to save the configuration\.
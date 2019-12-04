# Cloud Applications<a name="saasapps"></a>

You can use the AWS SSO application configuration wizard to include built\-in SAML integrations to many popular cloud applications\. Examples include Salesforce, Box, and Office 365\. For a complete list of applications that you can add from the wizard, see [Supported Applications](#saasapps-supported)\.

Most cloud applications come with detailed instructions on how to set up the trust between AWS SSO and the application's service provider\. You can find these instructions on the cloud applications configuration page during the setup process and after the application has been set up\. After the application has been configured, you can assign access to the groups or users that require it\.

## Supported Applications<a name="saasapps-supported"></a>

AWS SSO has built\-in support for the following commonly used cloud applications\.

**Note**  
AWS Support engineers can assist customers who have Business and Enterprise support plans with some integration tasks that involve third\-party software\. For a current list of supported platforms and applications, see [Third\-Party Software Support](https://aws.amazon.com/premiumsupport/faqs/#what3rdParty) on the *AWS Support Features* page\.


|  |  |  |  |  | 
| --- |--- |--- |--- |--- |
| 10000ft | Cybozu Mailwise | HappyFox | PhraseApp | Splunk Cloud | 
| 4me | Cybozu Office | Heap | PipeDrive | Splunk Enterprise | 
| 7Geese | Cybozu\.com | HelloSign | Pivotal Tracker | Spotinst | 
| Abstract | Dashlane | Helpdocs\.io | PlanMyLeave | SproutVideo | 
| Accredible | Databricks | HelpScout | PolicyIQ | Squadcast | 
| Adobe Connect | Datadog | HighGear | ProcessPlan | Stackify | 
| Adobe Creative Cloud | Declaree | Hightail | ProdPad | Status Hero | 
| Adobe Sign | Deputy | Honey | Proto\.io | StatusCast | 
| Aha | DeskPro | Honeycomb\.io | Proxyclick | StatusDashboard | 
| Airbrake | Deskradar | HostedGraphite | PurelyHR | StatusHub | 
| AlertOps | Detectify | HubSpot | Quip | Statuspage | 
| AlertSite | Digicert | Humanity | Rapid7 Insight products | StoriesOnBoard | 
| Amazon Business | Dmarcian | IdeaScale | Recognize | Stormboard | 
| Amazon WorkLink | Docebo | Igloo | Redash\.io | SugarCRM | 
| Andfrankly | DocuSign | ImageRelay | Redlock | SumoLogic | 
| AnswerHub | Dome9 | iSpring | RescueAssist | SurveyGizmo | 
| AppDynamics | Domo | IT Glue | RingCentral | SurveyMonkey | 
| AppFollow | Drift | JamaSoftware | Roadmunk | Syncplicity | 
| Area 1 | Dropbox | Jamf | Robin | Tableau | 
| Asana | DruvaInSync | Jenkins | Rollbar | Tableau Server | 
| Assembla | Duo | JFrog Artifactory | Room Booking System | TalentLMS | 
| Atlassian | Dynatrace | Jira | Salesforce | TargetProcess | 
| Automox | EduBrite | Jitbit | Salesforce Service Cloud | TeamSupport | 
| BambooHR | Egnyte | Jive | Samanage | Tenable\.io | 
| BenSelect | eLeaP | join\.me | SAP BW | TextMagic | 
| BitaBIZ | Engagedly | Kanbanize | SAP Cloud Platform | ThousandEyes | 
| Bitglass | Envoy | Keeper Security | SAP CRM ABAP | TinfoilSecurity | 
| BlueJeans | Evernote | Kentik | SAP CRM Java | TitanFile | 
| BMCRemedyforce | ExpenseIn | Kintone | SAP Enterprise Portal Java | TOPdesk Operator | 
| Bonusly | Expensify | Klipfolio | SAP ERP ABAP | TOPdesk Self Service Desk | 
| Box | Expiration Reminder | KnowledgeOwl | SAP EWM ABAP | Trakdesk | 
| Brandfolder | External AWS Account | Kudos | SAP Fiori ABAP | Trello | 
| Breezy HR | EZOfficeInventory | LiquidFiles | SAP GRC Access Control ABAP | Trend Micro Deep Security | 
| Buddy Punch | EZRentOut | LiquidPlanner | SAP LMS | Uptime\.com | 
| Bugsee | Fastly | Litmos | SAP Netweaver ABAP | Uptrends | 
| BugSnag | Federated Directory | LiveChat | SAP Netweaver Java | UserEcho | 
| Buildkite | FileCloud | LogMeInRescue | SAP S4 ABAP | UserVoice | 
| Bynder | FireHydrant | Lucidchart | SAP Solution Manager ABAP | Velpic | 
| CakeHR | Fivetran | ManageEngine | SAP Solution Manager Java | Veracode | 
| Canvas | Flock | MangoApps | SAP SRM ABAP | VictorOps | 
| Chartio | FogBugz | Marketo | SAP xMII Java | vtiger | 
| Chatwork | Formstack | Metricly | ScaleFT | WayWeDo | 
| Circonus | Fossa | Miro | Scalyr | WeekDone | 
| Cisco Webex | Freedcamp | MockFlow | ScreenSteps | WhosOnLocation | 
| CiscoMeraki | Freshdesk | Mode Analytics | Seeit | Wordbee | 
| CiscoUmbrella | FreshService | Moodle | Sentry\.io | Workable | 
| CitrixShareFile | Front | MuleSoft Anypoint | ServiceNow | Workfront | 
| Clarizen | G Suite | MyWebTimeSheets | SimpleMDM | Workplace by Facebook | 
| ClickTime | GitBook | N2F Expense Reports | Skeddly | Workstars | 
| Cloud CMS | Github | NewRelic | Skilljar | Wrike | 
| Cloud Conformity | GitLab | Nuclino | Slack | xMatters | 
| CloudAMQP | Glasscubes | Office365 | Slemma | XperienceHR | 
| CloudCheckr | GlassFrog | OnDMARC | Sli\.do | Yodeck | 
| CloudEndure | GorillaStack | OpenVoice | Small Improvements | Zendesk | 
| CloudPassage | GoToAssist | OpsGenie | Smartsheet | Zephyr | 
| CMNTY | GoToMeeting | Pacific Timesheet | SnapEngage | Ziflow | 
| CoderPad | GoToTraining | PagerDuty | Snowflake | Zillable | 
| Confluence | GoToWebinar | Panopta | SonarQube | Zoho | 
| Convo | Grovo | Panorama9 | SparkPost | Zoho One | 
| Coralogix | HackerOne | ParkMyCloud | Spinnaker | Zoom | 
| Cybozu Garoon | HackerRank | Peakon | Split\.io |  | 

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
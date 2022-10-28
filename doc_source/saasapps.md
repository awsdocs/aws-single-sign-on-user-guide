# Cloud applications<a name="saasapps"></a>

You can use the IAM Identity Center application configuration wizard to include built\-in SAML integrations to many popular cloud applications\. Examples include Salesforce, Box, and Office 365\. For a complete list of applications that you can add from the wizard, see [Supported applications](#saasapps-supported)\.

Most cloud applications come with detailed instructions on how to set up the trust between IAM Identity Center and the application's service provider\. You can find these instructions on the cloud applications configuration page during the setup process and after the application has been set up\. After the application has been configured, you can assign access to the groups or users that require it\.

## Supported applications<a name="saasapps-supported"></a>

IAM Identity Center has built\-in support for the following commonly used cloud applications\.

**Note**  
AWS Support engineers can assist customers who have Business and Enterprise support plans with some integration tasks that involve third\-party software\. For a current list of supported platforms and applications, see [Third\-Party Software Support](https://aws.amazon.com/premiumsupport/faqs/#what3rdParty) on the *AWS Support Features* page\.


|  |  |  |  |  | 
| --- |--- |--- |--- |--- |
| 10000ft | Cybozu Mailwise | Heap | Pivotal Tracker | Squadcast | 
| 4me | Cybozu Office | HelloSign | PlanMyLeave | Stackify | 
| 7Geese | Cybozu\.com | Helpdocs\.io | PolicyIQ | Status Hero | 
| Abstract | Dashlane | HelpScout | ProcessPlan | StatusCast | 
| Accredible | Databricks | HighGear | ProdPad | StatusDashboard | 
| Adobe Connect | Datadog | Hightail | Proto\.io | StatusHub | 
| Adobe Creative Cloud | Declaree | Honey | Proxyclick | Statuspage | 
| Adobe Sign | Deputy | Honeycomb\.io | PurelyHR | StoriesOnBoard | 
| Aha | DeskPro | HostedGraphite | Quip | Stormboard | 
| Airbrake | Deskradar | HubSpot | Rapid7 Insight products | SugarCRM | 
| AlertOps | Detectify | Humanity | Recognize | SumoLogic | 
| AlertSite | Digicert | IdeaScale | Redash\.io | SurveyGizmo | 
| Amazon Business | Dmarcian | Igloo | Redlock | SurveyMonkey | 
| Amazon WorkLink | Docebo | ImageRelay | RescueAssist | Syncplicity | 
| Andfrankly | DocuSign | iSpring | RingCentral | Tableau | 
| AnswerHub | Dome9 | IT Glue | Roadmunk | Tableau Server | 
| AppDynamics | Domo | JamaSoftware | Robin | TalentLMS | 
| AppFollow | Drift | Jamf | Rollbar | TargetProcess | 
| Area 1 | Dropbox | Jenkins | Room Booking System | TeamSupport | 
| Asana | DruvaInSync | JFrog Artifactory | Salesforce | Tenable\.io | 
| Assembla | Duo | Jira | Salesforce Service Cloud | TextMagic | 
| Atlassian | Dynatrace | Jitbit | Samanage | ThousandEyes | 
| Automox | EduBrite | Jive | SAP BW | TinfoilSecurity | 
| BambooHR | Egnyte | join\.me | SAP Cloud Platform | TitanFile | 
| BenSelect | eLeaP | Kanbanize | SAP CRM ABAP | TOPdesk Operator | 
| BitaBIZ | Engagedly | Keeper Security | SAP CRM Java | TOPdesk Self Service Desk | 
| Bitglass | Envoy | Kentik | SAP Enterprise Portal Java | Trakdesk | 
| BlueJeans | Evernote | Kintone | SAP ERP ABAP | Trello | 
| BMCRemedyforce | ExpenseIn | Klipfolio | SAP EWM ABAP | Trend Micro Deep Security | 
| Bonusly | Expensify | KnowledgeOwl | SAP Fiori ABAP | Uptime\.com | 
| Box | Expiration Reminder | Kudos | SAP GRC Access Control ABAP | Uptrends | 
| Brandfolder | External AWS Account | LiquidFiles | SAP LMS | UserEcho | 
| Breezy HR | EZOfficeInventory | LiquidPlanner | SAP Netweaver ABAP | UserVoice | 
| Buddy Punch | EZRentOut | Litmos | SAP Netweaver Java | Velpic | 
| Bugsee | Fastly | LiveChat | SAP S4 ABAP | Veracode | 
| BugSnag | Federated Directory | LogMeInRescue | SAP Solution Manager ABAP | VictorOps | 
| Buildkite | FileCloud | Lucidchart | SAP Solution Manager Java | vtiger | 
| Bynder | FireHydrant | ManageEngine | SAP SRM ABAP | WayWeDo | 
| CakeHR | Fivetran | MangoApps | SAP xMII Java | WeekDone | 
| Canvas | Flock | Marketo | ScaleFT | WhosOnLocation | 
| Chartio | FogBugz | Metricly | Scalyr | Wordbee | 
| Chatwork | Formstack | Miro | ScreenSteps | Workable | 
| Circonus | Fossa | MockFlow | Seeit | Workfront | 
| Cisco Webex | Freedcamp | Mode Analytics | Sentry\.io | Workplace by Facebook | 
| CiscoMeraki | Freshdesk | MongoDB | ServiceNow | Workstars | 
| CiscoUmbrella | FreshService | Moodle | SimpleMDM | Wrike | 
| CitrixShareFile | Front | MuleSoft Anypoint | Skeddly | xMatters | 
| Clari | G Suite | MyWebTimeSheets | Skilljar | XperienceHR | 
| Clarizen | Genesys Cloud | N2F Expense Reports | Slack | Yodeck | 
| ClickTime | GitBook | NewRelic | Slemma | Zendesk | 
| Cloud CMS | Github | Nuclino | Sli\.do | Zephyr | 
| Cloud Conformity | GitLab | Office365 | Small Improvements | Ziflow | 
| CloudAMQP | Glasscubes | OnDMARC | Smartsheet | Zillable | 
| CloudCheckr | GlassFrog | OpenVoice | SnapEngage | Zoho | 
| CloudEndure | GorillaStack | OpsGenie | Snowflake | Zoho One | 
| CloudHealth | GoToAssist | Pacific Timesheet | SonarQube | Zoom | 
| CloudPassage | GoToMeeting | PagerDuty | SparkPost |  | 
| CMNTY | GoToTraining | Panopta | Spinnaker |  | 
| CoderPad | GoToWebinar | Panorama9 | Split\.io |  | 
| Confluence | Grovo | ParkMyCloud | Splunk Cloud |  | 
| Convo | HackerOne | Peakon | Splunk Enterprise |  | 
| Coralogix | HackerRank | PhraseApp | Spotinst |  | 
| Cybozu Garoon | HappyFox | PipeDrive | SproutVideo |  | 

## Add and configure a cloud application<a name="saasapps-addconfigapp"></a>

Use this procedure when you need to set up a SAML trust relationship between IAM Identity Center and your cloud application's service provider\. Before you begin this procedure, make sure you have the service provider's metadata exchange file so that you can more efficiently set up the trust\. If you do not have this file, you can still use this procedure to configure it manually\.

**To add and configure a cloud application**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. Choose **Add application**\.

1. Under **Applications**, search for an application, and select the application from the list\. Choose **Next**\.

1. Under **Configure application**, the **Display name** and **Description** pre\-populates with the application you chose\. You can edit these\.

1. Under **IAM Identity Center metadata**, do the following:

   1. Under **IAM Identity Center SAML metadata file**, choose **Download** to download the identity provider metadata\.

   1. Under **IAM Identity Center certificate**, choose **Download certificate** to download the identity provider certificate\.
**Note**  
You will need these files later when you set up the cloud application from the service provider's website\. Follow the instructions from that provider\. 

1. \(Optional\) Under **Application properties**, you can specify additional properties for the **Application start URL**, **Relay state**, and **Session duration**\. For more information, see [Application properties](appproperties.md)\.

1. Under **Application metadata**, do one of the following: 

   1. Choose **Upload application SAML metadata file**\. Then, select **Choose file** to find and select the metadata file\.

   1. If you do not have a metadata file, choose **Manually type your metadata values**, and then provide the **Application ACS URL** and **Application SAML audience** values\.

1. Choose **Submit**\. You're taken to the details page of the application that you just added\.
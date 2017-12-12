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

## Assign Access to Users or Groups<a name="assignuserstoapp"></a>

Use the following procedure to assign SSO access to users and groups in your connected directory\.

**Note**  
To help simplify administration of access permissions, we recommended that you assign access directly to groups rather than to individual users\. With groups you can grant or deny permissions to groups of users, rather than having to apply those permissions to each individual\. If a user moves to a different organization, you simply move that user to a different group and they automatically receive the permissions that are needed for the new organization\.

**To assign access to users or groups**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the AWS SSO console is using the US East \(N\. Virginia\) \(us\-east\-1\) Region where your AWS Microsoft AD directory is located before you move to the next step\.

1. Choose **Applications**\.

1. In the list of applications, choose an application to which you want to assign access\. 

1. On the application details page, select the **Assigned users** tab\. Then choose **Assign users**\.

1. In the **Assign users** dialog box, type a user or group name\. Then choose **Search connected directory**\. You can specify multiple users or groups by selecting the applicable accounts as they appear in search results\. 

1. Choose **Assign users**\.

## Remove User Access<a name="removeaccessfromapp"></a>

Use this procedure to remove SSO application access from a particular user or group in your connected directory\.

**To remove user access from an application**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. In the list of applications, choose an application whose access you want to remove\. 

1. On the application details page, select the **Assigned users** tab, select the user or group you want to remove, and then choose **Remove**\.

1. In the **Remove access** dialog box, verify the user or group name\. Then choose **Yes, remove access**\. 

## Map AWS SSO Attributes to Attributes in Your Application \(Optional\)<a name="mapawsssoattributestoapp"></a>

Some service providers require custom SAML assertions to pass additional data about your user sign\-ins\. In that case, use the following procedure to specify how your applications user attributes should map to corresponding attributes in your connected directory\.

**To map application attributes to attributes in your connected directory**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Connected directory**\.

1. Under **Attribute Mappings**, choose **Edit attribute mappings**\.

1. On the **Attribute Mappings** page, find the application attribute that you want to map\. Then type a value in the text box\.
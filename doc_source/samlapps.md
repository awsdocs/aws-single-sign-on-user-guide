# Custom SAML 2\.0 Applications<a name="samlapps"></a>

You can use the AWS SSO application configuration wizard to add support for applications that allow identity federation using Security Assertion Markup Language \(SAML\) 2\.0\. In the console, you set these up by choosing **Custom SAML 2\.0 application** from the application selector\. Most of the steps for configuring a custom SAML application are the same as configuring a cloud application\. 

However, you also need to provide additional SAML attribute mappings for a custom SAML application\. These mappings tell AWS SSO how to populate the SAML assertion correctly for your application\. You can provide this additional SAML attribute mapping when you set up the application for the first time\. You can also provide SAML attribute mappings on the application detail page that is accessible from the AWS SSO console\.

## Add and Configure a Custom SAML 2\.0 Application<a name="addconfigcustomapp"></a>

Use this procedure when you need to set up a SAML trust relationship between AWS SSO and your custom application's service provider\. Before you begin this procedure, make sure that you have the service provider's certificate and metadata exchange files so that you can finish setting up the trust\.

**To add and configure a custom SAML application**

1.  In the AWS SSO console, choose **Applications** in the left navigation pane\. Then choose **Add a new application**\.

1. In the **Select an application** dialog box, select **Custom SAML 2\.0 application** from the list\. Then choose **Configure application**\. 

1. On the **Configure <Custom app name>** page, under **Details**, enter a **Display name** for the application, such as **MyApp**\.

1. Under **AWS SSO metadata**, do the following:

   1. Next to **AWS SSO SAML metadata****file**, choose **Download** to download the identity provider metadata\.

   1. Next to **AWS SSO certificate**, choose **Download certificate** to download the identity provider certificate\.
**Note**  
You will need these files later when you set up the custom application from the service provider's website\. 

1. \(Optional\) Under **Application properties**, you can specify additional properties for the **Application start URL**, **Relay State**, and **Session Duration**\. For more information, see [Application Properties](appproperties.md)\.

1. Under **Application metadata**, provide the **Application ACS URL** and **Application SAML audience** values\.

1. Choose **Save changes** to save the configuration\.
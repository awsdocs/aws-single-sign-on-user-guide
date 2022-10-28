# Custom SAML 2\.0 applications<a name="samlapps"></a>

You can use the IAM Identity Center application configuration wizard to add support for applications that allow identity federation using Security Assertion Markup Language \(SAML\) 2\.0\. In the console, you set these up by choosing **Custom SAML 2\.0 application** from the application selector\. Most of the steps for configuring a custom SAML application are the same as configuring a cloud application\. 

However, you also need to provide additional SAML attribute mappings for a custom SAML application\. These mappings tell IAM Identity Center how to populate the SAML assertion correctly for your application\. You can provide this additional SAML attribute mapping when you set up the application for the first time\. You can also provide SAML attribute mappings on the application detail page that is accessible from the IAM Identity Center console\.

## Add and configure a custom SAML 2\.0 application<a name="addconfigcustomapp"></a>

Use this procedure when you need to set up a SAML trust relationship between IAM Identity Center and your custom application's service provider\. Before you begin this procedure, make sure that you have the service provider's certificate and metadata exchange files so that you can finish setting up the trust\.

**To add and configure a custom SAML application**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. Choose **Add application**\.

1. On the **Select an application** page, choose **Add custom SAML 2\.0 application**\. Then, choose **Next**\.

1. On the **Configure application** page, under **Configure application**, enter a **Display name** for the application, such as **MyApp**\. Then, enter a **Description**\.

1. Under **IAM Identity Center metadata**, do the following:

   1. Under **IAM Identity Center SAML metadata file**, choose **Download** to download the identity provider metadata\.

   1. Under **IAM Identity Center certificate**, choose **Download certificate** to download the identity provider certificate\.
**Note**  
You will need these files later when you set up the custom application from the service provider's website\. 

1. \(Optional\) Under **Application properties**, you can specify additional properties for the **Application start URL**, **Relay State**, and **Session Duration**\. For more information, see [Application properties](appproperties.md)\.

1. Under **Application metadata**, choose **Manually type your metadata values**\. Then, provide the **Application ACS URL** and **Application SAML audience** values\.

1. Choose **Submit**\. You're taken to the details page of the application that you just added\.
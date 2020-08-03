# Certificate Expiration Status Indicators<a name="samlcertexpirationindicators"></a>

While on the **Manage SAML 2\.0 certificates** page, you might notice colored status indicator icons\. These icons appear in the **Expires on** column next to each certificate in the list\. The following describes the criteria that AWS SSO uses to determine which icon is displayed for each certificate\.
+ **Red** – Indicates that a certificate is currently expired\.
+ **Yellow** – Indicates that a certificate will expire in 90 days or less\.
+ **Green** – Indicates that a certificate is currently valid and will remain valid for at least 90 more days\.

**To check the current status of a certificate**

1. In the [AWS SSO console](https://console.aws.amazon.com/singlesignon), choose **Settings**\.

1. On the **Settings** page, under **Identity source**, next to **Authentication**, choose **View details**\.

1. On the **SAML 2\.0 authentication** page, under **Identity provider metadata**, choose **Manage certificates**\.

1. On the **Manage SAML 2\.0 certificates** page, review the status of the certificates in the list as indicated in the **Expires on** column\.
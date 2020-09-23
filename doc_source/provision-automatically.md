# Automatic Provisioning<a name="provision-automatically"></a>

AWS SSO supports automatic provisioning \(synchronization\) of user and group information from your identity provider \(IdP\) into AWS SSO using the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. When you configure SCIM synchronization, you create a mapping of your identity provider \(IdP\) user attributes to the named attributes in AWS SSO\. This causes the expected attributes to match between AWS SSO and your IdP\. You configure this connection in your IdP using your SCIM endpoint for AWS SSO and a bearer token that you create in AWS SSO\.

**Topics**
+ [Considerations for Using Automatic Provisioning](#auto-provisioning-considerations)
+ [How to Enable Automatic Provisioning](#how-to-with-scim)
+ [How to Disable Automatic Provisioning](#disable-provisioning)
+ [How to Generate a New Access Token](#generate-token)
+ [How to Delete an Access Token](#delete-token)
+ [How to Rotate an Access Token](#rotate-token)

## Considerations for Using Automatic Provisioning<a name="auto-provisioning-considerations"></a>

Before you begin deploying SCIM, we recommend that you first review the following important considerations about how it works with AWS SSO\. For additional provisioning considerations applicable to your IdP, see [Supported Identity Providers](supported-idps.md)\.
+ Your IdP must provide a unique primary email address for each user\. In some IdPs, the primary email address might not be a real email address\. For example, it might be a Universal Principal Name \(UPN\) that only looks like an email\. These IdPs may have a secondary or “other” email address that contains the user’s real email address\. You must configure SCIM in your IdP to map the non\-Null unique email address to the AWS SSO primary email address attribute\. And you must map the users non\-Null unique sign\-in identifier to the AWS SSO user name attribute\. Check to see whether your IdP has a single value that is both the sign\-in identifier and the user’s email name\. If so, you can map that IdP field to both the AWS SSO primary email and the AWS SSO user name\.
+ For SCIM synchronization to work, every user must have a **First name**, **Last name**, **Username** and **Display name** value specified\. If any of these values are missing from a user, that user will not be provisioned\.
+ If you need to use third\-party applications, you will first need to map the outbound SAML subject attribute to the user name attribute\. If the third\-party application needs a routable email address, you must provide the email attribute to your IdP\.
+ SCIM provisioning and update intervals are controlled by your identity provider\. Changes to users and groups in your identity provider are only reflected in AWS SSO after your identity provider sends those changes to AWS SSO\. Check with your identity provider for details on the frequency of user and group updates\.
+ Currently, multivalue attributes \(such as multiple emails or phone numbers for a given user\) are not provisioned with SCIM\. Attempts to synchronize multivalue attributes into AWS SSO with SCIM will fail\. To avoid failures, ensure that only a single value is passed for each attribute\. If you have users with multivalue attributes, remove or modify the duplicate attribute mappings in SCIM at your IdP for the connection to AWS SSO\.
+ Verify that the `externalId` SCIM mapping at your IdP corresponds to a value that is unique, always present, and least likely to change for your users\. For example, your IdP might provide a guaranteed `objectId` or other identifier that’s not affected by changes to user attributes like name and email\. If so, you can map that value to the SCIM `externalId` field\. This ensures that your users won’t lose AWS entitlements, assignments or permissions if you need to change their name or email\.
+ Users who have not yet been assigned to an application or AWS account cannot be provisioned into AWS SSO\. To synchronize users and groups, make sure that they are assigned to the application or other setup that represents your IdP’s connection to AWS SSO\.

For more information about AWS SSO’s SCIM implementation, see the [AWS SSO SCIM Implementation Developer Guide](https://docs.aws.amazon.com/singlesignon/latest/developerguide/what-is-scim.html)\.

## How to Enable Automatic Provisioning<a name="how-to-with-scim"></a>

Use the following procedure to enable automatic provisioning of users and groups from your IdP to AWS SSO using the SCIM protocol\.

**Note**  
Before you begin this procedure, we recommend that you first review provisioning considerations that are applicable to your IdP\. For more information, see [Supported Identity Providers](supported-idps.md)\.

**To enable automatic provisioning in AWS SSO**

1. After you have completed the prerequisites, open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under **Identity source > Provisioning**, choose **Enable automatic provisioning**\. This immediately enables automatic provisioning in AWS SSO and displays the necessary endpoint and access token information\.

1. In the **Inbound automatic provisioning** dialog box, copy each of the values for the following options\. You will need to paste these in later when you configure provisioning in your IdP\.

   1. **SCIM endpoint**

   1. **Access token**

1. Choose **Close**\.

Once you have completed this procedure, you must configure automatic provisioning in your IdP\. For more information, see [Supported Identity Providers](supported-idps.md)\.

## How to Disable Automatic Provisioning<a name="disable-provisioning"></a>

Use the following procedure to disable automatic provisioning in the AWS SSO console\.

**Important**  
You must delete the access token before you start this procedure\. For more information, see [How to Delete an Access Token](#delete-token)\.

**To disable automatic provisioning in the AWS SSO console**

1. In the [AWS SSO console](https://console.aws.amazon.com/singlesignon), choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under the **Identity source** section, next to **Provisioning**, choose **View details**\.

1. On the **Automatic provisioning** page, choose **Disable automatic provisioning**\.

1. In the **Disable automatic provisioning** dialog box, review the information, type **DISABLE**, and then choose **Disable automatic provisioning**\.

## How to Generate a New Access Token<a name="generate-token"></a>

Use the following procedure to generate a new access token in the AWS SSO console\.

**To generate a new access token**

1. In the [AWS SSO console](https://console.aws.amazon.com/singlesignon), choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under the **Identity source** section, next to **Provisioning**, choose **View details**\.

1. On the **Automatic provisioning** page, under **Access tokens**, choose **Generate new token**\.

1. In the **Generate new access token** dialog box, under **Access token**, choose **Show token**\.

## How to Delete an Access Token<a name="delete-token"></a>

Use the following procedure to delete an existing access token in the AWS SSO console\.

**To to delete an existing access token**

1. In the [AWS SSO console](https://console.aws.amazon.com/singlesignon), choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under the **Identity source** section, next to **Provisioning**, choose **View details**\.

1. On the **Automatic provisioning** page, under **Access tokens**, next to the access token you want to delete, choose **Delete**\.

1. In the **Delete access token** dialog box, review the information, type **DELETE**, and then choose **Delete access token**\.

## How to Rotate an Access Token<a name="rotate-token"></a>

If your SCIM access token is close to expiring, you can use the following procedure to rotate an existing access token in the AWS SSO console\.

**To rotate an access token**

1. In the [AWS SSO console](https://console.aws.amazon.com/singlesignon), choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under the **Identity source** section, next to **Provisioning**, choose **View details**\.

1. On the **Automatic provisioning** page, under **Access tokens**, make a note of the token ID of the token you want to rotate\.

1. Follow the steps in [How to Generate a New Access Token](#generate-token) to create a new token\. If you have already created the maximum number of SCIM access tokens, you will first need to delete one of the existing tokens\.

1. Go to your identity provider's website and configure the new access token for SCIM provisioning, and then test connectivity to AWS SSO using the new SCIM access token\. Once you've confirmed that provisioning is working successfully using the new token, continue to the next step in this procedure\.

1. Follow the steps in [How to Delete an Access Token](#delete-token) to delete the old access token you noted earlier\. You can also use the token’s creation date as a hint for which token to remove\.
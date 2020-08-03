# Okta<a name="okta-idp"></a>

AWS SSO supports automatic provisioning \(synchronization\) of user and group information from Okta into AWS SSO using the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. To configure this connection in Okta, you use your SCIM endpoint for AWS SSO and a bearer token that is created automatically by AWS SSO\. When you configure SCIM synchronization, you create a mapping of your user attributes in Okta to the named attributes in AWS SSO\. This causes the expected attributes to match between AWS SSO and your IdP\. 

Okta supports the following provisioning features when connected to AWS SSO through SCIM:
+ Create users – Users assigned to the AWS SSO application in Okta will be provisioned in AWS SSO\.
+ Update user attributes – Attribute changes for users who are assigned to the AWS SSO application in Okta will be updated in AWS SSO\. 
+ Deactivate users – Users who are unassigned from the AWS SSO application in Okta will be disabled in AWS SSO\.
+ Group push – Groups \(and their members\) in Okta are synchronized to AWS SSO\.

The following steps walk you through how to enable automatic provisioning of users and groups from Okta to AWS SSO using the SCIM protocol\.

**Note**  
Before you begin deploying SCIM, we recommend that you first review the [Considerations for Using Automatic Provisioning](https://docs.aws.amazon.com/singlesignon/latest/userguide/provision-automatically.html#auto-provisioning-considerations)\. Then continue reviewing additional considerations in the next section\.

**Topics**
+ [Additional Considerations](#okta-considerations)
+ [Prerequisites](#okta-prereqs)
+ [Step 1: Enable Provisioning in AWS SSO](#okta-step1)
+ [Step 2: Configure Provisioning in Okta](#okta-step2)
+ [Step 3: Assign Access for Users and Groups in Okta](#okta-step3)
+ [Troubleshooting](#okta-troubleshooting)

## Additional Considerations<a name="okta-considerations"></a>

The following are important considerations about Okta that can affect how you implement provisioning with AWS SSO\.
+ Using the same Okta group for both assignments and group push is not currently supported\. To maintain consistent group memberships between Okta and AWS SSO, you need to create a separate group and configure it to push groups to AWS SSO\.
+ If you update a user’s address you must have **streetAddress**, **city**, **state**, **zipCode** and the **countryCode** value specified\. If any of these values are not specified for the Okta user at the time of synchronization, the user or changes to the user will not be provisioned\.
+ Entitlements and role attributes are not supported and cannot be synced to AWS SSO\.

## Prerequisites<a name="okta-prereqs"></a>

You will need the following before you can get started:
+ An Okta account \([free trial](https://www.okta.com/free-trial/)\) with Okta's [AWS Single Sign\-On application](https://www.okta.com/integrations/aws-single-sign-on/) installed\.
+ A SAML connection from your Okta account to AWS SSO, as described in [How to Configure SAML 2\.0 for AWS Single Sign\-On](https://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-for-AWS-Single-Sign-on.html)\.
+ An AWS SSO\-enabled account \([free](https://aws.amazon.com/single-sign-on/)\)\. For more information, see [Enable AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/step1.html)\.

## Step 1: Enable Provisioning in AWS SSO<a name="okta-step1"></a>

In this first step, you use the AWS SSO console to enable automatic provisioning\.

**To enable automatic provisioning in AWS SSO**

1. After you have completed the prerequisites, open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under **Identity source > Provisioning**, choose **Enable automatic provisioning**\. This immediately enables automatic provisioning in AWS SSO and displays the necessary endpoint and access token information\.

1. In the **Inbound automatic provisioning** dialog box, copy each of the values for the following options\. You will need to paste these in later when you configure provisioning in your IdP\.

   1. **SCIM endpoint**

   1. **Access token**

1. Choose **Close**\.

You have set up provisioning in the AWS SSO console\. Now you need to do the remaining tasks using the Okta user interface as described in the following procedures\.

## Step 2: Configure Provisioning in Okta<a name="okta-step2"></a>

Use the following procedure in the Okta admin portal to enable integration between AWS SSO and the AWS Single Sign\-On app\.

**To configure provisioning in Okta**

1. In a separate browser window, login to the Okta admin portal and navigate to the [AWS Single Sign\-On app](https://www.okta.com/integrations/aws-single-sign-on/)\.

1. In the AWS Single Sign\-On app page, choose the **Provisioning** tab, and then choose **Integration**\.

1. Choose **Configure API Integration**, and then select the check box next to **Enable API integration** to enable provisioning\.

1. In the previous procedure you copied the **SCIM endpoint** value in AWS SSO\. Paste that value into the **Base URL** field in Okta\. Make sure that you remove the trailing forward slash at the end of the URL\. Also, in the previous procedure you copied the **Access token** value in AWS SSO\. Paste that value into the **API Token** field in Okta\.

1. Choose **Test API Credentials** to verify the credentials entered are valid\.

1. Choose **Save**\.

1. Under **Settings**, select **To App**, choose **Edit**, and then select the **Enable** checkbox for each of the **Provisioning Features** you want to enable\.

1. Choose **Save**\. 

By default, no users or groups are assigned to your Okta AWS Single Sign\-On app so you will need to complete the next procedure to begin synchronizing users and groups to AWS SSO\.

## Step 3: Assign Access for Users and Groups in Okta<a name="okta-step3"></a>

Use the following procedures in Okta to assign access to your users and groups\. Okta users who belong to groups that you assign here are synchronized automatically to AWS SSO\. To minimize administrative overhead in both Okta and AWS SSO, we recommend that you assign and *push* groups instead of individual users\.

After you complete this step and the first synchronization with SCIM is completed, the users and groups that you have assigned appear in AWS SSO\. Those users are able to access the AWS SSO user portal using their Okta credentials\. 

**To assign access for users in Okta**

1. In the **AWS Single Sign\-On app** page, select the **Assignments** tab\.

1. In the **Assignments** page, choose **Assign**, and then choose **Assign to People**\.

1. Select the Okta user or users whom you want to assign access to the AWS Single Sign\-On app\. Choose **Assign**, choose **Save and Go Back**, and then choose **Done**\. This starts the process of provisioning the user or users into AWS SSO\. 

**To assign access for groups in Okta**

1. On the **AWS Single Sign\-On app** page, choose the **Assignments** tab\.

1. In the **Assignments** page, choose **Assign**, and then choose **Assign to Groups**\.

1. Select the Okta group or groups that you want to assign access to the AWS Single Sign\-On app\. Choose **Assign**, choose **Save and Go Back**, and then choose **Done**\. This starts the process of provisioning the users in the group into AWS SSO\.

1. Choose the **Push Groups** tab, choose the Okta group or groups that you selected in the previous step\. Then choose **Save**\. The group status changes to **Active** after the group and its members have successfully been pushed to AWS SSO\.

To grant your Okta users access to AWS accounts and cloud applications, complete the following applicable procedures from the AWS SSO console:
+ To grant access to AWS accounts, see [Assign User Access](https://docs.aws.amazon.com/singlesignon/latest/userguide/useraccess.html#assignusers)\.
+ To grant access to cloud applications, see [Assign User Access](https://docs.aws.amazon.com/singlesignon/latest/userguide/assignuserstoapp.html)\.

## Troubleshooting<a name="okta-troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter while setting up automatic provisioning with Okta\.

**Base URL: Does not match required pattern**

The SCIM endpoint URL that you pasted into **Base URL** likely contains a trailing forward slash \(/\)\. Remove the forward slash from the SCIM endpoint URL before pasting into **Base URL**\. For example, https://scim\.us\-east\-2\.amazonaws\.com/*xxxxxxxx\-xxxx\-xxxxx\-xxxxxx\-xxxx*/scim/v2\.

**Error during synchronization**

After you have started synchronization, you might see the following error: 

```
Automatic profile push of <user> to app AWS Single Sign-On failed: Error while trying to push profile update for <user>@Corp.Example.com: Bad Request. Errors reported by remote server: Request is unparsable, syntactically incorrect, or violates schema.
```

For SCIM synchronization to work:
+ Every user must have a **First name**, **Last name**, **Username** and **Display name** value specified\. If any of these values are missing from a user, that user will not be provisioned\.
+ If you update a user’s address you must have **streetAddress**, **city**, **state**, **zipCode** and the **countryCode** value specified\. If any of these values are not specified for the Okta user at the time of synchronization, the user or changes to the user will not be provisioned\.
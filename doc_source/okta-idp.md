# Okta<a name="okta-idp"></a>

IAM Identity Center supports automatic provisioning \(synchronization\) of user and group information from Okta into IAM Identity Center using the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. To configure this connection in Okta, you use your SCIM endpoint for IAM Identity Center and a bearer token that is created automatically by IAM Identity Center\. When you configure SCIM synchronization, you create a mapping of your user attributes in Okta to the named attributes in IAM Identity Center\. This causes the expected attributes to match between IAM Identity Center and your IdP\. 

Okta supports the following provisioning features when connected to IAM Identity Center through SCIM:
+ Create users – Users assigned to the IAM Identity Center application in Okta will be provisioned in IAM Identity Center\.
+ Update user attributes – Attribute changes for users who are assigned to the IAM Identity Center application in Okta will be updated in IAM Identity Center\. 
+ Deactivate users – Users who are unassigned from the IAM Identity Center application in Okta will be disabled in IAM Identity Center\.
+ Group push – Groups \(and their members\) in Okta are synchronized to IAM Identity Center\.

The following steps walk you through how to enable automatic provisioning of users and groups from Okta to IAM Identity Center using the SCIM protocol\.

**Note**  
Before you begin deploying SCIM, we recommend that you first review the [Considerations for using automatic provisioning](provision-automatically.md#auto-provisioning-considerations)\. Then continue reviewing additional considerations in the next section\.

**Topics**
+ [Additional considerations](#okta-considerations)
+ [Prerequisites](#okta-prereqs)
+ [Step 1: Enable provisioning in IAM Identity Center](#okta-step1)
+ [Step 2: Configure provisioning in Okta](#okta-step2)
+ [Step 3: Assign access for users and groups in Okta](#okta-step3)
+ [\(Optional\) Step 4: Configure user attributes in Okta for access control in IAM Identity Center](#okta-step4)
+ [\(Optional\) Passing attributes for access control](#okta-passing-abac)
+ [Troubleshooting](#okta-troubleshooting)

## Additional considerations<a name="okta-considerations"></a>

The following are important considerations about Okta that can affect how you implement provisioning with IAM Identity Center\.
+ Using the same Okta group for both assignments and group push is not currently supported\. To maintain consistent group memberships between Okta and IAM Identity Center, you need to create a separate group and configure it to push groups to IAM Identity Center\.
+ If you update a user’s address you must have **streetAddress**, **city**, **state**, **zipCode** and the **countryCode** value specified\. If any of these values are not specified for the Okta user at the time of synchronization, the user or changes to the user will not be provisioned\.
+ Entitlements and role attributes are not supported and cannot be synced to IAM Identity Center\.

## Prerequisites<a name="okta-prereqs"></a>

You will need the following before you can get started:
+ An Okta account \([free trial](https://www.okta.com/free-trial/)\) with Okta's [IAM Identity Center application](https://www.okta.com/integrations/aws-single-sign-on/) installed\. Note also that for paid Okta products, you might need to confirm that your Okta license supports “lifecycle management” or similar capabilities that enable outbound provisioning\. These features might be necessary to configure SCIM from Okta to IAM Identity Center\.
+ A SAML connection from your Okta account to IAM Identity Center, as described in [How to Configure SAML 2\.0 for IAM Identity Center](https://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-for-Amazon-Web-Service.html)\.
+ An IAM Identity Center\-enabled account \([free](https://aws.amazon.com/single-sign-on/)\)\. For more information, see [Enable IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/step1.html)\.

## Step 1: Enable provisioning in IAM Identity Center<a name="okta-step1"></a>

In this first step, you use the IAM Identity Center console to enable automatic provisioning\.

**To enable automatic provisioning in IAM Identity Center**

1. After you have completed the prerequisites, open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings** in the left navigation pane\.

1. On the **Settings** page, locate the **Automatic provisioning** information box, and then choose **Enable**\. This immediately enables automatic provisioning in IAM Identity Center and displays the necessary SCIM endpoint and access token information\.

1. In the **Inbound automatic provisioning** dialog box, copy each of the values for the following options\. You will need to paste these in later when you configure provisioning in your IdP\.

   1. **SCIM endpoint**

   1. **Access token**

1. Choose **Close**\.

You have set up provisioning in the IAM Identity Center console\. Now you need to do the remaining tasks using the Okta user interface as described in the following procedures\.

## Step 2: Configure provisioning in Okta<a name="okta-step2"></a>

Use the following procedure in the Okta admin portal to enable integration between IAM Identity Center and the IAM Identity Center app\.

**To configure provisioning in Okta**

1. In a separate browser window, log in to the Okta admin portal and navigate to the [IAM Identity Center app](https://www.okta.com/integrations/aws-single-sign-on/)\.

1. On the **IAM Identity Center app** page, choose the **Provisioning** tab, and then choose **Integration**\.

1. Choose **Configure API Integration**, and then select the check box next to **Enable API integration** to enable provisioning\.

1. In the previous procedure you copied the **SCIM endpoint** value in IAM Identity Center\. Paste that value into the **Base URL** field in Okta\. Make sure that you remove the trailing forward slash at the end of the URL\. Also, in the previous procedure you copied the **Access token** value in IAM Identity Center\. Paste that value into the **API Token** field in Okta\.

1. Choose **Test API Credentials** to verify the credentials entered are valid\.

1. Choose **Save**\.

1. Under **Settings**, choose **To App**, choose **Edit**, and then select the **Enable** check box for each of the **Provisioning Features** you want to enable\.

1. Choose **Save**\. 

By default, no users or groups are assigned to your Okta IAM Identity Center app\. Therefore you must complete the next procedure to begin synchronizing users and groups to IAM Identity Center\.

## Step 3: Assign access for users and groups in Okta<a name="okta-step3"></a>

Use the following procedures in Okta to assign access to your users and groups\. Okta users who belong to groups that you assign here are synchronized automatically to IAM Identity Center\. To minimize administrative overhead in both Okta and IAM Identity Center, we recommend that you assign and *push* groups instead of individual users\.

After you complete this step and the first synchronization with SCIM is completed, the users and groups that you have assigned appear in IAM Identity Center\. Those users are able to access the AWS access portal using their Okta credentials\. 

**To assign access for users in Okta**

1. In the **IAM Identity Center app** page, choose the **Assignments** tab\.

1. In the **Assignments** page, choose **Assign**, and then choose **Assign to People**\.

1. Choose the Okta user or users whom you want to assign access to the IAM Identity Center app\. Choose **Assign**, choose **Save and Go Back**, and then choose **Done**\. This starts the process of provisioning the user or users into IAM Identity Center\. 

**To assign access for groups in Okta**

1. On the **IAM Identity Center app** page, choose the **Assignments** tab\.

1. In the **Assignments** page, choose **Assign**, and then choose **Assign to Groups**\.

1. Choose the Okta group or groups that you want to assign access to the IAM Identity Center app\. Choose **Assign**, choose **Save and Go Back**, and then choose **Done**\. This starts the process of provisioning the users in the group into IAM Identity Center\.

1. Choose the **Push Groups** tab\. Choose the Okta group or groups that you chose in the previous step\.
**Note**  
These chosen groups must be different from those assigned to the application\. To maintain consistent group memberships between Okta and IAM Identity Center, you need to create a separate group and configure it to push groups to IAM Identity Center\. 

   Then choose **Save**\. The group status changes to **Active** after the group and its members have successfully been pushed to IAM Identity Center\.

To grant your Okta users access to AWS accounts and cloud applications, complete the following applicable procedures from the IAM Identity Center console:
+ To grant access to AWS accounts, see [Assign user access](useraccess.md#assignusers)\.
+ To grant access to cloud applications, see [Assign user access](assignuserstoapp.md)\.

## \(Optional\) Step 4: Configure user attributes in Okta for access control in IAM Identity Center<a name="okta-step4"></a>

This is an optional procedure for Okta should you choose to configure attributes you will use in IAM Identity Center to manage access to your AWS resources\. The attributes you define in Okta will be passed in a SAML assertion to IAM Identity Center, you will then create a permission set in IAM Identity Center to manage access based on the attributes you passed from Okta\.

Before you begin this procedure, you first need to enable the [Attributes for access control](attributesforaccesscontrol.md) feature\. For more information about how to do this, see [Enable and configure attributes for access control](configure-abac.md)\.

**To configure user attributes in Okta for access control in IAM Identity Center**

1. In a separate browser window, log in to the Okta admin portal and navigate to the [IAM Identity Center app](https://www.okta.com/integrations/aws-single-sign-on/)\.

1. On the **IAM Identity Center app** page, choose the **Sign On** tab, and then choose **Edit**\.

1. In the **SAML** section, expand **Attributes \(Optional\)**\.

1. In the **Attribute Statements \(optional\)** section, do the following for each attribute where you will use IAM Identity Center for access control:

   1. In the **Name** field, enter `https://aws.amazon.com/SAML/Attributes/AccessControl:AttributeName`, and replace **AttributeName** with the name of the attribute you are expecting in IAM Identity Center\. For example, `https://aws.amazon.com/SAML/Attributes/AccessControl:Department`\. 

   1. In the **Name Format** field, choose **URI reference**\. 

   1. In the **Value** field, enter `user.AttributeName`, replace **AttributeName** with the Okta default user profile variable name\. For example, `user.department`\. To find your Okta default user profile variable name, see [View the Okta default user profile](https://help.okta.com/en/prod/Content/Topics/users-groups-profiles/usgp-view-user-profile.htm) on the Okta website\. 

1. \(Optional\) Choose **Preview SAML**, to review a sample SAML assertion that includes the new attributes\.

1. Choose **Save**\.

## \(Optional\) Passing attributes for access control<a name="okta-passing-abac"></a>

You can optionally use the [Attributes for access control](attributesforaccesscontrol.md) feature in IAM Identity Center to pass an `Attribute` element with the `Name` attribute set to `https://aws.amazon.com/SAML/Attributes/AccessControl:{TagKey}`\. This element allows you to pass attributes as session tags in the SAML assertion\. For more information about session tags, see [Passing session tags in AWS STS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_session-tags.html) in the *IAM User Guide*\.

To pass attributes as session tags, include the `AttributeValue` element that specifies the value of the tag\. For example, to pass the tag key\-value pair `CostCenter = blue`, use the following attribute\.

```
<saml:AttributeStatement>
<saml:Attribute Name="https://aws.amazon.com/SAML/Attributes/AccessControl:CostCenter">
<saml:AttributeValue>blue
</saml:AttributeValue>
</saml:Attribute>
</saml:AttributeStatement>
```

If you need to add multiple attributes, include a separate `Attribute` element for each tag\. 

## Troubleshooting<a name="okta-troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter while setting up automatic provisioning with Okta\.

**Base URL: Does not match required pattern**

The SCIM endpoint URL that you pasted into **Base URL** likely contains a trailing forward slash \(/\)\. Remove the forward slash from the SCIM endpoint URL before pasting into **Base URL**\. For example, https://scim\.us\-east\-2\.amazonaws\.com/*xxxxxxxx\-xxxx\-xxxxx\-xxxxxx\-xxxx*/scim/v2\.

**Error during synchronization**

After you have started synchronization, you might see the following error: 

```
Automatic profile push of <user> to app IAM Identity Center failed: Error while trying to push profile update for <user>@Corp.Example.com: Bad Request. Errors reported by remote server: Request is unparsable, syntactically incorrect, or violates schema.
```

For SCIM synchronization to work:
+ Every user must have a **First name**, **Last name**, **Username**, and **Display name** value specified\. If any of these values are missing from a user, that user will not be provisioned\.
+ Usernames should be mapped to attributes that are unique within your directory in Okta\.
+ The following special characters must not be used in attributes that are synchronized with SCIM: `<>;:%`
+ If you update a user’s address you must have **streetAddress**, **city**, **state**, **zipCode** and the **countryCode** value specified\. If any of these values are not specified for the Okta user at the time of synchronization, the user or changes to the user will not be provisioned\.
# JumpCloud<a name="jumpcloud-idp"></a>

IAM Identity Center supports automatic provisioning \(synchronization\) of user information from JumpCloud Directory Platform into IAM Identity Center\. This provisioning uses the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. You configure this connection in JumpCloud using your IAM Identity Center SCIM endpoint and access token\. When you configure SCIM synchronization, you create a mapping of your user attributes in JumpCloud to the named attributes in IAM Identity Center\. This causes the expected attributes to match between IAM Identity Center and JumpCloud\. 

This guide is based on JumpCloud as of June 2021\. Steps for newer versions may vary\. This guide contains a few notes regarding configuration of user authentication through SAML\. 

The following steps walk you through how to enable automatic provisioning of users and groups from JumpCloud to IAM Identity Center using the SCIM protocol\.

**Note**  
Before you begin deploying SCIM, we recommend that you first review the [Considerations for using automatic provisioning](provision-automatically.md#auto-provisioning-considerations)\. Then continue reviewing additional considerations in the next section\.

**Topics**
+ [Prerequisites](#jumpcloud-prereqs)
+ [SCIM considerations](#jumpcloud-scim)
+ [Step 1: Enable provisioning in IAM Identity Center](#jumpcloud-step1)
+ [Step 2: Configure provisioning in JumpCloud](#jumpcloud-step2)
+ [\(Optional\) Step 3: Configure user attributes in JumpCloud for access control in IAM Identity Center](#jumpcloud-step3)
+ [\(Optional\) Passing attributes for access control](#jumpcloud-passing-abac)

## Prerequisites<a name="jumpcloud-prereqs"></a>

You will need the following before you can get started:
+ JumpCloud subscription or free trial\. To sign up for a free trial visit [JumpCloud](https://console.jumpcloud.com/signup)\.
+ An IAM Identity Center enabled account \([free](https://aws.amazon.com/single-sign-on/)\)\. For more information, see [Enable IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/step1.html)\.
+ A SAML connection from your JumpCloud account to IAM Identity Center, as described in [ JumpCloud documentation for IAM Identity Center ](https://support.jumpcloud.com/support/s/article/Single-Sign-On-SSO-With-AWS-SSO)\.
+ Associate the IAM Identity Center connector with the groups you want to allow access to AWS accounts\.

## SCIM considerations<a name="jumpcloud-scim"></a>

 The following are considerations when using JumpCloud federation for IAM Identity Center\. 
+ Only groups associated with the AWS Single Sign\-On connector in JumpCloud will be synchronized via SCIM\.
+ Only one phone number attribute can be synchronized and the default is "work phone\."
+ Users in JumpCloud directory must have first and last names configured to be synchronized to IAM Identity Center via SCIM\.
+ Attributes are still synchronized if the user is disabled in IAM Identity Center but still activate in JumpCloud\.
+ You can choose to enable SCIM sync for only user information by unchecking the "Enable management of User Groups and Group membership" in the connector\.
+ If there is an existing user in Identity Center directory with the same username and email, the user will be overwritten and synchronized via SCIM from JumpCloud\.

## Step 1: Enable provisioning in IAM Identity Center<a name="jumpcloud-step1"></a>

In this first step, you use the IAM Identity Center console to enable automatic provisioning\.

**To enable automatic provisioning in IAM Identity Center**

1. After you have completed the prerequisites, open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings** in the left navigation pane\.

1. On the **Settings** page, locate the **Automatic provisioning** information box, and then choose **Enable**\. This immediately enables automatic provisioning in IAM Identity Center and displays the necessary SCIM endpoint and access token information\.

1. In the **Inbound automatic provisioning** dialog box, copy each of the values for the following options\. You will need to paste these in later when you configure provisioning in your IdP\.

   1. **SCIM endpoint**

   1. **Access token**

1. Choose **Close**\.

Now that you have set up provisioning in the IAM Identity Center console, you need to complete the remaining tasks using the JumpCloud IAM Identity Center connector\. These steps are described in the following procedure\. 

## Step 2: Configure provisioning in JumpCloud<a name="jumpcloud-step2"></a>

Use the following procedure in the JumpCloud IAM Identity Center connector to enable provisioning with IAM Identity Center\. This procedure assumes that you have already added the JumpCloud IAM Identity Center connector to your JumpCloud admin portal and groups\. If you have not yet done so, refer to [Prerequisites](#jumpcloud-prereqs), and then complete this procedure to configure SCIM provisioning\. 

**To configure provisioning in JumpCloud**

1. Open the JumpCloud IAM Identity Center connector that you installed as part of configuring SAML for JumpCloud \(**User Authentication** > **IAM Identity Center**\)\. See [Prerequisites](#jumpcloud-prereqs)\.

1. Choose the **IAM Identity Center** connector, and then choose the third tab **Identity Management**\.

1. Check the box for **Enable management of User Groups and Group membership in this application** if you want groups to SCIM sync\.

1. Click on **Configure**\.

1. In the previous procedure, you copied the **SCIM endpoint** value in IAM Identity Center\. Paste that value into the **Base URL** field in the JumpCloud IAM Identity Center connector\. Make sure that you remove the trailing forward slash at the end of the URL\.

1. From the previous procedure you copied the **Access token** value in IAM Identity Center\. Paste that value into the **Token Key** field in the JumpCloud IAM Identity Center connector\. 

1. Click **Activate** to apply the configuration\.

1. Make sure you have a green indicator next to **Single Sign\-On activated**\.

1. Move to the fourth tab **User Groups** and check the groups you want to be provisioned via SCIM\.

1. Click **Save** at the bottom once you are done\.

1. To verify that users have been successfully synchronized to IAM Identity Center, return to the IAM Identity Center console and choose **Users**\. Synchronized users from JumpCloud will appear on the **Users** page\. These users can now be assigned to accounts within IAM Identity Center\.

## \(Optional\) Step 3: Configure user attributes in JumpCloud for access control in IAM Identity Center<a name="jumpcloud-step3"></a>

This is an optional procedure for JumpCloud should you choose to configure attributes for IAM Identity Center to manage access to your AWS resources\. The attributes that you define in JumpCloud will be passed in a SAML assertion to IAM Identity Center\. You then create a permission set in IAM Identity Center to manage access based on the attributes you passed from JumpCloud\. 

Before you begin this procedure, you must first enable the [Attributes for access control](https://docs.aws.amazon.com/singlesignon/latest/userguide/attributesforaccesscontrol.html) feature\. For more information about how to do this, see [ Enable and configure attributes for access control](https://docs.aws.amazon.com/singlesignon/latest/userguide/configure-abac.html)\.

****To configure user attributes in JumpCloud for access control in IAM Identity Center****

1. Open the JumpCloud IAM Identity Center connector that you installed as part of configuring SAML for JumpCloud \(**User Authentication** > **IAM Identity Center**\)\.

1. Choose the **IAM Identity Center** connector\. Then, choose the second tab **IAM Identity Center**\.

1. At the bottom of this tab you have **User Attribute Mapping**, choose **Add new attribute**, and then do the following: You must perform these steps for each attribute you will add for use in IAM Identity Center for access control\. 

   1. In the **Service Provide Attribute Name** field, enter `https://aws.amazon.com/SAML/Attributes/AccessControl:AttributeName.` Replace `AttributeName` with the name of the attribute you are expecting in IAM Identity Center\. For example, `https://aws.amazon.com/SAML/Attributes/AccessControl:Email`\. 

   1. In the **JumpCloud Attribute Name** field, choose user attributes from your JumpCloud directory\. For example, **Email \(Work\)**\.

1. Choose **Save**\.

## \(Optional\) Passing attributes for access control<a name="jumpcloud-passing-abac"></a>

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
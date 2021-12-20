# CyberArk<a name="cyberark-idp"></a>

AWS SSO supports automatic provisioning \(synchronization\) of user information from CyberArk Directory Platform into AWS SSO\. This provisioning uses the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. You configure this connection in CyberArk using your AWS SSO SCIM endpoint and access token\. When you configure SCIM synchronization, you create a mapping of your user attributes in CyberArk to the named attributes in AWS SSO\. This causes the expected attributes to match between AWS SSO and CyberArk\. 

This guide is based on CyberArk as of August 2021\. Steps for newer versions may vary\. This guide contains a few notes regarding configuration of user authentication through SAML\. 

**Note**  
Before you begin deploying SCIM, we recommend that you first review the [Considerations for using automatic provisioning](provision-automatically.md#auto-provisioning-considerations)\. Then continue reviewing additional considerations in the next section\.

**Topics**
+ [Prerequisites](#cyberark-prereqs)
+ [SCIM considerations](#cyberark-considerations)
+ [Step 1: Enable provisioning in AWS SSO](#cyberark-step1)
+ [Step 2: Configure provisioning in CyberArk](#cyberark-step2)
+ [\(Optional\) Step 3: Configure user attributes in CyberArk for access control \(ABAC\) in AWS SSO](#cyberark-step3)
+ [\(Optional\) Passing attributes for access control](#cyberark-passing-abac)

## Prerequisites<a name="cyberark-prereqs"></a>

You will need the following before you can get started:
+ CyberArk subscription or free trial\. To sign up for a free trial visit [CyberArk](https://www.idaptive.com/free-trial)\.
+ An AWS SSO\-enabled account \([free](https://aws.amazon.com/single-sign-on/)\)\. For more information, see [ Enable AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/step1.html)\.
+ A SAML connection from your CyberArk account to AWS SSO, as described in [CyberArk documentation for AWS SSO](https://docs.cyberark.com/Product-Doc/OnlineHelp/Idaptive/Latest/en/Content/Applications/AppsWeb/AWS_SAML_SSO.htm#!#AWS_Single_Sign-On_SAML_Single_Sign-On_(SSO))\.
+ Associate the AWS Single Sign\-On connector with the roles, users and organizations you want to allow access to AWS accounts\.

## SCIM considerations<a name="cyberark-considerations"></a>

The following are considerations when using CyberArk federation for AWS SSO:
+ Only roles mapped in the application Provisioning section will be synchronized to AWS Single Sign\-On\.
+ The provisioning script is supported only in its default state, once changed the SCIM provisioning might fail\.
  + Only one phone number attribute can be synchronized and the default is “work phone”\.
+ If the role mapping in CyberArk AWS SSO application is changed, the below behavior is expected:
  + If the role names are changed \- no changes to the group names in AWS SSO\.
  + If the group names are changed \- new groups will be created in AWS SSO, old groups will remain but will have no members\.
+ User synchronization and de\-provisioning behavior can be set up from the CyberArk AWS Single Sign\-On application, make sure you set up the right behavior for your organization\. These are the options you have:
  + Overwrite \(or not\) users in AWS SSO directory with the same principal name\.
  + De\-provision users from AWS SSO when the user is removed from the CyberArk role\.
  + De\-provision user behavior \- disable or delete\.

## Step 1: Enable provisioning in AWS SSO<a name="cyberark-step1"></a>

In this first step, you use the AWS SSO console to enable automatic provisioning\.

**To enable automatic provisioning in AWS SSO**

1. After you have completed the prerequisites, open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under **Identity source**, next to **Provisioning**, choose **Enable automatic provisioning**\. This immediately enables automatic provisioning in AWS SSO and displays the necessary endpoint and access token information\.

1. In the **Inbound automatic provisioning** dialog box, copy each of the values for the following options\. You will need to paste these in later when you configure provisioning in your IdP\.

   1. **SCIM endpoint**

   1. **Access token**

1. Choose **Close**\.

Now that you have set up provisioning in the AWS SSO console, you need to complete the remaining tasks using the CyberArk AWS Single Sign\-On application\. These steps are described in the following procedure\.

## Step 2: Configure provisioning in CyberArk<a name="cyberark-step2"></a>

 Use the following procedure in the CyberArk AWS Single Sign\-On application to enable provisioning with AWS SSO\. This procedure assumes that you have already added the CyberArk AWS Single Sign\-On application to your CyberArk admin console under **Web Apps**\. If you have not yet done so, refer to the [Prerequisites](#cyberark-prereqs), and then complete this procedure to configure SCIM provisioning\. 

**To configure provisioning in CyberArk**

1. Open the CyberArk AWS Single Sign\-On application that you added as part of configuring SAML for CyberArk \(**Apps > Web App**\)\. See [Prerequisites](#cyberark-prereqs)\.

1. Choose the **AWS Single Sign\-On** application and go to the **Provisioning** section\.

1. Check the box for **Enable provisioning for this application** and choose **Live Mode**\.

1. In the previous procedure, you copied the **SCIM endpoint** value from AWS SSO\. Paste that value into the **SCIM Service URL** field, in the CyberArk's AWS Single Sign\-On's application set the **Authorization Type** to be **Authorization Header**\. Make sure that you remove the trailing forward slash at the end of the URL\. 

1. Set the **Header Type** to **Bearer Token**\.

1. From the previous procedure you copied the **Access token** value in AWS SSO\. Paste that value into the **Bearer Token** field in the CyberArk AWS Single Sign\-On application\.

1. Click **Verify** to test and apply the configuration\.

1. Under the **Sync Options**, choose the right behavior for which you want the outbound provisioning from CyberArk to work\. You can choose to overwrite \(or not\) existing AWS SSO users with similar principal name, and the de\-provisioning behavior\.

1. Under **Role Mapping** set up the mapping from CyberArk roles, under the **Name** field to the AWS SSO group, under the **Destination Group**\.

1. Click **Save** at the bottom once you are done\.

1. To verify that users have been successfully synchronized to AWS SSO, return to the AWS SSO console and choose **Users**\. Synchronized users from CyberArk will appear on the **Users** page\. These users can now be assigned to accounts and can connect within AWS SSO\.

## \(Optional\) Step 3: Configure user attributes in CyberArk for access control \(ABAC\) in AWS SSO<a name="cyberark-step3"></a>

This is an optional procedure for CyberArk should you choose to configure attributes for AWS SSO to manage access to your AWS resources\. The attributes that you define in CyberArk will be passed in a SAML assertion to AWS SSO\. You then create a permission set in AWS SSO to manage access based on the attributes you passed from CyberArk\. 

Before you begin this procedure, you must first enable the [Attributes for access control](attributesforaccesscontrol.md) feature\. For more information about how to do this, see [Enable and configure attributes for access control](configure-abac.md)\.

**To configure user attributes in CyberArk for access control in AWS SSO**

1. Open the CyberArk AWS Single Sign\-On application that you installed as part of configuring SAML for CyberArk \(**Apps > Web Apps**\)\.

1. Go to the **SAML Response** option\.

1. Under **Attributes**, add the relevant attributes to the table following the below logic:

   1. **Attribute Name** is the original attribute name from CyberArk\.

   1. **Attribute Value** is the attribute name sent in the SAML assertion to AWS SSO\.

1. Choose **Save**\.

## \(Optional\) Passing attributes for access control<a name="cyberark-passing-abac"></a>

You can optionally use the [Attributes for access control](attributesforaccesscontrol.md) feature in AWS SSO to pass an `Attribute` element with the `Name` attribute set to `https://aws.amazon.com/SAML/Attributes/AccessControl:{TagKey}`\. This element allows you to pass attributes as session tags in the SAML assertion\. For more information about session tags, see [Passing session tags in AWS STS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_session-tags.html) in the *IAM User Guide*\.

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
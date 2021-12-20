# PingOne<a name="pingone-idp"></a>

AWS SSO supports automatic provisioning \(synchronization\) of user information from the PingOne product by Ping Identity \(hereafter “Ping”\) into AWS SSO\. This provisioning uses the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. You configure this connection in PingOne using your AWS SSO SCIM endpoint and access token\. When you configure SCIM synchronization, you create a mapping of your user attributes in PingOne to the named attributes in AWS SSO\. This causes the expected attributes to match between AWS SSO and PingOne\.

This guide is based on PingOne as of October 2020\. Steps for newer versions may vary\. Contact Ping for more information about how to configure provisioning to AWS SSO for other versions of PingOne\. This guide also contains a few notes regarding configuration of user authentication through SAML\.

The following steps walk you through how to enable automatic provisioning of users from PingOne to AWS SSO using the SCIM protocol\.

**Note**  
Before you begin deploying SCIM, we recommend that you first review the [Considerations for using automatic provisioning](provision-automatically.md#auto-provisioning-considerations)\. Then continue reviewing additional considerations in the next section\.

**Topics**
+ [Prerequisites](#pingone-prereqs)
+ [Additional considerations](#pingone-considerations)
+ [Step 1: Enable provisioning in AWS SSO](#pingone-step1)
+ [Step 2: Configure provisioning in PingOne](#pingone-step2)
+ [\(Optional\) Step 3: Configure user attributes in PingOne for access control in AWS SSO](#pingone-step3)
+ [\(Optional\) Passing attributes for access control](#pingone-passing-abac)

## Prerequisites<a name="pingone-prereqs"></a>

You will need the following before you can get started:
+ A PingOne subscription or free trial, with both federated authentication and provisioning capabilities\. For more information about how to obtain a free trial, see the [Ping Identity](https://www.pingidentity.com/en/trials.html) website\.
+ An AWS SSO\-enabled account \([free](https://aws.amazon.com/single-sign-on/)\)\. For more information, see [Enable AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/step1.html)\.
+ The PingOne AWS Single Sign\-On application added to your PingOne admin portal\. You can obtain the PingOne AWS Single Sign\-On application from the PingOne Application Catalog\. For general information, see [Add an application from the Application Catalog](https://docs.pingidentity.com/bundle/pingone/page/vcx1564020496826-1.html) on the Ping Identity website\.
+ A SAML connection from your PingOne instance to AWS SSO\. After the PingOne AWS Single Sign\-On application has been added to your PingOne admin portal, you must use it to configure a SAML connection from your PingOne instance to AWS SSO\. Use the “download” and “import" metadata feature on both ends to exchange SAML metadata between PingOne and AWS SSO\. For instructions on how to configure this connection, see the PingOne documentation\.

## Additional considerations<a name="pingone-considerations"></a>

The following are important considerations about PingOne that can affect how you implement provisioning with AWS SSO\.
+ As of October 2020, PingOne does not support provisioning of groups through SCIM\. Please contact Ping for the latest information on group support in SCIM for PingOne\.
+ Users may continue to be provisioned from PingOne after disabling provisioning in the PingOne admin portal\. If you need to terminate provisioning immediately, delete the relevant SCIM bearer token, and/or disable [Automatic provisioning](provision-automatically.md) in AWS SSO\.
+ If an attribute for a user is removed from the data store configured in PingOne, that attribute will not be removed from the corresponding user in AWS SSO\. This is a known limitation in PingOne’s provisioner implementation\. If an attribute is modified, the change will be synchronized to AWS SSO\.
+ The following are important notes regarding your SAML configuration in PingOne:
  + AWS SSO supports only `emailaddress` as a `NameId` format\. This means you need to choose a user attribute that is unique within your directory in PingOne, non\-null, and formatted as an email/UPN \(for example, user@domain\.com\) for your **SAML\_SUBJECT** mapping in PingOne\. **Email \(Work\)** is a reasonable value to use for test configurations with the PingOne built\-in directory\.
  + Users in PingOne with an email address containing a **\+** character may be unable to sign in to AWS SSO, with errors such as `'SAML_215'` or `'Invalid input'`\. To fix this, in PingOne, choose the **Advanced** option for the **SAML\_SUBJECT** mapping in **Attribute Mappings**\. Then set **Name ID Format to send to SP:** to **urn:oasis:names:tc:SAML:1\.1:nameid\-format:emailAddress** in the drop\-down menu\.

## Step 1: Enable provisioning in AWS SSO<a name="pingone-step1"></a>

In this first step, you use the AWS SSO console to enable automatic provisioning\.

**To enable automatic provisioning in AWS SSO**

1. After you have completed the prerequisites, open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under **Identity source**, next to **Provisioning**, choose **Enable automatic provisioning**\. This immediately enables automatic provisioning in AWS SSO and displays the necessary endpoint and access token information\.

1. In the **Inbound automatic provisioning** dialog box, copy each of the values for the following options\. You will need to paste these in later when you configure provisioning in your IdP\.

   1. **SCIM endpoint**

   1. **Access token**

1. Choose **Close**\.

Now that you have set up provisioning in the AWS SSO console, you need to complete the remaining tasks using the PingOne AWS Single Sign\-On application\. These steps are described in the following procedure\. 

## Step 2: Configure provisioning in PingOne<a name="pingone-step2"></a>

Use the following procedure in the PingOne AWS Single Sign\-On application to enable provisioning with AWS SSO\. This procedure assumes that you have already added the PingOne AWS Single Sign\-On application to your PingOne admin portal\. If you have not yet done so, refer to [Prerequisites](#pingone-prereqs), and then complete this procedure to configure SCIM provisioning\. 

**To configure provisioning in PingOne**

1. Open the PingOne AWS Single Sign\-On application that you installed as part of configuring SAML for PingOne \(**Applications** > **My Applications**\)\. See [Prerequisites](#pingone-prereqs)\.

1. Scroll to the bottom of the page\. Under **User Provisioning**, choose the **complete** link to navigate to the user provisioning configuration of your connection\.

1. On the **Provisioning Instructions** page, choose **Continue to Next Step**\.

1. In the previous procedure, you copied the **SCIM endpoint** value in AWS SSO\. Paste that value into the **SCIM URL** field in the PingOne AWS Single Sign\-On application\. Make sure that you remove the trailing forward slash at the end of the URL\. Also, in the previous procedure you copied the **Access token** value in AWS SSO\. Paste that value into the **ACCESS\_TOKEN** field in the PingOne AWS Single Sign\-On application\.

1. For **REMOVE\_ACTION**, choose either **Disabled** or **Deleted** \(see the description text on the page for more details\)\.

1. On the **Attribute Mapping** page, choose a value to use for the **SAML\_SUBJECT** \(`NameId`\) assertion, following guidance from [Additional considerations](#pingone-considerations) earlier on this page\. Then choose **Continue to Next Step**\.

1. On the **PingOne App Customization \- AWS Single Sign\-On** page, make any desired customization changes \(optional\), and click **Continue to Next Step**\.

1. On the **Group Access** page, choose the groups containing the users you would like to enable for provisioning and single sign\-on to AWS SSO\. Choose **Continue to Next Step**\.

1. Scroll to the bottom of the page, and choose **Finish** to start provisioning\.

1. To verify that users have been successfully synchronized to AWS SSO, return to the AWS SSO console and choose **Users**\. Synchronized users from PingOne will appear on the **Users** page\. These users can now be assigned to accounts and applications within AWS SSO\.

   Remember that PingOne does not support provisioning of groups or group memberships through SCIM\. Contact Ping for more information\.

## \(Optional\) Step 3: Configure user attributes in PingOne for access control in AWS SSO<a name="pingone-step3"></a>

This is an optional procedure for PingOne should you choose to configure attributes for AWS SSO to manage access to your AWS resources\. The attributes that you define in PingOne will be passed in a SAML assertion to AWS SSO\. You then create a permission set in AWS SSO to manage access based on the attributes you passed from PingOne\.

Before you begin this procedure, you must first enable the [Attributes for access control](attributesforaccesscontrol.md) feature\. For more information about how to do this, see [Enable and configure attributes for access control](configure-abac.md)\.

**To configure user attributes in PingOne for access control in AWS SSO**

1. Open the PingOne AWS Single Sign\-On application that you installed as part of configuring SAML for PingOne \(**Applications > My Applications**\)\.

1. Choose **Edit**, and then choose **Continue to Next Step** until you get to the **Attribute Mappings** page\. 

1. On the **Attribute Mappings** page, choose **Add new attribute**, and then do the following\. You must perform these steps for each attribute you will add for use in AWS SSO for access control\.

   1. In the **Application Attribute** field, enter `https://aws.amazon.com/SAML/Attributes/AccessControl:AttributeName`\. Replace *AttributeName* with the name of the attribute you are expecting in AWS SSO\. For example, `https://aws.amazon.com/SAML/Attributes/AccessControl:Email`\.

   1. In the **Identity Bridge Attribute or Literal Value** field, choose user attributes from your PingOne directory\. For example, **Email \(Work\)**\.

1. Choose **Next** a few times, and then choose **Finish**\.

## \(Optional\) Passing attributes for access control<a name="pingone-passing-abac"></a>

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
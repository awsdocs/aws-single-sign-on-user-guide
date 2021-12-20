# OneLogin<a name="onelogin-idp"></a>

AWS SSO supports automatic provisioning \(synchronization\) of user and group information from OneLogin into AWS SSO using the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. You configure this connection in OneLogin, using your SCIM endpoint for AWS SSO and a bearer token that is created automatically by AWS SSO\. When you configure SCIM synchronization, you create a mapping of your user attributes in OneLogin to the named attributes in AWS SSO\. This causes the expected attributes to match between AWS SSO and OneLogin\. 

The following steps walk you through how to enable automatic provisioning of users and groups from OneLogin to AWS SSO using the SCIM protocol\.

**Note**  
Before you begin deploying SCIM, we recommend that you first review the [Considerations for using automatic provisioning](provision-automatically.md#auto-provisioning-considerations)\.

**Topics**
+ [Prerequisites](#onelogin-prereqs)
+ [Step 1: Enable provisioning in AWS SSO](#onelogin-step1)
+ [Step 2: Configure provisioning in OneLogin](#onelogin-step2)
+ [\(Optional\) Step 3: Configure user attributes in OneLogin for access control in AWS SSO](#onelogin-step3)
+ [\(Optional\) Passing attributes for access control](#onelogin-passing-abac)
+ [Troubleshooting](#onelogin-troubleshooting)

## Prerequisites<a name="onelogin-prereqs"></a>

You will need the following before you can get started:
+ A OneLogin account\. If you do not have an existing account, you may be able to obtain a free trial or developer account from the [OneLogin website](https://www.onelogin.com/free-trial)\.
+ An AWS SSO\-enabled account \([free](https://aws.amazon.com/single-sign-on/)\)\. For more information, see [Enable AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/step1.html)\.
+ A SAML connection from your OneLogin account to AWS SSO\. For more information, see [Enabling Single Sign\-On Between OneLogin and AWS](https://aws.amazon.com/blogs/apn/enabling-single-sign-on-between-onelogin-and-aws/) on the AWS Partner Network Blog\.

## Step 1: Enable provisioning in AWS SSO<a name="onelogin-step1"></a>

In this first step, you use the AWS SSO console to enable automatic provisioning\.

**To enable automatic provisioning in AWS SSO**

1. After you have completed the prerequisites, open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under **Identity source**, next to **Provisioning**, choose **Enable automatic provisioning**\. This immediately enables automatic provisioning in AWS SSO and displays the necessary endpoint and access token information\.

1. In the **Inbound automatic provisioning** dialog box, copy each of the values for the following options\. You will need to paste these in later when you configure provisioning in your IdP\.

   1. **SCIM endpoint**

   1. **Access token**

1. Choose **Close**\.

You have now set up provisioning in the AWS SSO console\. Now you need to do the remaining tasks using the OneLogin admin console as described in the following procedure\.

## Step 2: Configure provisioning in OneLogin<a name="onelogin-step2"></a>

Use the following procedure in the OneLogin admin console to enable integration between AWS SSO and the AWS Single Sign\-On app\. This procedure assumes you have already configured the AWS Single Sign\-On application in OneLogin for SAML authentication\. If you have not yet created this SAML connection, please do so before proceeding and then return here to complete the SCIM provisioning process\. For more information about configuring SAML with OneLogin, see [Enabling Single Sign\-On Between OneLogin and AWS](https://aws.amazon.com/blogs/apn/enabling-single-sign-on-between-onelogin-and-aws/) on the AWS Partner Network Blog\.

**To configure provisioning in OneLogin**

1. Sign in to OneLogin, and then navigate to **Applications > Applications**\. 

1. On the **Applications** page, search for the application you created previously to form your SAML connection with AWS SSO\. Choose it and then choose **Configuration** from the left navigation bar\.

1. In the previous procedure, you copied the **SCIM endpoint** value in AWS SSO\. Paste that value into the **SCIM Base URL** field in OneLogin\. Make sure that you remove the trailing forward slash at the end of the URL\. Also, in the previous procedure you copied the **Access token** value in AWS SSO\. Paste that value into the **SCIM Bearer Token** field in OneLogin\.

1. Next to **API Connection**, click **Enable**, and then click **Save** to complete the configuration\.

1. In the left navigation bar, choose **Provisioning**\.

1. Select the check boxes for **Enable provisioning**, **Create user**, **Delete user**, and **Update user**, and then choose **Save**\.

1. In the left navigation bar, choose **Users**\.

1. Click **More Actions** and choose **Sync logins**\. You should receive the message *Synchronizing users with AWS Single Sign\-on*\.

1. Click **More Actions** again, and then choose **Reapply entitlement mappings**\. You should receive the message *Mappings are being reapplied*\.

1. At this point, the provisioning process should begin\. To confirm this, navigate to **Activity > Events**, and monitor the progress\. Successful provisioning events, as well as errors, should appear in the event stream\.

1. To verify that your users and groups have all been successfully synchronized to AWS SSO, return to the AWS SSO console and choose **Users**\. Your synchronized users from OneLogin will appear on the **Users** page\. You can also view your synchronized groups on the **Groups** page\.

1. To synchronize user changes automatically to AWS SSO, navigate to the **Provisioning** page, locate the **Require admin approval before this action is performed** section, de\-select **Create User**, **Delete User**, and/or **Update User**, and click **Save**\.

## \(Optional\) Step 3: Configure user attributes in OneLogin for access control in AWS SSO<a name="onelogin-step3"></a>

This is an optional procedure for OneLogin should you choose to configure attributes you will use in AWS SSO to manage access to your AWS resources\. The attributes that you define in OneLogin will be passed in a SAML assertion to AWS SSO\. You will then create a permission set in AWS SSO to manage access based on the attributes you passed from OneLogin\.

Before you begin this procedure, you must first enable the [Attributes for access control](attributesforaccesscontrol.md) feature\. For more information about how to do this, see [Enable and configure attributes for access control](configure-abac.md)\.

**To configure user attributes in OneLogin for access control in AWS SSO**

1. Sign in to OneLogin, and then navigate to **Applications > Applications**\.

1. On the **Applications** page, search for the application you created previously to form your SAML connection with AWS SSO\. Choose it and then choose **Parameters** from the left navigation bar\. 

1. In the **Required Parameters** section, do the following for each attribute you want to use in AWS SSO:

   1. Choose **\+**\.

   1. In **Field name**, enter `https://aws.amazon.com/SAML/Attributes/AccessControl:AttributeName`, and replace **AttributeName** with the name of the attribute you are expecting in AWS SSO\. For example, `https://aws.amazon.com/SAML/Attributes/AccessControl:Department`\. 

   1. Under **Flags**, check the box next to **Include in SAML assertion**, and choose **Save**\.

   1. In the **Value** field, use the drop\-down list to choose the OneLogin user attributes\. For example, **Department**\. 

1. Choose **Save**\.

## \(Optional\) Passing attributes for access control<a name="onelogin-passing-abac"></a>

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

## Troubleshooting<a name="onelogin-troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter while setting up automatic provisioning with OneLogin\.

**Groups are not provisioned to AWS SSO**

By default, groups may not be provisioned from OneLogin to AWS SSO\. Ensure that you’ve enabled group provisioning for your AWS SSO application in OneLogin\. To do this, sign in to the OneLogin admin console, and check to make sure that the **Include in User Provisioning** option is selected under the properties of the AWS SSO application \(**AWS SSO application > Parameters > Groups**\)\. For more details on how to create groups in OneLogin, including how to synchronize OneLogin roles as groups in SCIM, please see the [OneLogin website](https://onelogin.service-now.com/support)\.

**Nothing is synchronized from OneLogin to AWS SSO, despite all settings being correct**

In addition to the note above regarding admin approval, you will need to **Reapply entitlement mappings** for many configuration changes to take effect\. This can be found in **Applications > Applications > AWS SSO application > More Actions**\. You can see details and logs for most actions in OneLogin, including synchronization events, under **Activity > Events**\.

**I’ve deleted or disabled a group in OneLogin, but it still appears in AWS SSO**

OneLogin currently does not support the SCIM DELETE operation for groups, which means that the group will continue to exist in AWS SSO\. You must therefore remove the group from AWS SSO directly to ensure that any corresponding permissions in AWS SSO for that group are removed\.

**I deleted a group in AWS SSO without first deleting it from OneLogin and now I’m having user/group sync issues**

To remedy this situation, first ensure that you do not have any redundant group provisioning rules or configurations in OneLogin\. For example, a group directly assigned to an application along with a rule that publishes to the same group\. Next, delete any undesirable groups in AWS SSO\. Finally, in OneLogin, **Refresh** the entitlements \(**AWS SSO App > Provisioning > Entitlements**\), and then **Reapply entitlement mappings \(AWS SSO App > More Actions\)**\. To avoid this issue in the future, first make the change to stop provisioning the group in OneLogin, then delete the group from AWS SSO\.
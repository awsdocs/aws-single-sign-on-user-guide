# Azure AD<a name="azure-ad-idp"></a>

IAM Identity Center supports automatic provisioning \(synchronization\) of user and group information from Azure AD into IAM Identity Center using the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. You configure this connection in Azure AD using your SCIM endpoint for IAM Identity Center and a bearer token that is created automatically by IAM Identity Center\. When you configure SCIM synchronization, you create a mapping of your user attributes in Azure AD to the named attributes in IAM Identity Center\. This causes the expected attributes to match between IAM Identity Center and your IdP\. 

The following steps walk you through how to enable automatic provisioning of users and groups from Azure AD to IAM Identity Center using the IAM Identity Center app in the Azure AD Application Gallery and the SCIM protocol\.

**Note**  
Before you begin deploying SCIM, we recommend that you first review [Considerations for using automatic provisioning](provision-automatically.md#auto-provisioning-considerations), and then continue reviewing [Prerequisites](#azure-ad-prereqs) and [Additional considerations](#azure-ad-considerations) in the next sections\.

## Prerequisites<a name="azure-ad-prereqs"></a>

You will need the following before you can get started:
+ An Azure AD tenant\. For more information, see [Quickstart: Set up a tenant](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-create-new-tenant) on Microsoft's website\.
+ An IAM Identity Center\-enabled account \([free](https://aws.amazon.com/single-sign-on/)\)\. For more information, see [Enable IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/step1.html)\.
+ A SAML connection from your Azure AD account to IAM Identity Center, as described in [Tutorial: Azure Active Directory single sign\-on \(SSO\) integration with IAM Identity Center](https://aka.ms/AWSSSOSAML) on Microsoft's website\.
**Important**  
Make sure that all users in Azure AD have filled out **First name**, **Last name**, and **Display name** values in their user properties\. Otherwise, automatic provisioning won't work with Azure AD\.

## Additional considerations<a name="azure-ad-considerations"></a>

Attributes for access control are used in permission policies that determine who in your identity source can access your AWS resources\. If an attribute is removed from a user in Azure AD, that attribute will not be removed from the corresponding user in IAM Identity Center\. This is a known limitation in Azure AD\. If an attribute is changed to a different \(non\-empty\) value on a user, that change will be synchronized to IAM Identity Center\.

## Step 1: Set up IAM Identity Center and configure automatic provisioning<a name="azure-ad-step1"></a>

To get started, you'll need to first follow the instructions in [Tutorial: Configure AWS Single Sign\-On for automatic user provisioning](https://aka.ms/AWSSSOProv)\. These instructions walk you through the following:
+ Enable IAM Identity Center\.
+ Install the IAM Identity Center app from the Azure AD Application Gallery\.
+ Configure automatic provisioning \(SCIM\) within the Azure portal\.

## Step 2: \(Optional\) Configure attribute\-based access control<a name="azure-ad-step2"></a>

Now that you have configured Azure AD to work with IAM Identity Center, you can optionally choose to configure attribute\-based access control \(ABAC\)\. ABAC is an authorization strategy that defines permissions based on attributes\.

With Azure AD, you have two different ways to configure ABAC for use with IAM Identity Center\. Choose either of the following methods\.

### Method 1: Configure ABAC using Azure AD<a name="azure-ad-step2-method1"></a>

This method can be used when you need to define which attributes in Azure AD can be used by IAM Identity Center to manage access to your AWS resources\. Once defined, Azure AD sends these attributes to IAM Identity Center through SAML assertions\. You will then need to [Create a permission set](howtocreatepermissionset.md) in IAM Identity Center to manage access based on the attributes you passed from Azure AD\.

Before you begin this procedure, you first need to enable the [Attributes for access control](attributesforaccesscontrol.md) feature\. For more information about how to do this, see [Enable and configure attributes for access control](configure-abac.md)\.

**To configure user attributes in Azure AD for access control in IAM Identity Center**

1. While signed into the Azure portal, navigate to **Azure Active Directory**, **Enterprise applications**\. Search for the name of the application that you created previously to form your SAML connection\. Then choose the application\.

1. Choose **Single sign\-on**\. 

1. In the **User Attributes & Claims** section, choose **Edit**\.

1. On the **User Attributes & Claims** page, do the following:

   1. Choose **Add new claim**

   1. For **Name**, enter `AccessControl:AttributeName`\. Replace **AttributeName** with the name of the attribute you are expecting in IAM Identity Center\. For example, `AccessControl:Department`\. 

   1. For **Namespace**, enter **https://aws\.amazon\.com/SAML/Attributes**\. 

   1. For **Source**, choose **Attribute**\. 

   1. For **Source attribute**, use the drop\-down list to choose the Azure AD user attributes\. For example, `user.department`\.

1. Repeat the previous step for each attribute you need to send to IAM Identity Center in the SAML assertion\.

1. Choose **Save**\.

### Method 2: Configure ABAC using IAM Identity Center<a name="azure-ad-step2-method2"></a>

With this method, you use the [Attributes for access control](attributesforaccesscontrol.md) feature in IAM Identity Center to pass an `Attribute` element with the `Name` attribute set to `https://aws.amazon.com/SAML/Attributes/AccessControl:{TagKey}`\. You can use this element to pass attributes as session tags in the SAML assertion\. For more information about session tags, see [Passing session tags in AWS STS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_session-tags.html) in the *IAM User Guide*\.

To pass attributes as session tags, include the `AttributeValue` element that specifies the value of the tag\. For example, to pass the tag key\-value pair `CostCenter = blue`, use the following attribute:

```
<saml:AttributeStatement>
<saml:Attribute Name="https://aws.amazon.com/SAML/Attributes/AccessControl:CostCenter">
<saml:AttributeValue>blue
</saml:AttributeValue>
</saml:Attribute>
</saml:AttributeStatement>
```

If you need to add multiple attributes, include a separate `Attribute` element for each tag\. 

## Troubleshooting<a name="azure-ad-troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter while setting up automatic provisioning with Azure AD\.

**Azure AD users are not synchronizing to IAM Identity Center**

This might be due to a syntax issue that IAM Identity Center has flagged when a new user is being added to IAM Identity Center\. You can confirm this by checking the Azure audit logs for failed events, such as an `'Export'`\. The **Status Reason** for this event will state:

```
{"schema":["urn:ietf:params:scim:api:messages:2.0:Error"],"detail":"Request is unparsable, syntactically incorrect, or violates schema.","status":"400"}
```

You can also check AWS CloudTrail for the failed event\. This can be done by searching in the **Event History** console of CloudTrail using the following filter:

```
"eventName":"CreateUser"
```

The error in the CloudTrail event will state the following:

```
"errorCode": "ValidationException",
        "errorMessage": "Currently list attributes only allow single item“
```

Ultimately, this exception means that one of the values passed from Azure contained more values than anticipated\. The solution here is to review the attributes of the user in Azure AD, ensuring that none contain duplicate values\. One common example of duplicate values is having multiple values present for contact numbers such as **mobile**, **work**, and **fax**\. Although separate values, they are all passed to IAM Identity Center under the single parent attribute **phoneNumbers**\.
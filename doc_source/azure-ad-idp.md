# Azure AD<a name="azure-ad-idp"></a>

AWS SSO supports automatic provisioning \(synchronization\) of user and group information from Azure AD into AWS SSO using the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. You configure this connection in Azure AD using your SCIM endpoint for AWS SSO and a bearer token that is created automatically by AWS SSO\. When you configure SCIM synchronization, you create a mapping of your user attributes in Azure AD to the named attributes in AWS SSO\. This causes the expected attributes to match between AWS SSO and your IdP\. 

The following steps walk you through how to enable automatic provisioning of users and groups from Azure AD to AWS SSO using the SCIM protocol\.

**Note**  
Before you begin deploying SCIM, we recommend that you first review [Considerations for Using Automatic Provisioning](provision-automatically.md#auto-provisioning-considerations)\.

## Prerequisites<a name="azure-ad-prereqs"></a>

You will need the following before you can get started:
+ An Azure AD tenant
+ An AWS SSO\-enabled account \([free](https://aws.amazon.com/single-sign-on/)\)\. For more information, see [Enable AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/step1.html)\.
+ A SAML connection from your Azure AD account to AWS SSO\. For an example showing how to set this up, see [The Next Evolution in AWS Single Sign\-On](https://aws.amazon.com/blogs/aws/the-next-evolution-in-aws-single-sign-on/) on the AWS Security Blog\.
**Important**  
Make sure that all users in Azure AD have filled out **First name**, **Last name**, and **Display name** values in their user properties\. Otherwise, automatic provisioning won't work with Azure AD\.

## Step 1: Enable Provisioning in AWS SSO<a name="azure-ad-step1"></a>

In this first step, you will use the AWS SSO console to enable automatic provisioning\.

**To enable automatic provisioning in AWS SSO**

1. After you have completed the prerequisites, open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under **Identity source > Provisioning**, choose **Enable automatic provisioning**\. This immediately enables automatic provisioning in AWS SSO and displays the necessary endpoint and access token information\.

1. In the **Inbound automatic provisioning** dialog box, copy each of the values for the following options\. You will need to paste these in later when you configure provisioning in your IdP\.

   1. **SCIM endpoint**

   1. **Access token**

1. Choose **Close**\.

Now that you have set up provisioning in the AWS SSO console, you need to do the remaining tasks using the Azure AD user interface as described in the procedures below\.

## Step 2: Configure User Provisioning in Azure AD<a name="azure-ad-step2"></a>

This procedure assumes you have already configured Azure AD to use a nongallery application for AWS SSO to form a SAML connection\. If you have not yet created this SAML connection, please refer to the instructions in [The Next Evolution in AWS Single Sign\-On](https://aws.amazon.com/blogs/aws/the-next-evolution-in-aws-single-sign-on/) on the AWS Security Blog, and then return here to complete this step to configure SCIM provisioning\.

**To configure user provisioning in Azure AD**

1. Sign into the Azure Portal, and then navigate to **Azure Active Directory > Enterprise applications**\.

1. On the **Enterprise applications \| All applications** page, search for the name of the application you created previously to form your SAML connection, and then select it\.

1. On the **Overview** page, choose **Provision User Accounts**\. 

1. On the **Provisioning** page, if provisioning has not yet been enabled you will need to choose **Get started**\. Otherwise next to **Provisioning Mode**, select **Automatic**\.

1. Under the **Admin Credentials** section, In the previous procedure you copied the **SCIM endpoint** value in AWS SSO\. Paste that value into the **Tenant URL** field in Azure AD\. In the previous procedure you copied the **Access token** value in AWS SSO\. Paste that value into the **Secret Token** field in Azure AD\.

1. Choose **Test Connection** to check that Azure AD can connect to your AWS SSO app\. If the connection fails, ensure that you copied the correct SCIM endpoint and OAuth bearer token from the AWS SSO console, and then try selecting **Test Connection** again\.

1. Next to **Notification Email**, type the email address of a person or group that you want to receive provisioning error notifications, select the **Send an email notification when a failure occurs** check box, and then choose **Save**\.

1. Under the **Mappings** section, select **Provision Azure Active Directory Users**\.

1. On the **Attibute Mapping** page, delete the mappings for the two attributes **facsimileTelephoneNumber** and **mobile**\. Choose **mailNickname** in the attribute table, under **Edit Attribute**, change **Source attribute** from **mailNickname** to **objectId**, and then choose** OK**\. Choose **Save** to commit your changes\. The attributes selected here are now set to match to the user accounts in AWS SSO\.

1. Go back to the **Provisioning** page\. Under the **Settings** section, next to **Provisioning Status** choose the **On** option to enable provisioning, and then choose **Save**\.

The initial Azure AD sync is triggered immediately after you turn on provisioning and have assigned user access \(next step\)\. The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 to 40 minutes depending on the number of users and groups in the application\. Once the initial sync completes, you can go into AWS SSO and start managing your assignments\. 

By default, no users or groups are assigned to your application so you will need to complete the next procedure to begin synchronizing them to AWS SSO\.

## Step 3: Assign Access for Users and Groups in Azure AD<a name="azure-ad-step3"></a>

Use the following procedures in Azure AD to assign access to your users and groups\. All Azure AD users that belong to groups that you assign here will also be synchronized automatically to AWS SSO\. To minimize administrative overhead in both Azure AD and AWS SSO, we recommend that you assign groups instead of individual users\.

After you complete this step and the first synchronization with SCIM has completed, the users and groups you've assigned will appear in AWS SSO, and will be able to access the AWS SSO user portal using their Azure AD credentials\. 

**To assign access for users and groups in Azure AD**

1. While signed into the Azure Portal, navigate to **Azure Active Directory > Enterprise applications**, search for the name of the application you created previously to form your SAML connection, and then select it\.

1. Choose Users and groups\. 

1. On the **Users and groups** page, choose **Add user**\.

1. On the **Add Assignment** page, choose **Users**, and then under **Users** type the name of the user\(s\) that you want to add, select each of the users, choose **Select**, and then choose **Assign**\. This will start the process of provisioning the users into AWS SSO\. 

You can verify that the provisioning process completed successfully by viewing your Azure AD users within AWS SSO\. To do this in the AWS SSO console, go to the **Users** page\. If it was successful, you would see that the Azure AD users are now showing up in the AWS SSO console\. In Azure portal, you also can use the **Provisioning** page to monitor the sync progress and to also follow links to the provisioning activity logs\. The audit logs describe all actions performed by the provisioning service on your AWS SSO app\. For more information on how to read the Azure AD provisioning logs, see [Report on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/check-status-user-account-provisioning)\.

## Troubleshooting<a name="azure-ad-troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter while setting up automatic provisioning with Azure AD\.

**Azure AD users are not synchronizing to AWS SSO**

This might be due to a syntax issue that AWS SSO has flagged when a new user is being added to AWS SSO\. You can confirm this by checking the Azure audit logs for failed events, such as an 'Export'\. The **Status Reason** for this event will state:

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

Ultimately, this exception means that one of the values passed from Azure contained more values than anticipated\. The solution here is to review the attributes of the user in Azure AD, ensuring that none contain duplicate values\. One common example of duplicate values is having multiple values present for contact numbers such as **mobile**, **work**, and **fax**\. Although separate values, they are all passed to AWS SSO under the single parent attribute **phoneNumbers**\.
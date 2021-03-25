# PingFederate<a name="pingfederate-idp"></a>

AWS SSO supports automatic provisioning \(synchronization\) of user and group information from the PingFederate product by Ping Identity \(hereafter “Ping”\) into AWS SSO\. This provisioning uses the System for Cross\-domain Identity Management \(SCIM\) v2\.0 protocol\. You configure this connection in PingFederate using your AWS SSO SCIM endpoint and access token\. When you configure SCIM synchronization, you create a mapping of your user attributes in PingFederate to the named attributes in AWS SSO\. This causes the expected attributes to match between AWS SSO and PingFederate\.

This guide is based on PingFederate version 10\.2\. Steps for other versions may vary\. Contact Ping for more information about how to configure provisioning to AWS SSO for other versions of PingFederate\. 

The following steps walk you through how to enable automatic provisioning of users and groups from PingFederate to AWS SSO using the SCIM protocol\.

**Note**  
Before you begin deploying SCIM, we recommend that you first review the [Considerations for using automatic provisioning](provision-automatically.md#auto-provisioning-considerations)\. Then continue reviewing additional considerations in the next section\.

**Topics**
+ [Prerequisites](#pingfederate-prereqs)
+ [Additional considerations](#pingfederate-considerations)
+ [Step 1: Enable provisioning in AWS SSO](#pingfederate-step1)
+ [Step 2: Configure provisioning in PingFederate](#pingfederate-step2)
+ [\(Optional\) Step 3: Configure user attributes in PingFederate for access control in AWS SSO](#pingfederate-step3)
+ [\(Optional\) Passing attributes for access control](#pingfederate-passing-abac)

## Prerequisites<a name="pingfederate-prereqs"></a>

You will need the following before you can get started:
+ A working PingFederate server\. If you do not have an existing PingFederate server, you might be able to obtain a free trial or developer account from the [Ping Identity](https://www.pingidentity.com/developer/en/get-started.html#:~:text=Get%20started%20developing%20with%20open,a%20developer%20trial%20of%20PingOne.) website\. The trial includes licenses and software downloads and associated documentation\.
+ A copy of the PingFederate AWS Single Sign\-On Connector software installed on your PingFederate server\. For more information about how to obtain this software, see [AWS Single Sign\-On Connector](https://support.pingidentity.com/s/marketplace-integration/a7i1W000000TOZ1/) on the Ping Identity website\.
+ An AWS SSO\-enabled account \([free](https://aws.amazon.com/single-sign-on/)\)\. For more information, see [Enable AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/step1.html)\.
+ A SAML connection from your PingFederate instance to AWS SSO\. For instructions on how to configure this connection, see the PingFederate documentation\. In summary, the recommended path is to use the AWS Single Sign\-On Connector to configure "Browser SSO" in PingFederate, using the “download" and "import" metadata features on both ends to exchange SAML metadata between PingFederate and AWS SSO\.

## Additional considerations<a name="pingfederate-considerations"></a>

The following are important considerations about PingFederate that can affect how you implement provisioning with AWS SSO\.
+ If an attribute \(such as a phone number\) is removed from a user in the data store configured in PingFederate, that attribute will not be removed from the corresponding user in AWS SSO\. This is a known limitation in PingFederate’s provisioner implementation\. If an attribute is changed to a different \(non\-empty\) value on a user, that change will be synchronized to AWS SSO\.

## Step 1: Enable provisioning in AWS SSO<a name="pingfederate-step1"></a>

In this first step, you use the AWS SSO console to enable automatic provisioning\.

**To enable automatic provisioning in AWS SSO**

1. After you have completed the prerequisites, open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings** in the left navigation pane\.

1. On the **Settings** page, under **Identity source**, next to **Provisioning**, choose **Enable automatic provisioning**\. This immediately enables automatic provisioning in AWS SSO and displays the necessary endpoint and access token information\.

1. In the **Inbound automatic provisioning** dialog box, copy each of the values for the following options\. You will need to paste these in later when you configure provisioning in your IdP\.

   1. **SCIM endpoint**

   1. **Access token**

1. Choose **Close**\.

Now that you have set up provisioning in the AWS SSO console, you must complete the remaining tasks using the PingFederate administrative console\., The steps are described in the following procedure\. 

## Step 2: Configure provisioning in PingFederate<a name="pingfederate-step2"></a>

Use the following procedure in the PingFederate administrative console to enable integration between AWS SSO and the AWS Single Sign\-On Connector\. This procedure assumes that you have already installed the AWS Single Sign\-On Connector software\. If you have not yet done so, refer to [Prerequisites](#pingfederate-prereqs), and then complete this procedure to configure SCIM provisioning\. 

**Important**  
If your PingFederate server has not been previously configured for outbound SCIM provisioning, you may need to make a configuration file change to enable provisioning\. For more information, see Ping documentation\. In summary, you must modify the `pf.provisioner.mode` setting in the **pingfederate\-<version>/pingfederate/bin/run\.properties** file to a value other than `OFF` \(which is the default\), and restart the server if currently running\. For example, you may choose to use `STANDALONE` if you don’t currently have a high\-availability configuration with PingFederate\.

**To configure provisioning in PingFederate**

1. Sign on to the PingFederate administrative console\.

1. Select **Applications** from the top of the page, then click **SP Connections**\.

1. Locate the application you created previously to form your SAML connection with AWS SSO, and click on the connection name\. 

1. Select **Connection Type** from the dark navigation headings near the top of the page\. You should see **Browser SSO** already selected from your previous configuration of SAML\. If not, you must complete those steps first before you can continue\. 

1. Select the **Outbound Provisioning** check box, choose **AWS SSO Cloud Connector** as the type, and click **Save**\. If **AWS SSO Cloud Connector** does not appear as an option, ensure that you have installed the AWS Single Sign\-On Connector and have restarted your PingFederate server\.

1. Click **Next** repeatedly until you arrive on the **Outbound Provisioning** page, and then click the **Configure Provisioning** button\.

1. In the previous procedure, you copied the **SCIM endpoint** value in AWS SSO\. Paste that value into the **SCIM URL** field in the PingFederate console\. Make sure that you remove the trailing forward slash at the end of the URL\. Also, in the previous procedure you copied the **Access token** value in AWS SSO\. Paste that value into the **Access Token** field in the PingFederate console\. Click **Save**\.

1. On the **Channel Configuration \(Configure Channels\)** page, click **Create**\.

1. Enter a **Channel Name** for this new provisioning channel \(such as **AWSSSOchannel**\), and click **Next**\.

1. On the **Source** page, choose the **Active Data Store** you want to use for your connection to AWS SSO, and click **Next**\.
**Note**  
If you have not yet configured a data source, you must do so now\. See the Ping product documentation for information on how to choose and configure a data source in PingFederate\.

1. On the **Source Settings** page, confirm all values are correct for your installation, then click **Next**\.

1. On the **Source Location** page, enter settings appropriate to your data source, and then click **Next**\. For example, if using Active Directory as an LDAP directory:

   1. Enter the **Base DN** of your AD forest \(such as **DC=myforest,DC=mydomain,DC=com**\)\.

   1. In **Users > Group DN**, specify a single group that contains all of the users that you want to provision to AWS SSO\. If no such single group exists, create that group in AD, return to this setting, and then enter the corresponding DN\.

   1. Specify whether to search subgroups \(**Nested Search**\), and any required LDAP **Filter**\.

   1. In **Groups > Group DN**, specify a single group that contains all of the groups that you want to provision to AWS SSO\. In many cases, this may be the same DN as you specified in the **Users** section\. Enter **Nested Search** and **Filter** values as required\.

1. On the **Attribute Mapping** page, ensure the following, and then click **Next**:

   1. The **userName** field must be mapped to an **Attribute** that is formatted as an email \(user@domain\.com\)\. It must also match the value that the user will use to log in to Ping\. This value in turn is populated in the SAML `nameId` claim during federated authentication and used for matching to the user in AWS SSO\. For example, when using Active Directory, you may choose to specify the `UserPrincipalName` as the **userName**\.

   1. Other fields suffixed with a **\*** must be mapped to attributes that are non\-null for your users\.

1. On the **Activation & Summary** page, set the **Channel Status** to **Active** to cause the synchronization to start immediately after the configuration is saved\.

1. Confirm that all configuration values on the page are correct, and click **Done**\.

1. On the **Manage Channels** page, click **Save**\.

1. At this point, provisioning will start\. To confirm activity, you can view the **provisioner\.log** file, located by default in the **pingfederate\-<version>/pingfederate/log** directory on your PingFederate server\.

1. To verify that users and groups have been successfully synchronized to AWS SSO, return to the AWS SSO Console and choose **Users**\. Synchronized users from PingFederate will appear on the **Users** page\. You can also view synchronized groups on the **Groups** page\.

## \(Optional\) Step 3: Configure user attributes in PingFederate for access control in AWS SSO<a name="pingfederate-step3"></a>

This is an optional procedure for PingFederate should you choose to configure attributes you will use in AWS SSO to manage access to your AWS resources\. The attributes that you define in PingFederate will be passed in a SAML assertion to AWS SSO\. You will then create a permission set in AWS SSO to manage access based on the attributes you passed from PingFederate\.

Before you begin this procedure, you must first enable the [Attributes for access control](attributesforaccesscontrol.md) feature\. For more information about how to do this, see [Enable and configure attributes for access control](configure-abac.md)\.

**To configure user attributes in PingFederate for access control in AWS SSO**

1. Sign on to the PingFederate administrative console\.

1. Choose **Applications** from the top of the page, then click **SP Connections**\. 

1. Locate the application you created previously to form your SAML connection with AWS SSO, and click on the connection name\. 

1. Choose **Browser SSO** from the dark navigation headings near the top of the page\. Then click on **Configure Browser SSO**\.

1. On the **Configure Browser SSO** page, choose **Assertion Creation**, and then click on **Configure Assertion Creation**\.

1. On the **Configure Assertion Creation** page, choose **Attribute Contract**\.

1. On the **Attribute Contract** page, under **Extend the Contract** section, add a new attribute by performing the following steps:

   1. In the text box, enter `https://aws.amazon.com/SAML/Attributes/AccessControl:AttributeName`, replace **AttributeName** with the name of the attribute you are expecting in AWS SSO\. For example, `https://aws.amazon.com/SAML/Attributes/AccessControl:Department`\. 

   1. For **Attribute Name Format**, choose **urn:oasis:names:tc:SAML:2\.0:attrname\-format:uri**\.

   1. Choose **Add**, and then choose **Next**\.

1. On the **Authentication Source Mapping** page, choose the Adapter Instance configured with your application\. 

1. On the **Attribute Contract Fulfillment** page, choose the **Source** \(*data store*\) and **Value** \(*data store attribute*\) for the **Attribute Contract** `https://aws.amazon.com/SAML/Attributes/AccessControl:Department`\.
**Note**  
If you have not yet configured a data source, you will need to do so now\. See the Ping product documentation for information on how to choose and configure a data source in PingFederate\.

1. Click **Next** repeatedly until you arrive on the **Activation & Summary** page, and then click **Save**\.

## \(Optional\) Passing attributes for access control<a name="pingfederate-passing-abac"></a>

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
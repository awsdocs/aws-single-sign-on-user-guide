# Connect to an external identity provider<a name="manage-your-identity-source-idp"></a>

If you're using a self\-managed directory in Active Directory or an AWS Managed Microsoft AD, see [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)\. For other external identity providers \(IdPs\), you can use AWS IAM Identity Center \(successor to AWS Single Sign\-On\) to authenticate identities from the IdPs through the Security Assertion Markup Language \(SAML\) 2\.0 standard\. This enables your users to sign in to the AWS access portal with their corporate credentials\. They can then navigate to their assigned accounts, roles, and applications hosted in external IdPs\.

For example, you can connect an external IdP such as Okta or Azure Active Directory \(AD\), to IAM Identity Center\. Your users can then sign in to the AWS access portal with their existing Okta or Azure credentials\. In addition, you can assign access permissions centrally for your users across all the accounts and applications in your AWS organization\. In addition, developers can simply sign in to the AWS Command Line Interface \(AWS CLI\) using their existing credentials, and benefit from automatic short\-term credential generation and rotation\.

The SAML protocol does not provide a way to query the IdP to learn about users and groups\. Therefore, you must make IAM Identity Center aware of those users and groups by provisioning them into IAM Identity Center\.

## Provisioning when users come from an external IdP<a name="provisioning-when-external-idp"></a>

When using an external IdP, you must provision all users and groups into IAM Identity Center before you can make any assignments to AWS accounts or applications\. In this case, you can: You can configure [Automatic provisioning](provision-automatically.md), or you can configure [Manual provisioning](provision-manually.md) of your users and groups\. Regardless of how you provision users, IAM Identity Center redirects the AWS Management Console, command line interface, and application authentication to your external IdP\. IAM Identity Center then grants access to those resources based on policies you create in IAM Identity Center\. For more information about provisioning, see [User and group provisioning](users-groups-provisioning.md#user-group-provision)\.

## How to connect to an external identity provider<a name="how-to-connect-idp"></a>

Use the following procedure to connect to an external identity provider from the IAM Identity Center console\.

**To connect to an external identity provider**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, and then choose **Actions > Change identity source**\.

1. Under **Choose identity source**, select **External identity provider**, and then choose **Next**\. 

1. Under **Configure external identity provider**, do the following:

   1. Under **Service provider metadata**, choose **Download metadata file** to download the metadata file and save it on your system\. The IAM Identity Center SAML metadata file is required by your external identity provider\.

   1. Under **Identity provider metadata**, choose **Choose file**, and locate the metadata file that you downloaded from your external identity provider\. Then upload the file\. This metadata file contains the necessary public x509 certificate used to trust messages that are sent from the IdP\.

   1. Choose **Next**\.
**Important**  
Changing your source to or from Active Directory removes all existing user and group assignments\. You must manually reapply assignments after you have successfully changed your source\.

1. After you read the disclaimer and are ready to proceed, enter **ACCEPT**\.

1. Choose **Change identity source**\.

**Topics**
+ [Provisioning when users come from an external IdP](#provisioning-when-external-idp)
+ [How to connect to an external identity provider](#how-to-connect-idp)
+ [SCIM profile and SAML 2\.0 implementation](scim-profile-saml.md)
+ [Supported identity providers](supported-idps.md)
+ [Other identity providers](other-idps.md)
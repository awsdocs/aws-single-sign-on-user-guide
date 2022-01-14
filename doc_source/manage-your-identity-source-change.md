# Change your identity source<a name="manage-your-identity-source-change"></a>

You can change where you store users at any time\. Use the following procedure to switch from a directory that AWS SSO provides \(the default\) to an external identity provider, AWS Managed Microsoft AD directory or vice versa\. Make sure to review identity source considerations before proceeding\. For more information, see [Considerations for changing your identity source](manage-your-identity-source-considerations.md)\.

**To change your identity source**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**

1. On the **Settings** page, choose the **Identity source** tab, and then choose **Actions > Change identity source**\.

1. Under **Choose identity source**, select the source you want to switch to, and then choose **Next**\. 

   If you are switching to a Microsoft AD directory, you must choose the available directory from the menu on the next page\. 
**Important**  
Changing your source to or from Active Directory removes all existing user and group assignments\. You must manually reapply assignments after you have successfully changed your source\.

   If you are switching to an external identity provider, we recommend that you following the procedure [How to connect to an external identity provider](manage-your-identity-source-idp.md#how-to-connect-idp) for additional instructions\.

1. Once you have read the disclaimer and are ready to proceed, type **ACCEPT**\.

1. Choose **Change identity source**\.
# Change Your Identity Source<a name="manage-your-identity-source-change"></a>

You can change where you store users at any time\. Use the following procedure to switch from a directory that AWS SSO provides \(the default\) to an external identity provider, AWS Managed Microsoft AD directory or vice versa\. Make sure to review identity source considerations before proceeding\. For more information, see [Considerations for Changing Your Identity Source](manage-your-identity-source-considerations.md)\.

**To change your identity source**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**

1. On the **Settings** page, under **Identity source**, choose **Change**\.

1. On the **Change identity source** page, select the source you want to switch to, and then choose **Next**\. If you are switching to a Microsoft AD directory, you must choose the available directory from the provided menu\. 
**Important**  
Changing your source to or from Active Directory removes all existing user and group assignments\. You must manually reapply assignments after you have successfully changed your source\.

1. Choose **Next: Review**\.

1. Once you have read the disclaimer and are ready to proceed, type **CONFIRM**\.

1. Choose **Finish**\.
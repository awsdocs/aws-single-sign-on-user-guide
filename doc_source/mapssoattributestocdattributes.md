# Map attributes in AWS SSO to attributes in your AWS Managed Microsoft AD directory<a name="mapssoattributestocdattributes"></a>

You can use the following procedure to specify how your user attributes in AWS SSO should map to corresponding attributes in your Microsoft AD directory\.

**To map attributes in AWS SSO to attributes in your directory**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, and then choose **Actions > Manage attribute mappings**\.

1. On the **Manage attribute mappings** page, find the attribute in AWS SSO that you want to map and then type a value in the text box\. For example, you might want to map the AWS SSO user attribute **`email`** to the Microsoft AD directory attribute **`${dir:windowsUpn}`**\.

1. Choose **Save changes**\.
# Map attributes in IAM Identity Center to attributes in your AWS Managed Microsoft AD directory<a name="mapssoattributestocdattributes"></a>

You can use the following procedure to specify how your user attributes in IAM Identity Center should map to corresponding attributes in your Microsoft AD directory\.

**To map attributes in IAM Identity Center to attributes in your directory**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, and then choose **Actions > Manage attribute mappings**\.

1. On the **Manage attribute mappings** page, find the attribute in IAM Identity Center that you want to map and then type a value in the text box\. For example, you might want to map the IAM Identity Center user attribute **`email`** to the Microsoft AD directory attribute **`${dir:windowsUpn}`**\.

1. Choose **Save changes**\.
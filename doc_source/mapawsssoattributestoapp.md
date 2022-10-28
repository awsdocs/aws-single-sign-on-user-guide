# Map attributes in your application to IAM Identity Center attributes<a name="mapawsssoattributestoapp"></a>

Some service providers require custom SAML assertions to pass additional data about your user sign\-ins\. In that case, use the following procedure to specify how your applications user attributes should map to corresponding attributes in IAM Identity Center\.

**To map application attributes to attributes in IAM Identity Center**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. In the list of applications, choose the application where you want to map attributes\. 

1. On the application details page, choose the **Attribute mappings** tab\.

1. Choose **Add new attribute mapping**

1. In the first text box, enter the application attribute\.

1. In the second text box, enter the attribute in IAM Identity Center that you want to map to the application attribute\. For example, you might want to map the application attribute **Username** to the IAM Identity Center user attribute **email**\. To see the list of allowed user attributes in IAM Identity Center, see the table in [Attribute mappings](attributemappingsconcept.md)\.

1. In the third column of the table, choose the appropriate format for the attribute from the menu\.

1. Choose **Save changes**\.
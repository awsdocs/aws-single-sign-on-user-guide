# Map Attributes in Your Application to AWS SSO Attributes<a name="mapawsssoattributestoapp"></a>

Some service providers require custom SAML assertions to pass additional data about your user sign\-ins\. In that case, use the following procedure to specify how your applications user attributes should map to corresponding attributes in AWS SSO\.

**To map application attributes to attributes in AWS SSO**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. In the list of applications, choose the application where you want to map attributes\. 

1. On the application details page, choose the **Attribute mappings** tab\.

1. Choose **Add new attribute mapping**

1. In the first text box, enter the application attribute\.

1. In the second text box, enter the attribute in AWS SSO that you want to map to the application attribute\. For example, you might want to map the application attribute **Username** to the AWS SSO user attribute **email**\. To see the list of allowed user attributes in AWS SSO, see the table in [Attribute Mappings](attributemappingsconcept.md)\.

1. In the third column of the table, choose the appropriate format for the attribute from the menu\.

1. Choose **Save changes**\.
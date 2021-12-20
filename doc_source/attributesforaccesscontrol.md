# Attributes for access control<a name="attributesforaccesscontrol"></a>

**Attributes for access control** is the name of the page in the AWS SSO console where you select user attributes that you want to use in policies to control access to resources\. Administrators can assign users to workloads in AWS based on existing attributes in the users' identity source\.

For example, suppose you want to assign access to S3 buckets based on department names\. While on the **Attributes for access control** page, you select the **Department** user attribute for use with attribute\-based access control \(ABAC\)\. In the AWS SSO permission set, you then write a policy that grants users access only when the **Department** attribute matches the department tag that you assigned to your S3 buckets\. AWS SSO passes the user's department attribute to the account being accessed\. The attribute is then used to determine access based on the policy\. For more information about ABAC, see [Attribute\-based access control](abac.md)\. 

## Getting started<a name="abac-getting-started"></a>

How you get started configuring attributes for access control depends on which identity source you are using\. Regardless of the identity source you choose, after you have selected your attributes you need to create or edit permission set policies\. These policies must grant user identities access to AWS resources\. 

### Choosing attributes when using AWS SSO as your identity source<a name="abac-getting-started-sso"></a>

When you configure AWS SSO as the identity source, you first add users and configure their attributes\. Next, navigate to the **Attributes for access control** page and select the attributes you want to use in policies\. Finally, navigate to the **AWS accounts** page to create or edit permission sets to use the attributes for ABAC\.

### Choosing attributes when using AWS Managed Microsoft AD as your identity source<a name="abac-getting-started-ms-ad"></a>

When you configure AWS SSO with AWS Managed Microsoft AD as your identity source, you first map a set of attributes from Active Directory to user attributes in AWS SSO\. Next, navigate to the **Attributes for access control** page\. Then choose which attributes to use in your ABAC configuration based on the existing set of SSO attributes mapped from Active Directory\. Finally, author ABAC rules using the access control attributes in permission sets to grant user identities access to AWS resources\. For a list of the default mappings for user attributes in AWS SSO to the user attributes in your AWS Managed Microsoft AD directory, see [Default mappings](attributemappingsconcept.md#defaultattributemappings)\.

### Choosing attributes when using an external identity provider as your identity source<a name="abac-getting-started-idp"></a>

When you configure AWS SSO with an external identity provider \(IdP\) as your identity source, there are two ways to use attributes for ABAC\.
+ You can configure your IdP to send the attributes through SAML assertions\. In this case, AWS SSO passes the attribute name and value from the IdP through for policy evaluation\.
**Note**  
Attributes in SAML assertions will not be visible to you on the **Attributes for access control** page\. You will have to know these attributes in advance and add them to access control rules when you author policies\. If you decide to trust your external IdPs for attributes, then these attributes will always be passed when users federate into AWS accounts\. In scenarios where the same attributes are coming to SSO through SAML and SCIM, the SAML attributes value take precedence in access control decisions\.
+ You can configure which attributes you use from the **Attributes for access control** page in the AWS SSO console\. The attributes values that you choose here replace the values for any matching attributes that come from an IdP through an assertion\. Depending on whether you are using SCIM, consider the following:
  + If using SCIM, the IdP automatically synchronizes the attribute values into AWS SSO\. Additional attributes that are required for access control might not be present in the list of SCIM attributes\. In that case, consider collaborating with the IT admin in your IdP to send such attributes to SSO via SAML assertions using the required `https://aws.amazon.com/SAML/Attributes/AccessControl:` prefix\. For information about how to configure user attributes for access control in your IdP to send through SAML assertions, see [Supported identity providers](supported-idps.md)\.
  + If you are not using SCIM, you must manually add the users and set their attributes just as if you were using AWS SSO as an identity source\. Next, navigate to the **Attributes for access control** page and choose the attributes you want to use in policies\. 

For a complete list of supported attributes for user attributes in AWS SSO to the user attributes in your external IdPs, see [Supported external identity provider attributes](attributemappingsconcept.md#supportedidpattributes)\.

To get started with ABAC in AWS SSO, see the following topics\.

**Topics**
+ [Getting started](#abac-getting-started)
+ [Enable and configure attributes for access control](configure-abac.md)
+ [Create permission policies for ABAC in AWS SSO](configure-abac-policies.md)
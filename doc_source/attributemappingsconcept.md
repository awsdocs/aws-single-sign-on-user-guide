# Attribute mappings<a name="attributemappingsconcept"></a>

Attribute mappings are used to map attribute types that exist in AWS SSO with like attributes in an AWS Managed Microsoft AD directory\. AWS SSO retrieves user attributes from your Microsoft AD directory and maps them to AWS SSO user attributes\. These AWS SSO user attribute mappings are also used for generating SAML assertions for your cloud applications\. Each cloud application determines the list of SAML attributes it needs for successful single sign\-on\. 

AWS SSO prefills a set of attributes for you under the **Attribute mappings** tab found on your application's configuration page\. AWS SSO uses these user attributes to populate SAML assertions \(as SAML attributes\) that are sent to the cloud application\. These user attributes are in turn retrieved from your Microsoft AD directory\. For more information, see [Map attributes in your application to AWS SSO attributes](mapawsssoattributestoapp.md)\. 

AWS SSO also manages a set of attributes for you under the **Attribute mappings** section of your directory configuration page\. For more information, see [Map attributes in AWS SSO to attributes in your AWS Managed Microsoft AD directory](mapssoattributestocdattributes.md)\.

## Supported directory attributes<a name="supporteddirectoryattributes"></a>

The following table lists all AWS Managed Microsoft AD directory attributes that are supported and that can be mapped to user attributes in AWS SSO\. 


****  

| Supported attributes in your Microsoft AD directory | 
| --- | 
| $\{dir:email\} | 
| $\{dir:displayname\} | 
| $\{dir:distinguishedName\} | 
| $\{dir:firstname\} | 
| $\{dir:guid\} | 
| $\{dir:initials\} | 
| $\{dir:lastname\} | 
| $\{dir:proxyAddresses\} | 
| $\{dir:proxyAddresses:smtp\} | 
| $\{dir:proxyAddresses:SMTP\} | 
| $\{dir:windowsUpn\} | 

You can specify any combination of supported Microsoft AD directory attributes to map to a single mutable attribute in AWS SSO\. For example, you can choose the `subject` attribute under the **User attribute in AWS SSO** column\. Then map it to either `${dir:displayname}` or `${dir:lastname}${dir:firstname }` or any single supported attribute or any arbitrary combination of supported attributes\. For a list of the default mappings for user attributes in AWS SSO, see [Default mappings](#defaultattributemappings)\.

**Note**  
Certain AWS SSO attributes can't be modified because they are immutable and mapped by default to specific Microsoft AD directory attributes\.

If you use the [ListUsers](https://docs.aws.amazon.com/singlesignon/latest/IdentityStoreAPIReference/API_ListUsers.html) or [ListGroups](https://docs.aws.amazon.com/singlesignon/latest/IdentityStoreAPIReference/API_ListGroups.html) API actions or the [list\-users](https://docs.aws.amazon.com/cli/latest/reference/identitystore/list-users.html) and [list\-groups](https://docs.aws.amazon.com/cli/latest/reference/identitystore/list-groups.html) AWS CLI commands to assign users and groups access to AWS accounts and to applications, you must specify the value for `AttributeValue` as an FQDN\. This value must be in the following format: user@example\.com\. In the following example, `AttributeValue` is set to `janedoe@example.com`\.

```
aws identitystore list-users --identity-store-id d-12345a678b --filters AttributePath=UserName,AttributeValue=janedoe@example.com
```

## Supported AWS SSO attributes<a name="supportedssoattributes"></a>

The following table lists all AWS SSO attributes that are supported and that can be mapped to user attributes in your AWS Managed Microsoft AD directory\. After you set up your application attribute mappings, you can use these same AWS SSO attributes to map to actual attributes used by that application\.


****  

| Supported attributes in AWS SSO | 
| --- | 
| $\{user:AD\_GUID\} | 
| $\{user:email\} | 
| $\{user:familyName\} | 
| $\{user:givenName\} | 
| $\{user:middleName\} | 
| $\{user:name\} | 
| $\{user:preferredUsername\} | 
| $\{user:subject\} | 

## Supported external identity provider attributes<a name="supportedidpattributes"></a>

The following table lists all external identity provider \(IdP\) attributes that are supported and that can be mapped to attributes you can use when configuring [Attributes for access control](attributesforaccesscontrol.md) in AWS SSO\. When using SAML assertions, you can use whichever attributes your IdP supports\.


****  

| Supported attributes in your IdP | 
| --- | 
| $\{path:userName\} | 
| $\{path:name\.familyName\} | 
| $\{path:name\.givenName\} | 
| $\{path:displayName\} | 
| $\{path:nickName\} | 
| $\{path:emails\[primary eq true\]\.value\} | 
| $\{path:addresses\[type eq "work"\]\.streetAddress\} | 
| $\{path:addresses\[type eq "work"\]\.locality\} | 
| $\{path:addresses\[type eq "work"\]\.region\} | 
| $\{path:addresses\[type eq "work"\]\.postalCode\} | 
| $\{path:addresses\[type eq "work"\]\.country\} | 
| $\{path:addresses\[type eq "work"\]\.formatted\} | 
| $\{path:phoneNumbers\[type eq "work"\]\.value\} | 
| $\{path:userType\} | 
| $\{path:title\} | 
| $\{path:locale\} | 
| $\{path:timezone\} | 
| $\{path:enterprise\.employeeNumber\} | 
| $\{path:enterprise\.costCenter\} | 
| $\{path:enterprise\.organization\} | 
| $\{path:enterprise\.division\} | 
| $\{path:enterprise\.department\} | 
| $\{path:enterprise\.manager\.value\} | 

## Default mappings<a name="defaultattributemappings"></a>

The following table lists the default mappings for user attributes in AWS SSO to the user attributes in your AWS Managed Microsoft AD directory\. AWS SSO only supports the list of attributes in the **User attribute in AWS SSO** column\. 

**Note**  
If you don't have any assignments for your users and groups in AWS SSO when you enable configurable AD sync, the default mappings in the following table are used\. For information about how to customize these mappings, see [Configure attribute mappings for your sync](provision-users-from-ad-configurable-ADsync.md#manage-sync-configure-attribute-mapping-configurable-ADsync)\.


****  

| User attribute in AWS SSO  | Maps to this attribute in your Microsoft AD directory | 
| --- | --- | 
| AD\_GUID | $\{dir:guid\} | 
| email \* | $\{dir:windowsUpn\} | 
| familyName | $\{dir:lastname\} | 
| givenName | $\{dir:firstname\} | 
| middleName | $\{dir:initials\} | 
| name | $\{dir:displayname\} | 
| preferredUsername | $\{dir:displayname\} | 
| subject | $\{dir:windowsUpn\} | 

\* The email attribute in AWS SSO must be unique within the directory\. Otherwise, the JIT login process could fail\.

You can change the default mappings or add more attributes to the SAML assertion based on your requirements\. For example, assume that your cloud application requires the users email in the `User.Email` SAML attribute\. In addition, assume that email addresses are stored in the `windowsUpn` attribute in your Microsoft AD directory\. To achieve this mapping, you must make changes in the following two places in the AWS SSO console:

1. On the **Directory** page, under the **Attribute mappings** section, you would need to map the user attribute **`email`** to the **`${dir:windowsUpn}`** attribute \(in the **Maps to this attribute in your directory** column\)

1. On the **Applications** page, choose the application from the table\. Choose the **Attribute mappings** tab\. Then map the `User.Email` attribute to the **`${user:email}`** attribute \(in the **Maps to this string value or user attribute in AWS SSO** column\)\.

Note that you must supply each directory attribute in the form $\{dir:**AttributeName**\}\. For example, the `firstname` attribute in your Microsoft AD directory becomes `${dir:firstname}`\. It is important that every directory attribute have an actual value assigned\. Attributes missing a value after `${dir:` will cause user sign\-in issues\.
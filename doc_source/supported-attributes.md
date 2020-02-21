# Supported User and Group Attributes<a name="supported-attributes"></a>

Attributes are pieces of information that help you define and identify individual user or group objects, such as `name`, `email`, or `members`\. AWS SSO supports most commonly used attributes regardless if they are entered manually during user creation or when automatically provisioned using a synchronization engine such as defined in the System for Cross\-Domain Identity Management \(SCIM\) specification\. For more information about this specification, see [https://tools\.ietf\.org/html/rfc7642]( https://tools.ietf.org/html/rfc7642)\. For more information about manual and automatic provisioning, see [Provisioning When Users Come from an External Identity Provider](manage-your-identity-source-idp.md#provisioning-when-external-idp)\.

Because AWS SSO supports SCIM for automatic provisioning use cases, the AWS SSO identity store supports all of the same user and group attributes that are listed in the SCIM specification, with a few exceptions\. The following sections describe which attributes AWS SSO does not support\.

## User Objects<a name="user-object-attributes"></a>

All attributes from the SCIM user schema \([https://tools\.ietf\.org/html/rfc7643\#section\-8\.3](https://tools.ietf.org/html/rfc7643#section-8.3)\) are supported in the AWS SSO identity store EXCEPT the following:
+ `password`
+ `ims`
+ `photos`
+ `entitlements`
+ `x509Certificates`

All sub\-attributes for users are supported EXCEPT the following:
+ `'display'` sub\-attribute of any multi\-valued attribute \(For example, `emails` or `phoneNumbers`\)
+ `'version'` sub\-attribute of `'meta'` attribute

## Group Objects<a name="group-object-attributes"></a>

All attributes from the SCIM group schema \([https://tools\.ietf\.org/html/rfc7643\#section\-8\.4](https://tools.ietf.org/html/rfc7643#section-8.4)\) are supported\.

All sub\-attributes for groups are supported EXCEPT the following:
+ `'display'` sub\-attribute of any multi\-valued attribute \(For example, members\)\.
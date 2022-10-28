# Supported user and group attributes<a name="supported-attributes"></a>

Attributes are pieces of information that help you define and identify individual user or group objects, such as `name`, `email`, or `members`\. IAM Identity Center supports most commonly used attributes regardless if they are entered manually during user creation or when automatically provisioned using a synchronization engine such as defined in the System for Cross\-Domain Identity Management \(SCIM\) specification\. For more information about this specification, see [https://tools\.ietf\.org/html/rfc7642]( https://tools.ietf.org/html/rfc7642)\. For more information about manual and automatic provisioning, see [Provisioning when users come from an external IdP](manage-your-identity-source-idp.md#provisioning-when-external-idp)\.

Because IAM Identity Center supports SCIM for automatic provisioning use cases, the Identity Center directory supports all of the same user and group attributes that are listed in the SCIM specification, with a few exceptions\. The following sections describe which attributes are not supported by IAM Identity Center\.

## User objects<a name="user-object-attributes"></a>

All attributes from the SCIM user schema \([https://tools\.ietf\.org/html/rfc7643\#section\-8\.3](https://tools.ietf.org/html/rfc7643#section-8.3)\) are supported in the IAM Identity Center identity store, except for the following:
+ `password`
+ `ims`
+ `photos`
+ `entitlements`
+ `x509Certificates`

All sub\-attributes for users are supported, except for the following:
+ `'display'` sub\-attribute of any multi\-valued attribute \(For example, `emails` or `phoneNumbers`\)
+ `'version'` sub\-attribute of `'meta'` attribute

## Group objects<a name="group-object-attributes"></a>

All attributes from the SCIM group schema \([https://tools\.ietf\.org/html/rfc7643\#section\-8\.4](https://tools.ietf.org/html/rfc7643#section-8.4)\) are supported\.

All sub\-attributes for groups are supported, except for the following:
+ `'display'` sub\-attribute of any multi\-valued attribute \(For example, members\)\.
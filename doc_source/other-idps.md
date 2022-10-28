# Other identity providers<a name="other-idps"></a>

IAM Identity Center implements the following standards\-based protocols for identity federation:
+ SAML 2\.0 for user authentication
+ SCIM for provisioning

Any identity provider \(IdP\) that implements these standard protocols is expected to interoperate successfully with IAM Identity Center, with the following special considerations:
+ **SAML**
  + IAM Identity Center requires a SAML nameID format of email address \(that is, `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`\)\.
  + The value of the nameID field in assertions must be an RFC 2822 \([https://tools\.ietf\.org/html/rfc2822](https://tools.ietf.org/html/rfc2822)\) addr\-spec compliant \(“`name@domain.com`”\) string \(https://tools\.ietf\.org/html/rfc2822\#section\-3\.4\.1\)\.
  + The metadata file cannot be over 75000 characters\.
  + The metadata must contain an entityId, X509 certificate, and SingleSignOnService as part of the sign\-in URL\.
  + An encryption key is not supported\.
+ **SCIM**
  + The IAM Identity Center SCIM implementation is based on SCIM RFCs 7642 \([https://tools\.ietf\.org/html/rfc7642](https://tools.ietf.org/html/rfc7642)\), 7643 \([https://tools\.ietf\.org/html/rfc7643](https://tools.ietf.org/html/rfc7643)\), and 7644 \([https://tools\.ietf\.org/html/rfc7644](https://tools.ietf.org/html/rfc7644)\), and the interoperability requirements laid out in the March 2020 draft of the FastFed Basic SCIM Profile 1\.0 \([https://openid\.net/specs/fastfed\-scim\-1\_0\-02\.html\#rfc\.section\.4](https://openid.net/specs/fastfed-scim-1_0-02.html#rfc.section.4)\)\. Any differences between these documents and the current implementation in IAM Identity Center are described in the [Supported API operations](https://docs.aws.amazon.com/singlesignon/latest/developerguide/supported-apis.html) section of the *IAM Identity Center SCIM Implementation Developer Guide*\.

IdPs that do not conform to the standards and considerations mentioned above are not supported\. Please contact your IdP for questions or clarifications regarding the conformance of their products to these standards and considerations\.

If you have any issues connecting your IdP to IAM Identity Center, we recommend that you check:
+ AWS CloudTrail logs by filtering on the event name **ExternalIdPDirectoryLogin**
+ IdP\-specific logs and/or debug logs
+ [Troubleshooting IAM Identity Center issues](troubleshooting.md)

**Note**  
Some IdPs, including the list of [Supported identity providers](supported-idps.md), offer a simplified configuration experience for IAM Identity Center in the form of an “application” or “connector” built specifically for IAM Identity Center\. If your IdP provides this option, we recommend that you use it, being careful to choose the item that’s built specifically for IAM Identity Center\. Other items called “AWS”, “AWS federation”, or similar generic "AWS" names may use other federation approaches and/or endpoints, and may not work as expected with IAM Identity Center\.
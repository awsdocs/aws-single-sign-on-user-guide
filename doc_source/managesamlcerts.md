# Manage SAML 2\.0 certificates<a name="managesamlcerts"></a>

IAM Identity Center uses certificates to set up a SAML trust relationship between IAM Identity Center and your external identity provider \(IdP\)\. When you add an external IdP in IAM Identity Center, you must also obtain at least one public SAML 2\.0 X\.509 certificate from the external IdP\. That certificate is usually installed automatically during the IdP SAML metadata exchange during trust creation\.

As an IAM Identity Center administrator, you'll occasionally need to replace older IdP certificates with newer ones\. For example, you might need to replace an IdP certificate when the expiration date on the certificate approaches\. The process of replacing an older certificate with a newer one is referred to as certificate rotation\.

**Topics**
+ [Rotate a SAML 2\.0 certificate](rotatesamlcert.md)
+ [Certificate expiration status indicators](samlcertexpirationindicators.md)
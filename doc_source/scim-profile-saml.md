# SCIM Profile and SAML 2\.0 Implementation<a name="scim-profile-saml"></a>

Both SCIM and SAML are important considerations for configuring AWS SSO\. 

## SAML 2\.0 Implementation<a name="samlfederationconcept"></a>

AWS SSO supports identity federation with [SAML \(Security Assertion Markup Language\)](https://wiki.oasis-open.org/security) 2\.0\. This allows AWS SSO to authenticate identities from external identity providers \(IdPs\)\. SAML 2\.0 is an industry standard used for securely exchanging SAML assertions\. SAML 2\.0 passes information about a user between a SAML authority \(called an identity provider or IdP\), and a SAML consumer \(called a service provider or SP\)\. The AWS SSO service uses this information to provide federated single sign\-on \(SSO\), allowing users to access AWS accounts and configured applications based on their existing identity provider credentials \(such as a username and password\)\. 

AWS SSO adds SAML IdP capabilities to your AWS SSO store, AWS Managed Microsoft AD, or to an external identity provider\. Users can then SSO into services that support SAML, including the AWS Management Console and third\-party applications such as Microsoft 365, Concur, and Salesforce\. 

The SAML protocol however does not provide a way to query the IdP to learn about users and groups\. Therefore, you must make AWS SSO aware of those users and groups by provisioning them into AWS SSO\. 

## SCIM Profile<a name="scim-profile"></a>

AWS SSO provides support for the System for Cross\-domain Identity Management \(SCIM\) v2\.0 standard\. SCIM keeps your AWS SSO identities in sync with identities from your IdP\. This includes any provisioning, updates, and deprovisioning of users between your IdP and AWS SSO\.

For more information about how to implement SCIM, see [Automatic Provisioning](provision-automatically.md)\. For additional details about AWS SSO’s SCIM implementation, see the [AWS SSO SCIM Implementation Developer Guide](https://docs.aws.amazon.com/singlesignon/latest/developerguide/what-is-scim.html)\.

**Topics**
+ [SAML 2\.0 Implementation](#samlfederationconcept)
+ [SCIM Profile](#scim-profile)
+ [Automatic Provisioning](provision-automatically.md)
+ [Manual Provisioning](provision-manually.md)
+ [Manage SAML 2\.0 Certificates](managesamlcerts.md)
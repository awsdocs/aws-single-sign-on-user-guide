# SAML Federation<a name="samlfederationconcept"></a>

AWS SSO supports identity federation with [SAML \(Security Assertion Markup Language\)](https://wiki.oasis-open.org/security) 2\.0\. SAML 2\.0 is an industry standard used for securely exchanging SAML assertions that pass information about a user between a SAML authority \(called an identity provider or IdP\), and a SAML consumer \(called a service provider or SP\)\. AWS SSO service uses this information to provide federated single sign\-on \(SSO\) for those users who are authorized to use applications within the AWS SSO user portal\. 

AWS SSO adds SAML IdP capabilities to either your AWS Managed Microsoft AD or AWS SSO directory\. Users can then SSO into services that support SAML, including the AWS Management Console and third\-party applications such as Office 365, SAP Concur, and Salesforce\. At this time, AWS SSO does not support other directory types or IdPs\.

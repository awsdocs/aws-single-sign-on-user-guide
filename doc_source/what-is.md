# What Is AWS Single Sign\-On?<a name="what-is"></a>

AWS Single Sign\-On is a cloud\-based single sign\-on \(SSO\) service that makes it easy to centrally manage SSO access to all of your AWS accounts and cloud applications\. Specifically, it helps you manage SSO access and user permissions across all your AWS accounts in AWS Organizations\. AWS SSO also helps you manage access and permissions to commonly used third\-party software as a service \(SaaS\) applications as well as custom applications that support Security Assertion Markup Language \(SAML\) 2\.0\. AWS SSO includes a user portal where your end\-users can find and access all their assigned AWS accounts, cloud applications, and custom applications in one place\. 

## AWS SSO Features<a name="features"></a>

AWS SSO provides the following features:

**Integration with AWS Organizations**

AWS SSO is integrated deeply with AWS Organizations and AWS API operations, unlike other cloud native SSO solutions\. AWS SSO natively integrates with AWS Organizations, enumerates all your AWS accounts, and if you have organized your accounts under organizational units \(OUs\) you will see them displayed that way within the AWS SSO console\. This enables you to quickly discover your AWS accounts, deploy common sets of permissions, and manage access from a central location\.

**SSO access to your AWS accounts and cloud applications**

AWS SSO makes it simple for you to manage SSO across all your AWS accounts, cloud applications, and custom SAML 2\.0–based applications\. without custom scripts or third\-party SSO solutions\. Use the AWS SSO console to quickly assign which users should have one\-click access to only the applications that you've authorized for their personalized end\-user portal\.

**Use your existing corporate identities**

AWS SSO is integrated with Microsoft AD through the AWS Directory Service\. That means your employees can sign in to your AWS SSO user portal using their corporate Active Directory credentials\. To grant Active Directory users access to accounts and applications, you simply add them to the appropriate Active Directory groups\. For example, you can grant the DevOps group SSO access to your production AWS accounts\. Users added to the DevOps group are then granted SSO access to these AWS accounts automatically\. This automation makes it easy to on\-board new users and give existing users access to new accounts and applications quickly\.

**Compatible with commonly used cloud applications**

AWS SSO supports commonly used cloud applications such as Salesforce, Box, and Office 365\. This cuts the time needed to set up these applications for SSO by providing application integration instructions\. These instructions act as guard rails to help administrators set up and troubleshoot these SSO configurations\. This eliminates the need for administrators to learn the configuration nuances of each cloud application\.

**Easy to set up and monitor usage**

With AWS SSO, you can enable a highly available SSO service with just a few clicks\. There is no additional infrastructure to deploy or AWS account to set up\. AWS SSO is a highly available and a completely secure infrastructure that scales to your needs and does not require software or hardware to manage\. AWS SSO records all sign\-in activity in AWS CloudTrail, giving you the visibility to monitor and audit SSO activity in one place\. 
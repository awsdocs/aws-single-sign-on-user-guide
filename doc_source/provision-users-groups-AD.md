# Provision users and groups from Active Directory<a name="provision-users-groups-AD"></a>

AWS SSO provides the following two ways to provision users and groups from Active Directory\.
+ [AWS SSO configurable Active Directory \(AD\) sync \(recommended\)](provision-users-from-ad-configurable-ADsync.md) — With this sync method, you can do the following:
  + Control data boundaries by explicitly defining the users and groups in Microsoft Active Directory that are automatically synchronized into AWS SSO\. You can add or remove users and groups to change the scope of the sync at any time\.
  + Assign synchronized users and groups access to AWS accounts and applications \[AWS SSO\-integrated applications, cloud applications, or custom Security Assertion Markup Language \(SAML 2\.0\) applications\]\. 
  + Control the synchronization process by pausing and resuming the sync as needed\. This helps you regulate the load on production systems\.
+ [AWS SSO AD sync](provision-users-from-ad-ADsync.md) — With this sync method, you use AWS SSO to assign users and groups in Active Directory access to AWS accounts and to applications\. All identities with assignments are automatically synced into AWS SSO\.
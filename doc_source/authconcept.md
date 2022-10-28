# User authentications<a name="authconcept"></a>

A user signs in to the AWS access portal using their user name\. When they do, IAM Identity Center redirects the request to the IAM Identity Center authentication service based on the directory associated with the user email address\. Once authenticated, users have single sign\-on access to any of the AWS accounts and third\-party software\-as\-a\-service \(SaaS\) applications that show up in the portal without additional sign\-in prompts\. This means that users no longer need to keep track of multiple account credentials for the various assigned AWS applications that they use on a daily basis\.

## Authentication sessions<a name="sessionsconcept"></a>

There are two types of authentication sessions maintained by IAM Identity Center: one to represent the users’ sign in to IAM Identity Center, and another to represent the users’ access to IAM Identity Center enabled applications, such as Amazon SageMaker Studio or Amazon Managed Grafana\. Each time a user signs in to IAM Identity Center, a sign in session is created for the duration configured in Identity Center, which can be up to 7 days\. For more information, see [Manage IAM Identity Center integrated application sessions](manage-app-session.md)\. Each time the user accesses an Identity Center enabled application, the IAM Identity Center sign in session is used to obtain an IAM Identity Center application session for that application\. IAM Identity Center application sessions have a refreshable 1\-hour lifetime – that is, IAM Identity Center application sessions are automatically refreshed every hour as long as the IAM Identity Center sign in session from which they were obtained is still valid\. When the user uses IAM Identity Center to access the AWS Management Console or CLI, the IAM Identity Center sign in session is used to obtain an IAM session, as specified in the corresponding IAM Identity Center permission set \(more specifically, IAM Identity Center assumes an IAM role, which IAM Identity Center manages, in the target account\)\.

When you disable or delete a user in IAM Identity Center, that user will immediately be prevented from signing in to create new IAM Identity Center sign in sessions\. IAM Identity Center sign in sessions are cached for one hour, which means that when you disable or delete a user while they have an active IAM Identity Center sign in session, their existing IAM Identity Center sign in session will continue for up to an hour, depending on when the sign in session was last refreshed\. During this time, the user can initiate new IAM Identity Center application and IAM role sessions\. 

After the IAM Identity Center sign in session expires, the user can no longer initiate new IAM Identity Center application or IAM role sessions\. However, IAM Identity Center application sessions can also be cached for up to an hour, such that the user may retain access to an Identity Center enabled application for up to an hour after the IAM Identity Center sign in session has expired\. Any existing IAM role sessions will continue based on the duration configured in the IAM Identity Center permission set \(admin\-configurable, up to 12 hours\)\.

The table below summarizes these behaviors:


****  

| User experience / system behavior | Time after user is disabled / deleted | 
| --- | --- | 
| User can no longer sign in to IAM Identity Center; user cannot obtain a new IAM Identity Center sign in session | None \(effective immediately\) | 
| User can no longer start new application or IAM role sessions via IAM Identity Center | Up to 1 hour | 
| User can no longer access any Identity Center enabled applications \(all app sessions are terminated\) | Up to 2 hours \(up to 1 hour for IAM Identity Center sign in session expiry, plus up to 1 hour for IAM Identity Center app session expiry\) | 
| User can no longer access any AWS accounts through IAM Identity Center | Up to 13 hours \(up to 1 hour for IAM Identity Center sign in session expiry, plus up to 12 hours for administrator\-configured IAM role session expiry per the IAM Identity Center session duration settings for the permission set\) | 

For more information about sessions, see [Set session duration](howtosessionduration.md)\.
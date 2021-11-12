# User authentications<a name="authconcept"></a>

A user signs in to the user portal using their user name\. When they do, AWS SSO redirects the request to the AWS SSO authentication service based on the directory associated with the user email address\. Once authenticated, users have SSO access to any of the AWS accounts and third\-party software\-as\-a\-service \(SaaS\) applications that show up in the portal without additional sign\-in prompts\. This means that users no longer need to keep track of multiple account credentials for the various assigned AWS applications that they use on a daily basis\.

## Authentication sessions<a name="sessionsconcept"></a>

There are two types of authentication sessions maintained by AWS SSO: one to represent the users’ sign in to AWS SSO, and another to represent the users’ access to AWS SSO\-integrated applications, such as Amazon SageMaker Studio or Amazon Managed Grafana\. Each time a user signs in to AWS SSO, a sign in session is created with an 8\-hour lifetime\. Each time the user accesses an AWS SSO\-enabled application, the AWS SSO sign in session is used to obtain an AWS SSO application session for that application\. AWS SSO application sessions have a refreshable 1\-hour lifetime – that is, AWS SSO application sessions are automatically refreshed every hour as long as the AWS SSO sign in session from which they were obtained is still valid\. When the user uses AWS SSO to access the AWS Management Console or CLI, the AWS SSO sign in session is used to obtain an IAM session, as specified in the corresponding AWS SSO permission set \(more specifically, AWS SSO assumes an IAM role, which AWS SSO manages, in the target account\)\.

When you disable or delete a user in AWS SSO, that user will immediately be prevented from signing in to create new AWS SSO sign in sessions\. AWS SSO sign in sessions are cached for one hour, which means that when you disable or delete a user while they have an active AWS SSO sign in session, their existing SSO sign in session will continue for up to an hour, depending on when the sign in session was last refreshed\. During this time, the user can initiate new AWS SSO application and IAM role sessions\. 

After the AWS SSO sign in session expires, the user can no longer initiate new AWS SSO application or IAM role sessions\. However, AWS SSO application sessions can also be cached for up to an hour, such that the user may retain access to an AWS SSO\-integrated application for up to an hour after the AWS SSO sign in session has expired\. Any existing IAM role sessions will continue based on the duration configured in the AWS SSO permission set \(admin\-configurable, up to 12 hours\)\.

The table below summarizes these behaviors:


****  

| User experience / system behavior | Time after SSO user is disabled / deleted | 
| --- | --- | 
| User can no longer sign in to AWS SSO; user cannot obtain a new AWS SSO sign in session | None \(effective immediately\) | 
| User can no longer start new application or IAM role sessions via AWS SSO | Up to 1 hour | 
| User can no longer access any AWS SSO\-integrated applications \(all app sessions are terminated\) | Up to 2 hours \(up to 1 hour for AWS SSO sign in session expiry, plus up to 1 hour for AWS SSO app session expiry\) | 
| User can no longer access any AWS accounts through AWS SSO | Up to 13 hours \(up to 1 hour for AWS SSO sign in session expiry, plus up to 12 hours for administrator\-configured IAM role session expiry per the AWS SSO session duration settings for the permission set\) | 

For more information about sessions, see [Set session duration](howtosessionduration.md)\.
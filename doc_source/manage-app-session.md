# Manage IAM Identity Center integrated application sessions<a name="manage-app-session"></a>

Administrators can customize session duration for the AWS access portal to define how often users are required to re\-authenticate\. Administrators can also terminate AWS access portal sessions\. The AWS access portal session duration changes the duration of IAM Identity Center integrated application sessions, and AWS access portal session termination also affects these applications\. IAM Identity Center integrated applications poll the AWS access portal sessions and terminate when they detect that the AWS access portal session has ended\.

For more information about how to configure the length of AWS access portal sessions, see [Configure AWS access portal session duration](configure-user-session.md)\. For more information about how to manage and delete user sessions, see [Manage AWS access portal sessions](manage-user-session.md)\. Modifying the AWS access portal session duration and terminating AWS access portal sessions has no effect on the AWS Management Console session duration that you define in your permission sets\.

**Note**  
Session management is currently not supported for an Active Directory identity source\.
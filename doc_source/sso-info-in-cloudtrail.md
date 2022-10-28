# IAM Identity Center information in CloudTrail<a name="sso-info-in-cloudtrail"></a>

CloudTrail is enabled on your AWS account when you create the account\. When activity occurs in IAM Identity Center, that activity is recorded in a CloudTrail event along with other AWS service events in **Event history**\. You can view, search, and download recent events in your AWS account\. For more information, see [Viewing events with CloudTrail event history](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html)\. 

For an ongoing record of events in your AWS account, including events for IAM Identity Center, create a trail\. A *trail* enables CloudTrail to deliver log files to an Amazon S3 bucket\. By default, when you create a trail in the console, the trail applies to all AWS Regions\. The trail logs events from all Regions in the AWS partition and delivers the log files to the Amazon S3 bucket that you specify\. Additionally, you can configure other AWS services to further analyze and act upon the event data collected in CloudTrail logs\. For more information, see the following: 
+ [Overview for creating a trail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail.html)
+ [CloudTrail supported services and integrations](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-aws-service-specific-topics.html#cloudtrail-aws-service-specific-topics-integrations)
+ [Configuring Amazon SNS notifications for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)
+ [Receiving CloudTrail log files from multiple Regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail log files from multiple accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)

When CloudTrail logging is enabled in your AWS account, API calls made to IAM Identity Center actions are tracked in log files\. IAM Identity Center records are written together with other AWS service records in a log file\. CloudTrail determines when to create and write to a new file based on a time period and file size\.

The following IAM Identity Center CloudTrail operations are supported:


****  

| Console API operations | Public API operations | 
| --- | --- | 
| AssociateDirectory | AttachManagedPolicyToPermissionSet | 
| AssociateProfile | CreateAccountAssignment | 
| BatchDeleteSession | CreateInstanceAccessControlAttributeConfiguration | 
| BatchGetSession | CreatePermissionSet | 
| CreateApplicationInstance | DeleteAccountAssignment | 
| CreateApplicationInstanceCertificate | DeleteInlinePolicyFromPermissionSet | 
| CreatePermissionSet | DeleteInstanceAccessControlAttributeConfiguration | 
| CreateProfile | DeletePermissionSet | 
| DeleteApplicationInstance | DescribeAccountAssignmentCreationStatus | 
| DeleteApplicationInstanceCertificate | DescribeAccountAssignmentDeletionStatus | 
| DeletePermissionsPolicy | DescribeInstanceAccessControlAttributeConfiguration | 
| DeletePermissionSet | DescribePermissionSet | 
| DeleteProfile | DescribePermissionSetProvisioningStatus | 
| DescribePermissionsPolicies | DetachManagedPolicyFromPermissionSet | 
| DisassociateDirectory | GetInlinePolicyForPermissionSet | 
| DisassociateProfile | ListAccountAssignmentCreationStatus | 
| GetApplicationInstance | ListAccountAssignmentDeletionStatus | 
| GetApplicationTemplate | ListAccountAssignments | 
| GetMfaDeviceManagementForDirectory | ListAccountsForProvisionedPermissionSet | 
| GetPermissionSet | ListInstances | 
| GetSSOStatus | ListManagedPoliciesInPermissionSet | 
| ImportApplicationInstanceServiceProviderMetadata | ListPermissionSetProvisioningStatus | 
| ListApplicationInstances | ListPermissionSets | 
| ListApplicationInstanceCertificates | ListPermissionSetsProvisionedToAccount | 
| ListApplicationTemplates | ListTagsForResource | 
| ListDirectoryAssociations | ProvisionPermissionSet | 
| ListPermissionSets | PutInlinePolicyToPermissionSet | 
| ListProfileAssociations | TagResource | 
| ListProfiles | UntagResource | 
| ListSessions | UpdateInstanceAccessControlAttributeConfiguration | 
| PutMfaDeviceManagementForDirectory | UpdatePermissionSet | 
| PutPermissionsPolicy |  | 
| StartSSO |  | 
| UpdateApplicationInstanceActiveCertificate |  | 
| UpdateApplicationInstanceDisplayData |  | 
| UpdateApplicationInstanceServiceProviderConfiguration |  | 
| UpdateApplicationInstanceStatus |  | 
| UpdateApplicationInstanceResponseConfiguration |  | 
| UpdateApplicationInstanceResponseSchemaConfiguration |  | 
| UpdateApplicationInstanceSecurityConfiguration |  | 
| UpdateDirectoryAssociation |  | 
| UpdateProfile |  | 

For more information about IAM Identity Center’s public API operations, see the [IAM Identity Center API Reference Guide](https://docs.aws.amazon.com/singlesignon/latest/APIReference/welcome.html)\.

The following IAM Identity Center identity store CloudTrail operations are supported:
+ `AddMemberToGroup`
+ `CompleteVirtualMfaDeviceRegistration`
+ `CompleteWebAuthnDeviceRegistration`
+ `CreateAlias`
+ `CreateExternalIdPConfigurationForDirectory` 
+ `CreateGroup`
+ `CreateUser`
+ `DeleteExternalIdPConfigurationForDirectory`
+ `DeleteGroup`
+ `DeleteMfaDeviceForUser`
+ `DeleteUser`
+ `DescribeDirectory`
+ `DescribeGroups`
+ `DescribeUsers`
+ `DisableExternalIdPConfigurationForDirectory`
+ `DisableUser`
+ `EnableExternalIdPConfigurationForDirectory`
+ `EnableUser`
+ `GetAWSSPConfigurationForDirectory`
+ `ListExternalIdPConfigurationsForDirectory`
+ `ListGroupsForUser`
+ `ListMembersInGroup`
+ `ListMfaDevicesForUser`
+ `PutMfaDeviceManagementForDirectory`
+ `RemoveMemberFromGroup`
+ `SearchGroups`
+ `SearchUsers`
+ `StartVirtualMfaDeviceRegistration`
+ `StartWebAuthnDeviceRegistration`
+ `UpdateExternalIdPConfigurationForDirectory` 
+ `UpdateGroup`
+ `UpdateMfaDeviceForUser`
+ `UpdatePassword`
+ `UpdateUser`
+ `VerifyEmail`

The following IAM Identity Center OIDC CloudTrail actions are supported:
+ `CreateToken`
+ `RegisterClient`
+ `StartDeviceAuthorization`

The following IAM Identity Center Portal CloudTrail actions are supported:
+ `Authenticate`
+ `Federate`

Every log entry contains information about who generated the request\. The identity information in the log helps you determine whether the request was made by an AWS account root user or with IAM user credentials\. You can also learn whether the request was made with temporary security credentials for a role or federated user or by another AWS service\. For more information, see the [CloudTrail userIdentity Element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

You can create a trail and store your log files in your Amazon S3 bucket for as long as you want\. You can also define Amazon S3 lifecycle rules to archive or delete log files automatically\. By default, your log files are encrypted with Amazon S3 server\-side encryption \(SSE\)\.

To be notified of log file delivery, configure CloudTrail to publish Amazon SNS notifications when new log files are delivered\. For more information, see [Configuring Amazon SNS notifications for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)\.

You can also aggregate IAM Identity Center log files from multiple AWS Regions and multiple AWS accounts into a single Amazon S3 bucket\. For more information, see [Receiving CloudTrail log files from multiple Regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail log files from multiple accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)\.
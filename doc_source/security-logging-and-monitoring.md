# Logging and Monitoring in AWS Single Sign\-On<a name="security-logging-and-monitoring"></a>

As a best practice, you should monitor your organization to ensure that changes are logged\. This helps you to ensure that any unexpected change can be investigated and unwanted changes can be rolled back\. AWS Single Sign\-On currently supports two AWS services that help you monitor your organization and the activity that happens within it\.

**Topics**
+ [Logging AWS SSO API Calls with AWS CloudTrail](#logging-using-cloudtrail)
+ [Amazon CloudWatch Events](#cloudwatch-integration)

## Logging AWS SSO API Calls with AWS CloudTrail<a name="logging-using-cloudtrail"></a>

AWS SSO is integrated with AWS CloudTrail, a service that provides a record of actions taken by a user, role, or an AWS service in AWS SSO\. If you create a trail, you can enable continuous delivery of CloudTrail events to an Amazon S3 bucket, Amazon CloudWatch Logs, and Amazon CloudWatch Events\. Using the information collected by CloudTrail, you can determine the request that was made to AWS SSO, the IP address from which the request was made, who made the request, when it was made, and additional details\. 

To learn more about CloudTrail, see the [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

### AWS SSO Information in CloudTrail<a name="sso-info-in-cloudtrail"></a>

CloudTrail is enabled on your AWS account when you create the account\. When activity occurs in AWS SSO, that activity is recorded in a CloudTrail event along with other AWS service events in **Event history**\. You can view, search, and download recent events in your AWS account\. For more information, see [Viewing Events with CloudTrail Event History](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html)\. 

For an ongoing record of events in your AWS account, including events for AWS SSO, create a trail\. A *trail* enables CloudTrail to deliver log files to an Amazon S3 bucket\. By default, when you create a trail in the console, the trail applies to all AWS Regions\. The trail logs events from all Regions in the AWS partition and delivers the log files to the Amazon S3 bucket that you specify\. Additionally, you can configure other AWS services to further analyze and act upon the event data collected in CloudTrail logs\. For more information, see the following: 
+ [Overview for Creating a Trail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail.html)
+ [CloudTrail Supported Services and Integrations](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-aws-service-specific-topics.html#cloudtrail-aws-service-specific-topics-integrations)
+ [Configuring Amazon SNS Notifications for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)
+ [Receiving CloudTrail Log Files from Multiple Regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail Log Files from Multiple Accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)

When CloudTrail logging is enabled in your AWS account, API calls made to AWS SSO actions are tracked in log files\. AWS SSO records are written together with other AWS service records in a log file\. CloudTrail determines when to create and write to a new file based on a time period and file size\.

The following AWS SSO CloudTrail actions are supported:


****  

| Console APIs | Public APIs | 
| --- | --- | 
| AssociateDirectory | AttachManagedPolicyToPermissionSet | 
| AssociateProfile | CreateAccountAssignment | 
| CreateApplicationInstance | CreatePermissionSet | 
| CreateApplicationInstanceCertificate | DeleteAccountAssignment | 
| CreatePermissionSet | DeleteInlinePolicyFromPermissionSet | 
| CreateProfile | DeletePermissionSet | 
| DeleteApplicationInstance | DescribeAccountAssignmentCreationStatus | 
| DeleteApplicationInstanceCertificate | DescribeAccountAssignmentDeletionStatus  | 
| DeletePermissionsPolicy | DescribePermissionSet | 
| DeletePermissionSet | DescribePermissionSetProvisioningStatus | 
| DeleteProfile | DetachManagedPolicyFromPermissionSet | 
| DescribePermissionsPolicies | GetInlinePolicyForPermissionSet | 
| DisassociateDirectory | ListAccountAssignmentCreationStatus | 
| DisassociateProfile | ListAccountAssignmentDeletionStatus | 
| GetApplicationInstance | ListAccountAssignments | 
| GetApplicationTemplate | ListAccountsForProvisionedPermissionSet | 
| GetMfaDeviceManagementForDirectory | ListInstances | 
| GetPermissionSet | ListManagedPoliciesInPermissionSet | 
| GetSSOStatus | ListPermissionSetProvisioningStatus | 
| ImportApplicationInstanceServiceProviderMetadata | ListPermissionSets | 
| ListApplicationInstances | ListPermissionSetsProvisionedToAccount | 
| ListApplicationInstanceCertificates | ListTagsForResource | 
| ListApplicationTemplates | ProvisionPermissionSet | 
| ListDirectoryAssociations | PutInlinePolicyToPermissionSet | 
| ListPermissionSets | TagResource | 
| ListProfileAssociations | UntagResource | 
| ListProfiles | UpdatePermissionSet | 
| PutMfaDeviceManagementForDirectory |  | 
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

For more information about AWS SSO’s public APIs, see the [AWS Single Sign\-On API Reference Guide](https://docs.aws.amazon.com/singlesignon/latest/APIReference/welcome.html)\.

The following AWS SSO identity store CloudTrail actions are supported:
+ `AddMemberToGroup`
+ `CompleteVirtualMfaDeviceRegistration`
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
+ `RemoveMemberFromGroup`
+ `SearchGroups`
+ `SearchUsers`
+ `StartVirtualMfaDeviceRegistration`
+ `UpdateExternalIdPConfigurationForDirectory` 
+ `UpdateGroup`
+ `UpdatePassword`
+ `UpdateUser`
+ `VerifyEmail`

The following AWS SSO OIDC CloudTrail actions are supported:
+ `RegisterClient`
+ `StartDeviceAuthorization`
+ `CreateToken`

Every log entry contains information about who generated the request\. The identity information in the log helps you determine whether the request was made by an AWS account root user or with IAM user credentials\. You can also learn whether the request was made with temporary security credentials for a role or federated user or by another AWS service\. For more information, see the [CloudTrail userIdentity Element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

You can create a trail and store your log files in your Amazon S3 bucket for as long as you want\. You can also define Amazon S3 lifecycle rules to archive or delete log files automatically\. By default, your log files are encrypted with Amazon S3 server\-side encryption \(SSE\)\.

To be notified of log file delivery, configure CloudTrail to publish Amazon SNS notifications when new log files are delivered\. For more information, see [Configuring Amazon SNS Notifications for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)\.

You can also aggregate AWS SSO log files from multiple AWS Regions and multiple AWS accounts into a single Amazon S3 bucket\. For more information, see [Receiving CloudTrail Log Files from Multiple Regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail Log Files from Multiple Accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)\.

### Understanding AWS SSO Log File Entries<a name="understanding-sso-entries"></a>

A trail is a configuration that enables delivery of events as log files to an Amazon S3 bucket that you specify\. CloudTrail log files contain one or more log entries\. An event represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. CloudTrail log files are not an ordered stack trace of the public API calls, so they do not appear in any specific order\. 

The following example shows a CloudTrail log entry for an administrator \(samadams@example\.com\) that took place in the AWS SSO console:

```
{
   "Records":[
      {
         "eventVersion":"1.05",
         "userIdentity":{
            "type":"IAMUser",
            "principalId":"AIDAJAIENLMexample",
            "arn":"arn:aws:iam::08966example:user/samadams",
            "accountId":"08966example",
            "accessKeyId":"AKIAIIJM2K4example",
            "userName":"samadams"
         },
         "eventTime":"2017-11-29T22:39:43Z",
         "eventSource":"sso.amazonaws.com",
         "eventName":"DescribePermissionsPolicies",
         "awsRegion":"us-east-1",
         "sourceIPAddress":"203.0.113.0",
         "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36",
         "requestParameters":{
            "permissionSetId":"ps-79a0dde74b95ed05"
         },
         "responseElements":null,
         "requestID":"319ac6a1-d556-11e7-a34f-69a333106015",
         "eventID":"a93a952b-13dd-4ae5-a156-d3ad6220b071",
         "readOnly":true,
         "resources":[

         ],
         "eventType":"AwsApiCall",
         "recipientAccountId":"08966example"
      }
   ]
}
```

The following example shows a CloudTrail log entry for an end\-user \(bobsmith@example\.com\) action that took place in the AWS SSO user portal:

```
{
   "Records":[
      {
         "eventVersion":"1.05",
         "userIdentity":{
            "type":"Unknown",
            "principalId":"example.com//S-1-5-21-1122334455-3652759393-4233131409-1126",
            "accountId":"08966example",
            "userName":"bobsmith@example.com"
         },
         "eventTime":"2017-11-29T18:48:28Z",
         "eventSource":"sso.amazonaws.com",
         "eventName":"https://portal.sso.us-east-1.amazonaws.com/instance/appinstances",
         "awsRegion":"us-east-1",
         "sourceIPAddress":"203.0.113.0",
         "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36",
         "requestParameters":null,
         "responseElements":null,
         "requestID":"de6c0435-ce4b-49c7-9bcc-bc5ed631ce04",
         "eventID":"e6e1f3df-9528-4c6d-a877-6b2b895d1f91",
         "eventType":"AwsApiCall",
         "recipientAccountId":"08966example"
      }
   ]
}
```

The following example shows a CloudTrail log entry for an end\-user \(bobsmith@example\.com\) action that took place in AWS SSO OIDC:

```
{
      "eventVersion": "1.05",
      "userIdentity": {
        "type": "Unknown",
        "principalId": "example.com//S-1-5-21-1122334455-3652759393-4233131409-1126",
        "accountId": "08966example",
        "userName": "bobsmith@example.com"
      },
      "eventTime": "2020-06-16T01:31:15Z",
      "eventSource": "sso.amazonaws.com",
      "eventName": "CreateToken",
      "awsRegion": "us-east-1",
      "sourceIPAddress": "203.0.113.0",
      "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36",
      "requestParameters": {
        "clientId": "clientid1234example",
        "clientSecret": "HIDDEN_DUE_TO_SECURITY_REASONS",
        "grantType": "urn:ietf:params:oauth:grant-type:device_code",
        "deviceCode": "devicecode1234example"
      },
      "responseElements": {
        "accessToken": "HIDDEN_DUE_TO_SECURITY_REASONS",
        "tokenType": "Bearer",
        "expiresIn": 28800,
        "refreshToken": "HIDDEN_DUE_TO_SECURITY_REASONS",
        "idToken": "HIDDEN_DUE_TO_SECURITY_REASONS"
      },
      "eventID": "09a6e1a9-50e5-45c0-9f08-e6ef5089b262",
      "readOnly": false,
      "resources": [
        {
          "accountId": "08966example",
          "type": "IdentityStoreId",
          "ARN": "d-1234example"
        }
      ],
      "eventType": "AwsApiCall",
      "recipientAccountId": "08966example"
}
```

## Amazon CloudWatch Events<a name="cloudwatch-integration"></a>

AWS SSO can work with CloudWatch Events to raise events when administrator\-specified actions occur in an organization\. For example, because of the sensitivity of such actions, most administrators would want to be warned every time someone creates a new account in the organization or when an administrator of a member account attempts to leave the organization\. You can configure CloudWatch Events rules that look for these actions and then send the generated events to administrator\-defined targets\. Targets can be an Amazon SNS topic that emails or text messages its subscribers\. You could also create an AWS Lambda function that logs the details of the action for your later review\.

To learn more about CloudWatch Events, including how to configure and enable it, see the *[Amazon CloudWatch Events User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/)*\.
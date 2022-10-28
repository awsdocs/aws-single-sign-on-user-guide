# Logging IAM Identity Center API calls with AWS CloudTrail<a name="logging-using-cloudtrail"></a>

IAM Identity Center is integrated with AWS CloudTrail, a service that provides a record of actions taken by a user, role, or an AWS service in IAM Identity Center\. If you create a trail, you can enable continuous delivery of CloudTrail events to an Amazon S3 bucket, Amazon CloudWatch Logs, and Amazon CloudWatch Events\. Using the information collected by CloudTrail, you can determine the request that was made to IAM Identity Center, the IP address from which the request was made, who made the request, when it was made, and additional details\. 

To learn more about CloudTrail, see the [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

**Topics**
+ [IAM Identity Center information in CloudTrail](sso-info-in-cloudtrail.md)
+ [Understanding IAM Identity Center log file entries](understanding-sso-entries.md)
+ [Understanding IAM Identity Center sign\-in events](understanding-sign-in-events.md)
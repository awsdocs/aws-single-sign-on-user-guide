# Logging AWS SSO API calls with AWS CloudTrail<a name="logging-using-cloudtrail"></a>

AWS SSO is integrated with AWS CloudTrail, a service that provides a record of actions taken by a user, role, or an AWS service in AWS SSO\. If you create a trail, you can enable continuous delivery of CloudTrail events to an Amazon S3 bucket, Amazon CloudWatch Logs, and Amazon CloudWatch Events\. Using the information collected by CloudTrail, you can determine the request that was made to AWS SSO, the IP address from which the request was made, who made the request, when it was made, and additional details\. 

To learn more about CloudTrail, see the [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

**Topics**
+ [AWS SSO information in CloudTrail](sso-info-in-cloudtrail.md)
+ [Understanding AWS SSO log file entries](understanding-sso-entries.md)
+ [Understanding AWS SSO sign\-in events](understanding-sign-in-events.md)
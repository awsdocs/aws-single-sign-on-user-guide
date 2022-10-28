# Attribute\-based access control<a name="abac"></a>

Attribute\-based access control \(ABAC\) is an authorization strategy that defines permissions based on attributes\. You can use IAM Identity Center to manage access to your AWS resources across multiple AWS accounts using user attributes that come from any IAM Identity Center identity source\. In AWS, these attributes are called tags\. Using user attributes as tags in AWS helps you simplify the process of creating fine\-grained permissions in AWS and ensures that your workforce gets access only to the AWS resources with matching tags\.

For example, you can assign developers Bob and Sally, who are from two different teams, to the same permission set in IAM Identity Center and then select the team name attribute for access control\. When Bob and Sally sign in to their AWS accounts, IAM Identity Center sends their team name attribute in the AWS session so Bob and Sally can access AWS project resources only if their team name attribute matches the team name tag on the project resource\. If Bob moves to Sally’s team in the future, you can modify his access by simply updating his team name attribute in the corporate directory\. When Bob signs in next time, he will automatically get access to the project resources of his new team without requiring any permissions updates in AWS\. 

This approach also helps in reducing the number of distinct permissions you need to create and manage in IAM Identity Center as users associated with the same permission sets can now have unique permissions based on their attributes\. You can use these user attributes in IAM Identity Center permission sets and resource\-based policies to implement ABAC to AWS resources and simplify permissions management at scale\.

## Benefits<a name="abac-benefits"></a>

The following are additional benefits of using ABAC in IAM Identity Center\.
+ **ABAC requires fewer permission sets **– Because you don't have to create different policies for different job functions, you create fewer permission sets\. This reduces your permissions management complexity\.
+ **Using ABAC, teams can change and grow quickly **– Permissions for new resources are automatically granted based on attributes when resources are appropriately tagged upon creation\. 
+ **Use employee attributes from your corporate directory with ABAC **– You can use existing employee attributes from any identity source configured in IAM Identity Center to make access control decisions in AWS\.
+ **Track who is accessing resources **– Security administrators can easily determine the identity of a session by looking at the user attributes in AWS CloudTrail to track user activity in AWS\.

For information about how to configure ABAC using the IAM Identity Center console, see [Attributes for access control](attributesforaccesscontrol.md)\. For information about how to enable and configure ABAC using the IAM Identity Center APIs, see [CreateInstanceAccessControlAttributeConfiguration](https://docs.aws.amazon.com/singlesignon/latest/APIReference/API_CreateInstanceAccessControlAttributeConfiguration.html) in the *IAM Identity Center API Reference Guide*\.

**Topics**
+ [Benefits](#abac-benefits)
+ [Checklist: Configuring ABAC in AWS using IAM Identity Center](abac-checklist.md)
+ [Attributes for access control](attributesforaccesscontrol.md)
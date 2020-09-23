# Tagging AWS Single Sign\-On Resources<a name="tagging"></a>

A *tag* is a metadata label that you assign or that AWS assigns to an AWS resource\. Each tag consists of a *key* and a *value*\. For tags that you assign, you define the key and value\. For example, you might define the key as `stage` and the value for one resource as `test`\.

Tags help you do the following:
+ Identify and organize your AWS resources\. Many AWS services support tagging, so you can assign the same tag to resources from different services to indicate that the resources are related\. For example, you could assign the same tag to a specific permission set in your AWS SSO instance\.
+ Track your AWS costs\. You activate these tags on the AWS Billing and Cost Management dashboard\. AWS uses the tags to categorize your costs and deliver a monthly cost allocation report to you\. For more information, see [Use Cost Allocation Tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the *AWS Billing and Cost Management User Guide*\.
+ Control access to your resources based on the tags that are assigned to them\. You control access by specifying tag keys and values in the conditions for an AWS Identity and Access Management \(IAM\) policy\. For example, you could allow an IAM user to update an AWS SSO instance, but only if the AWS SSO instance has an `owner` tag with a value of that user's name\. For more information, see [Controlling Access Using Tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html) in the *IAM User Guide*\.

Currently, tags can only be applied to permission sets and cannot be applied to corresponding roles that AWS SSO creates in AWS accounts\. You can use the AWS SSO console, AWS CLI or the AWS SSO APIs to add, edit, or delete tags for a given permission set\.

For tips on using tags, see the [AWS Tagging Strategies](https://aws.amazon.com/answers/account-management/aws-tagging-strategies/) post on the *AWS Answers* blog\. 

The following sections provide more information about tags for AWS SSO\.

## Tag Restrictions<a name="tagging-restrictions"></a>

The following basic restrictions apply to tags on AWS SSO resources:
+ Maximum number of tags that you can assign to a resource – 50 
+ Maximum key length – 128 Unicode characters 
+ Maximum value length – 256 Unicode characters 
+ Valid characters for key and value – a\-z, A\-Z, 0\-9, space, and the following characters: \_ \. : / = \+ \- and @
+ Keys and values are case sensitive
+ Don't use `aws:` as a prefix for keys; it's reserved for AWS use

## Manage Tags Using the AWS SSO Console<a name="tagging-console"></a>

You can use the AWS SSO console to add, edit and remove tags that are associated with your permission sets\.

**To manage tags for an AWS SSO console**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. Choose the **Permission sets** tab\.

1. Choose the name of the permission set that has the tags you want to manage\.

1. On the **Permissions** tab, under **Tags** do one of the following, and then proceed to the next step:

   1. If you have existing tags assigned for this permission set, choose **Edit tags**\.

   1. If no tags have been assigned to this permission set, choose **Add tags**\.

1. For each new tag, type the values in the **Key** and **Value \(optional\)** columns\. When you are finished, choose **Save changes\.**

To remove a tag, choose the **X** in the **Remove** column next to the tag you want to remove\.

## AWS CLI Examples<a name="tagging-cli-examples"></a>

The AWS CLI provides commands that you can use to manage the tags that you assign to your permission set\. 

### Assigning tags<a name="tagging-cli-examples-assigning"></a>

Use the following commands to assign tags to your permission set\.

**Example `tag-resource` command for a permission set**  
Assign tags to a permission set by using [https://docs.aws.amazon.com/cli/latest/reference/sso-admin/tag-resource.html](https://docs.aws.amazon.com/cli/latest/reference/sso-admin/tag-resource.html) within the `sso` set of commands:  

```
$ aws sso tag-resource \
> --instance-arn sso-instance-arn \
> --resource-arn sso-resource-arn \
> --tags Stage=Test
```
This command includes the following parameters:  
+ `instance-arn` – The Amazon Resource Name \(ARN\) of the AWS SSO instance under which the operation will be executed\. 
+ `resource-arn` – The ARN of the resource with the tags to be listed\. 
+ `tags` – The key\-value pairs of the tags\.
To assign multiple tags at once, specify them in a comma\-separated list:  

```
$ aws sso tag-resource \
> --instance-arn sso-instance-arn \
> --resource-arn sso-resource-arn \
> --tags Stage=Test,CostCenter=80432,Owner=SysEng
```

### Viewing tags<a name="tagging-cli-examples-viewing"></a>

Use the following commands to view the tags that you have assigned to your permission set\.

**Example `list-tags-for-resource` command for a permission set**  
View the tags that are assigned to a permission set by using [https://docs.aws.amazon.com/cli/latest/reference/sso-admin/list-tags-for-resource.html](https://docs.aws.amazon.com/cli/latest/reference/sso-admin/list-tags-for-resource.html) within the `sso` set of commands:  

```
$ aws sso list-tags-for-resource --resource-arn sso-resource-arn
```

### Removing tags<a name="tagging-cli-examples-removing"></a>

Use the following commands to remove tags from a permission set\.

**Example `untag-resource` command for a permission set**  
Remove tags from a permission set by using [https://docs.aws.amazon.com/cli/latest/reference/sso-admin/untag-resource.html](https://docs.aws.amazon.com/cli/latest/reference/sso-admin/untag-resource.html) within the `sso` set of commands:  

```
$ aws sso untag-resource \
> --instance-arn sso-instance-arn \
> --resource-arn sso-resource-arn \
> --tag-keys Stage CostCenter Owner
```
For the `--tag-keys` parameter, specify one or more tag keys, and do not include the tag values\.

### Applying tags when you create a permission set<a name="tagging-cli-examples-applying"></a>

Use the following commands to assign tags at the moment you create a permission set\.

**Example `create-permission-set` command with tags**  
When you create a permission set by using the [https://docs.aws.amazon.com/cli/latest/reference/sso-admin/create-permission-set.html](https://docs.aws.amazon.com/cli/latest/reference/sso-admin/create-permission-set.html) command, you can specify tags with the `--tags` parameter:  

```
$ aws sso create-permission-set \
> --instance-arn sso-instance-arn \
> --name permission=set-name \
> --tags Stage=Test,CostCenter=80432,Owner=SysEng
```

## Manage Tags Using the AWS SSO API<a name="tagging-api"></a>

You can use the following actions in the AWS SSO API to manage the tags for your permission set\.

### API Actions for AWS SSO instance Tags<a name="tagging-api-user-pools"></a>

Use the following API actions to assign, view, and remove tags for a permission set\.
+ [TagResource](https://docs.aws.amazon.com/singlesignon/latest/APIReference/API_TagResource.html)
+ [ListTagsForResource](https://docs.aws.amazon.com/singlesignon/latest/APIReference/API_ListTagsForResource.html)
+ [UntagResource](https://docs.aws.amazon.com/singlesignon/latest/APIReference/API_UntagResource.html)
+ [CreatePermissionSet](https://docs.aws.amazon.com/singlesignon/latest/APIReference/API_CreatePermissionSet.html)
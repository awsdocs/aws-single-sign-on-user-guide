# Create a permission set<a name="howtocreatepermissionset"></a>

Use this procedure to create a predefined permission set that uses a single AWS managed policy, or a custom permission set that uses up to 10 AWS managed or customer managed policies and an inline policy\. You can request an adjustment to the maximum number of 10 policies in the [Service Quotas console](https://console.aws.amazon.com/servicequotas) for IAM\.

You can create a permission set in the AWS Management Console\.

Use this procedure to create a predefined permission set that uses a single AWS managed policy, or a custom permission set that uses up to 10 AWS managed or customer managed policies and an inline policy\.

**To create a permission set**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Under **Multi\-account permissions**, choose **Permission sets**\.

1. Choose **Create permission set**\.

1. On the **Select permission set type** page, under **Permission set type**, select a permission set type\.

1. Choose one or more policies that you want to use for the permission set, based on the permission set type:
   + **Predefined permission set**

     1. Choose **Next**\.

     1. Under **Predefined policy**, select one of the IAM **Job function policies** or **Common permission policies** in the list, and then choose **Next**\. For more information, see [AWS managed policies for job functions](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) and [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *AWS Identity and Access Management User Guide*\.

     1. At the **Review and create** screen, review the selections you made, and then choose **Create**\.
   + **Custom permission set**

     1. Choose **Next**\.

     1. On the **Specify policies** page, choose the types of IAM policies that you want to apply to your new permission set\. By default, you can add any combination of up to 10 **AWS managed policies** and **Customer managed policies** to your permission set\. This quota is set by IAM\. To raise it, request an increase to the IAM quota *Managed policies attached to an IAM role* in the Service Quotas console in each AWS account where you want to assign the permission set\.
        + Expand **AWS managed policies** to add policies from IAM that AWS builds and maintains\. For more information, see [AWS managed policies](permissionsetcustom.md#permissionsetsampconcept)\.

          1. Search for and choose **AWS managed policies** that you want to apply to your users in the permission set\.

          1. If you want to add another type of policy, choose its container and make your selection\. Choose **Next** when you've chosen all the policies that you want to apply\.
        + Expand **Customer managed policies** to add policies from IAM that you build and maintain\. For more information, see [Customer managed policies](permissionsetcustom.md#permissionsetscmpconcept)\.

          1. Choose **Attach policies** and enter the name of a policy that you want to add to your permission set\. In each account where you want to assign the permission set, create a policy with the name you entered\. As a best practice, assign the same permissions to the policy in each account\.

          1. Choose **Attach more** to add another policy\.

          1. If you want to add another type of policy, choose its container and make your selection\. Choose **Next** when you've chosen all the policies that you want to apply\.
        + Expand **Custom inline policy** to add custom JSON\-formatted policy text\. Inline policies don't correspond to existing IAM resources\. To create an inline policy, enter custom policy language in the provided form\. IAM Identity Center adds the policy to the IAM resources that it creates in your member accounts\. For more information, see [Inline policies](permissionsetcustom.md#permissionsetsinlineconcept)\.

          1. Choose **Design** to use an interactive editor to choose permissions that you want to include in your inline policy\. Choose **Code** to paste in preformatted policy JSON\.

          1. If you want to add another type of policy, choose its container and make your selection\. Choose **Next** when you've chosen all the policies that you want to apply\.
        + Expand **Permissions boundary** to add an AWS managed or customer managed IAM policy as the maximum permissions that your other policies in the permission set can assign\. For more information, see [Permissions boundaries](permissionsetcustom.md#permissionsetsboundaryconcept)\.

          1. Choose **Use a permissions boundary to control the maximum permissions**\.

          1. Choose **AWS managed policy** to set a policy from IAM that *AWS* builds and maintains as your permissions boundary\. Chose **Customer managed policies** to set a policy from IAM that *you* build and maintain as your permissions boundary\.

          1. If you want to add another type of policy, choose its container and make your selection\. Choose **Next** when you've chosen all the policies that you want to apply\.

1. On the **Specify permission set details** page, do the following:

   1. Under **Permission set name**, type a name to identify this permission set in IAM Identity Center\. The name that you specify for this permission set appears in the AWS access portal as an available role\. Users sign into the AWS access portal, choose an AWS account, and then choose the role\. 

   1. \(Optional\) You can also type a description\. The description appears in the IAM Identity Center console only, not the AWS access portal\.

   1. \(Optional\) Specify the value for **Session duration**\. This value determines the length of time that a user can be logged on before the console logs them out of their session\. For more information, see [Set session duration](howtosessionduration.md)\.

   1. \(Optional\) Specify the value for **Relay state**\. This value is used in the federation process to redirect users within the account\. For more information, see [Set relay state](howtopermrelaystate.md)\.

   1. Expand **Tags \(optional\)**, choose **Add tag**, and then specify values for **Key** and **Value \(optional\)**\. 

      For information about tags, see [Tagging AWS IAM Identity Center \(successor to AWS Single Sign\-On\) resources](tagging.md)\.

   1. Choose **Next**\.

1. On the **Review and create** page, review the selections that you made, and then choose **Create**\.

1. By default, when you create a permission set, the permission set isn't provisioned \(used in any AWS accounts\)\. To provision a permission set in an AWS account, you must assign IAM Identity Center access to users and groups in the account, and then apply the permission set to those users and groups\. For more information, see [Single sign\-on access](useraccess.md)\.
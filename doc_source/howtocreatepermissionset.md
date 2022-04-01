# Create a permission set<a name="howtocreatepermissionset"></a>

Use this procedure to create a predefined permission set that uses a single AWS managed policy, or a custom permission set that uses up to 10 AWS managed policies and an inline policy\.

**To create a permission set**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Permission sets**\.

1. Choose **Create permission set**\.

1. On the **Select permission set type** page, under **Permission set type**, select a permission set type\.

1. Specify one or more policies as required for the permission set, based on the permission set type:
   + **Predefined permission set**

     1. Choose **Predefined permission set**\.

     1. Under **Policy for predefined permission set**, select an AWS managed policy\.

        For more information, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies)\.

     1. Choose **Next**\.
   + **Custom permission set**

     1. Choose **Custom permission set**, and then choose **Next**\.

     1. On the **Specify policies **page, do either or both of the following:
        + To specify one or more AWS managed policies, expand **AWS managed policies**, and then select up to 10 policies from the list\. 
        + To specify an inline policy, expand **Inline policy**, and then create or paste a policy document that specifies custom permissions\. For a list of example policies to use for delegating AWS SSO tasks, see [Custom policy examples](iam-auth-access-using-id-policies.md#policyexample)\.

          When you create a JSON policy or edit an existing policy, the policy is validated automatically\. If the policy syntax is not valid, you receive a notification and must fix the problem before you can continue\. The findings from the policy validation are automatically returned if you have permissions for `access-analyzer:ValidatePolicy`\.

     1. Choose **Next**\.

1. On the **Specify permission set details** page, do the following:

   1. Under **Permission set name**, type a name to identify this permission set in AWS SSO\. The name that you specify for this permission set appears in the AWS SSO user portal as an available role\. Users sign into the user portal, choose an AWS account, and then choose the role\. 

   1. \(Optional\) You can also type a description\. The description appears in the AWS SSO console only, not the user portal\.

   1. \(Optional\) Specify the value for **Session duration**\. This value determines the length of time that a user can be logged on before the console logs them out of their session\. For more information, see [Set session duration](howtosessionduration.md)\.

   1. \(Optional\) Specify the value for **Relay state**\. This value is used in the federation process to redirect users within the account\. For more information, see [Set relay state](howtopermrelaystate.md)\.

   1. Expand **Tags \(optional\)**, choose **Add tag**, and then specify values for **Key** and **Value \(optional\)**\. 

      For information about tags, see [Tagging AWS Single Sign\-On resources](tagging.md)\.

   1. Choose **Next**\.

1. On the **Review and create** page, review the selections that you made, and then choose **Create**\.

1. By default, when you create a permission set, the permission set isn't provisioned \(used in any AWS accounts\)\. To provision a permission set in an AWS account, you must assign AWS SSO access to users and groups in the account, and then apply the permission set to those users and groups\. For more information, see [Single sign\-on access](useraccess.md)\.
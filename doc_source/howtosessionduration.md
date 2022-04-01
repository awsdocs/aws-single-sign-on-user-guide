# Set session duration<a name="howtosessionduration"></a>

For each [permission set](https://docs.aws.amazon.com/singlesignon/latest/userguide/permissionsetsconcept.html), you can specify a session duration to control the length of time that a user can be signed in to an AWS account\. When the specified duration elapses, AWS signs the user out of the session\. 

When you create a new permission set, the session duration is set to 1 hour \(in seconds\) by default\. The minimum session duration is 1 hour, and can be set to a maximum of 12 hours\. AWS SSO automatically creates IAM roles in each assigned account for each permission set, and configures these roles with a maximum session duration of 12 hours\.

When users federate into their AWS account console or when the AWS Command Line Interface \(CLI\) is used, AWS SSO uses the session duration setting on the permission set to control the duration of the session\. By default, AWS SSO\-generated IAM roles for permission sets can only be assumed by AWS SSO users, which ensures that the session duration specified in the AWS SSO permission set is enforced\.

**Important**  
As a security best practice, we recommend that you do not set the session duration length longer than is needed to perform the role\.

After you create a permission set, you can update it to apply a new session duration\. Use the following procedure to modify the session duration length for a permission set\.

**To set the session duration**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Permission sets**\.

1. Choose the name of the permission set for which you want to change the session duration\.

1. On the details page for the permission set, to the right of the **General settings** section heading, choose **Edit**\.

1. On the **Edit general permission set settings** page, choose a new value for **Session duration**\.

1. If the permission set is provisioned in any AWS accounts, the names of the accounts appear under **AWS accounts to reprovision automatically**\. After the session duration value for the permission set is updated, all AWS accounts that use the permission set are reprovisioned\. This means that the new value for this setting is applied to all AWS accounts that use the permission set\.

1. Choose **Save changes**\.

1. At the top of the **AWS Organization** page, a notification appears\.
   + If the permission set is provisioned in one or more AWS accounts, the notification confirms that the AWS accounts were reprovisioned successfully, and the updated permission set was applied to the accounts\.
   + If the permission set isn't provisioned in an AWS account, the notification confirms that the settings for the permission set were updated\.
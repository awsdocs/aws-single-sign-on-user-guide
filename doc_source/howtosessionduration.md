# Set session duration<a name="howtosessionduration"></a>

For each [permission set](https://docs.aws.amazon.com/singlesignon/latest/userguide/permissionsetsconcept.html), you can specify a session duration to control the length of time that a user can be signed in to an AWS account\. When the specified duration has elapsed, AWS signs the user out of the session\. 

When you create a new permission set, the session duration is set to 1 hour \(in seconds\) by default\. The minimum session duration is 1 hour, and can be set to a maximum of 12 hours\. AWS SSO automatically creates IAM roles in each assigned account for each permission set, and configures these roles with a maximum session duration of 12 hours\.

When users federate into their AWS account console or when the AWS Command Line Interface \(CLI\) is used, AWS SSO uses the session duration setting on the permission set to control the duration of the session\. By default, AWS SSO\-generated IAM roles for permission sets can only be assumed by SSO users, which ensures that the session duration specified in the SSO permission set is enforced\.

**Important**  
As a security best practice, we recommend that you do not set the session duration length longer than is needed to perform the role\.

After you create a permission set, you can update it to apply a new session duration\. Use the following procedure to modify the session duration length for a given permission set\.

**To set the session duration**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Permission sets**\.

1. Choose the name of the permission set for which you want to change the session duration\.

1. On the **Permissions** tab, under the **General** section, choose **Edit**\.

1. For **Session duration**, choose a new value, and then choose **Continue**\.

1. Select one or more AWS accounts in the list that you want the new session duration value to apply to, and then choose **Reprovision**\.
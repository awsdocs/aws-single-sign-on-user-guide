# Manage AWS access portal sessions<a name="manage-user-session"></a>

Use the following procedure to manage sessions for a user in your IAM Identity Center store\. 

**To manage an AWS access portal session**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Users**\.

1. On the **Users** page, choose the username of the user whose sessions you want to manage\. This takes you to a page with the user’s information\.

1. On the user’s page, choose the **Active sessions** tab\. The number in parentheses next to **Active sessions** indicates the number of current active sessions for this user\.

1. Select the check boxes beside the sessions that you want to delete, and then choose **Delete session**\. A dialog box appears that confirms you're deleting active sessions for this user\. Read the information in the dialog box, and if you want to continue, choose **Delete session**\.
**Note**  
Deleting a session ends the AWS access portal session, but it does not affect the user's active AWS Management Console sessions that they created by choosing a permission set from the AWS access portal\. Those sessions will continue until the permission set session duration elapses or the user signs out of the session\. This also does not affect any active SAML application sessions\. Those sessions continue until the user signs out of the application or the application ends its session with the user\. For IAM Identity Center integrated applications such as Amazon SageMaker Studio or Amazon Monitron, those sessions end the next time the application checks to see if the AWS access portal session is still active for up to 2 hours, or if the user signs out of the application\.
**Note**  
When you delete a session, any running AWS CLI sessions are also revoked\. Revoking these sessions does not happen immediately and can take up to an hour\.

1. You return to the user's page\. A green flash bar appears to indicate that the selected sessions were successfully deleted\.
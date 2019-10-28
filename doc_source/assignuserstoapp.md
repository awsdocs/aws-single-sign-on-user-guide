# Assign User Access<a name="assignuserstoapp"></a>

Use the following procedure to assign users SSO access to cloud applications or custom SAML 2\.0 applications\.

**Note**  
To help simplify administration of access permissions, we recommend that you assign access directly to groups rather than to individual users\. With groups you can grant or deny permissions to groups of users, rather than having to apply those permissions to each individual\. If a user moves to a different organization, you simply move that user to a different group\. The user then automatically receives the permissions that are needed for the new organization\.
When assigning user access to applications, AWS SSO does not currently support users being added to nested groups\. If a user is added to a nested group, they may receive a “You do not have any applications” message during sign\-in\. Assignments must be made against the immediate group the user is a member of\.

**To assign access to users or groups**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the AWS SSO console is using the Region where your AWS Managed Microsoft AD directory is located before taking the next step\.

1. Choose **Applications**\.

1. In the list of applications, choose an application to which you want to assign access\. 

1. On the application details page, choose the **Assigned users** tab\. Then choose **Assign users**\.

1. In the **Assign users** dialog box, enter a user or group name\. Then choose **Search connected directory**\. You can specify multiple users or groups by selecting the applicable accounts as they appear in search results\. 

1. Choose **Assign users**\.
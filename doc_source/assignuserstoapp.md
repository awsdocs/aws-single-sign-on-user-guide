# Assign User Access<a name="assignuserstoapp"></a>

Use the following procedure to assign users SSO access to cloud applications or custom SAML 2\.0 applications\.

**Note**  
To help simplify administration of access permissions, we recommended that you assign access directly to groups rather than to individual users\. With groups you can grant or deny permissions to groups of users, rather than having to apply those permissions to each individual\. If a user moves to a different organization, you simply move that user to a different group and they automatically receive the permissions that are needed for the new organization\.

**To assign access to users or groups**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.
**Note**  
Make sure that the AWS SSO console is using the US East \(N\. Virginia\) Region where your AWS Microsoft AD directory is located before you move to the next step\.

1. Choose **Applications**\.

1. In the list of applications, choose an application to which you want to assign access\. 

1. On the application details page, select the **Assigned users** tab\. Then choose **Assign users**\.

1. In the **Assign users** dialog box, type a user or group name\. Then choose **Search connected directory**\. You can specify multiple users or groups by selecting the applicable accounts as they appear in search results\. 

1. Choose **Assign users**\.
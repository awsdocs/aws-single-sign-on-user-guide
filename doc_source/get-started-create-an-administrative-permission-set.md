# Step 3: Create an administrative permission set<a name="get-started-create-an-administrative-permission-set"></a>

Permission sets are stored in IAM Identity Center and define the level of access that users and groups have to an AWS account\. Perform the following steps to create a permission set that grants administrative permissions\. 

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon) using your AWS account root user credentials\.

1. In the IAM Identity Center navigation pane, under **Multi\-account permissions**, choose **Permission sets**\.

1. Choose **Create permission set**\.

1. **For Step 1: Select permission set type**, on the **Select permission set type** page, keep the default settings and choose **Next**\. The default settings grant full access to AWS services and resources using the **AdministratorAccess** predefined permission set\. 
**Note**  
The predefined **AdministratorAccess** permission set uses the **AdministratorAccess** AWS managed policy\.

1. **For Step 2: Specify permission set details**, on the **Specify permission set details** page, keep the default settings and choose **Next**\. The default setting limits your session to one hour\.

1. **For Step 3: Review and create**, on the **Review and create** page, do the following:

   1. Review the permission set type and confirm that it is **AdministratorAccess**\.

   1. Review the AWS managed policy and confirm that it is **AdministratorAccess**\.

   1. Choose **Create**\.
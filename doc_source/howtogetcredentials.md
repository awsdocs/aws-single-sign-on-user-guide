# How to Get Credentials of an IAM Role for Use with CLI Access to an AWS Account<a name="howtogetcredentials"></a>

Use this procedure in the user portal when you need temporary security credentials for short\-term access to resources in an AWS account using the AWS CLI\. The user portal makes it easy for you to quickly select an AWS account and get the temporary credentials for a given IAM role\. You can then copy the necessary CLI syntax \(including all necessary credentials\) and paste them into your AWS CLI command prompt\. 

By default, credentials retrieved through the user portal are valid for 1 hour\. You can change this value up to 12 hours\. Once you have completed this procedure, you can run any AWS CLI command \(that your administrator has given you access to\) until those temporary credentials have expired\.

**Note**  
Before you get started with the steps in this procedure, you must first install the AWS CLI\. For instructions, see [Installing the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)\.

**To get temporary credentials of an IAM role for CLI access to an AWS account**

1. While signed into the portal, choose the **AWS Accounts** icon ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/singlesignon/latest/userguide/images/aws_accounts_icon.png) to expand the list of accounts\.

1. Choose the AWS account from which you want to retrieve access credentials\. Then, next to the IAM role name \(for example **Administrator**\), choose **Command line or programmatic access**\.

1. In the **Get credentials** dialog box, choose either **MacOS and Linux** or **Windows**, depending on the operating system where you plan to use the CLI command prompt\.

1. Depending on how you want to use the temporary credentials, choose one or more of the following options:
   + If you need to run commands from the AWS CLI in the selected AWS account, under **Option 1: Set AWS environment variables**, pause on the commands\. Then choose **Copy**\. Paste the commands into the CLI terminal window and press **Enter** to set the necessary environment variables\.
   + If you need to run commands from multiple command prompts in the same AWS account, under **Option 2: Add a profile to your AWS credentials file**, pause on the commands\. Then choose **Copy**\. Paste the commands into your AWS credentials file to set up a newly named profile\. For more information, see [Configuration and Credential Files](https://docs.aws.amazon.com/cli/latest/userguide/cli-config-files.html) in the *AWS CLI User Guide*\. Modifying the credential files in this way enables the `--profile` option in your AWS CLI command so that you can use this credential\. This affects all command prompts that use the same credential file\.
   + If you need to access AWS resources from an AWS service client, under **Option 3: Use individual values in your AWS service client**, choose **Copy** next to the commands you need to use\. For more information, see [Configuration and Credential File Settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-config-files.html) in the *AWS CLI User Guide* or see [Tools for Amazon Web Services](https://aws.amazon.com/tools/)\.

1. Continue using the AWS CLI as necessary for your AWS account until the credentials have expired\. 
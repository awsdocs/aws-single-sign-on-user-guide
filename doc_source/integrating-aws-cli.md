# Integrating AWS CLI with IAM Identity Center<a name="integrating-aws-cli"></a>

AWS Command Line Interface \(CLI\) version 2 integration with IAM Identity Center simplifies the sign\-in process\. Developers can sign in directly to the AWS CLI using the same Active Directory or IAM Identity Center credentials that they normally use to sign in to IAM Identity Center, and access their assigned accounts and roles\. For example, after an administrator configures IAM Identity Center to use Active Directory for authentication, a developer can sign into the AWS CLI directly using their Active Directory credentials\. 

AWS CLI integration with IAM Identity Center offers the following benefits:
+ Enterprises can enable their developers to sign in using credentials from IAM Identity Center or Active Directory by connecting IAM Identity Center to their Active Directory using AWS Directory Service\.
+ Developers can sign in from the CLI for faster access\.
+ Developers can list and switch between accounts and roles to which they have assigned access\.
+ Developers can generate and save named role profiles in their CLI configuration automatically and reference them in the CLI to run commands in desired accounts and roles\.
+ The CLI manages short\-term credentials automatically so developers can start in and stay in the CLI securely without interruption, and run long running scripts\.

## How to integrate AWS CLI with IAM Identity Center<a name="how-to-integrate-aws-cli"></a>

To use the AWS CLI integration with IAM Identity Center, you need to download, install, and configure AWS Command Line Interface version 2\. For detailed steps on how to download and integrate the AWS CLI with IAM Identity Center, see [Configuring the AWS CLI to use IAM Identity Center](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html) in the *AWS Command Line Interface User Guide*\.
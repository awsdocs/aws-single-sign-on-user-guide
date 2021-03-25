# Integrating AWS CLI with AWS SSO<a name="integrating-aws-cli"></a>

AWS Command Line Interface \(CLI\) version 2 integration with AWS Single Sign\-On \(AWS SSO\) simplifies the sign\-in process\. Developers can sign in directly to the AWS CLI using the same Active Directory or AWS SSO credentials that they normally use to sign in to AWS SSO, and access their assigned accounts and roles\. For example, after an administrator configures AWS SSO to use Active Directory for authentication, a developer can sign into the AWS CLI directly using their Active Directory credentials\. 

AWS CLI integration with AWS SSO offers the following benefits:
+ Enterprises can enable their developers to sign in using credentials from AWS SSO or Active Directory by connecting AWS SSO to their Active Directory using AWS Directory Service\.
+ Developers can sign in from the CLI for faster access\.
+ Developers can list and switch between accounts and roles to which they have assigned access\.
+ Developers can generate and save named role profiles in their CLI configuration automatically and reference them in the CLI to run commands in desired accounts and roles\.
+ The CLI manages short\-term credentials automatically so developers can start in and stay in the CLI securely without interruption, and run long running scripts\.

## How to integrate AWS CLI with AWS SSO<a name="how-to-integrate-aws-cli"></a>

To use the AWS CLI integration with AWS SSO, you need to download, install, and configure AWS Command Line Interface version 2\. For detailed steps on how to download and integrate the AWS CLI with AWS SSO, see [Configuring the AWS CLI to use AWS Single Sign\-On \(AWS SSO\)](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html) in the *AWS Command Line Interface User Guide*\.
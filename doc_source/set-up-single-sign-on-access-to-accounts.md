# Step 6: Set up AWS account access for additional users \(optional\)<a name="set-up-single-sign-on-access-to-accounts"></a>

Now that you've created an administrative user in IAM Identity Center, you can add other users by doing any of the following:
+ [Synchronizing your users from Active Directory](provision-users-groups-AD.md)
+ [Synchronizing your users from your external identity provider \(IdP\)](manage-your-identity-source-idp.md#provisioning-when-external-idp)
+ [Creating your users in IAM Identity Center](addusers.md)

After you add other users, create permission sets for these users and assign the users to the new permission sets as needed to grant them single sign\-on access to one or more AWS accounts in your organization\.

If you are using the default Identity Center directory as an identity source, after your users [accept their invitation](howtoactivateaccount.md) to activate their account and they sign into the AWS access portal, the only icons that appear in the portal are for the AWS accounts to which the users are assigned\. Users who are assigned to multiple permission sets can sign in to the AWS access portal, choose an account, and then choose a role that was created from an assigned permission set\. 

For information about how to assign additional users single sign\-on access to your AWS accounts by using the console, see [Assign user access to AWS accounts](useraccess.md#assignusers)\. Alternatively, you can use [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_SSO.html) to create and assign permission sets and assign users to those permission sets\. Users can then [sign in to the AWS access portal](howtosignin.md) or use [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/singlesignon/latest/userguide/integrating-aws-cli.html) commands\.
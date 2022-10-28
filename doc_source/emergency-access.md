# Set up emergency access to the AWS Management Console<a name="emergency-access"></a>

IAM Identity Center is built from highly available AWS infrastructure and uses an Availability Zone architecture to eliminate single points of failure\. For an extra layer of protection in the unlikely event of an IAM Identity Center or AWS Region disruption, we recommend that you set up a configuration that you can use to provide temporary access to the AWS Management Console\.

**Topics**
+ [Overview](#emergency-access)
+ [Summary of emergency access configuration](#emergency-access-implementation)
+ [How to design your critical operations roles](#emergency-access-implementation-design)
+ [How to plan your access model](#emergency-access-planning)
+ [How to design emergency role, account, and group mapping](#emergency-access-mapping-design)
+ [How to create your emergency access configuration](#emergency-access-role-idp-group-creation-mapping-plan)
+ [Emergency preparation tasks](#emergency-access-prepare-configuration)
+ [Emergency failover process](#emergency-access-failover-steps)
+ [Return to normal operations](#emergency-access-return-to-normal-operations)
+ [One\-time setup of a direct IAM federation application in Okta](#emergency-access-one-time-setup-direct-IAM-federation-application-in-idp)

## Overview<a name="emergency-access"></a>

AWS enables you to:
+ [Connect your third\-party IdP to IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-idp.html)\.
+ Connect your third\-party IdP to individual AWS accounts by using [SAML 2\.0\-based federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_saml.html)\.

If you use IAM Identity Center, you can use these capabilities to create the emergency access configuration described in the following sections\. This configuration enables you to use IAM Identity Center as the mechanism for AWS account access\. If IAM Identity Center is disrupted, your emergency operations users can sign in to the AWS Management Console through direct federation, by using the same credentials that they use to access their accounts\. This configuration works when IAM Identity Center is unavailable, but the IAM data plane and your external identity provider \(IdP\) are available\.

**Important**  
We recommend that you deploy this configuration before a disruption occurs because you can't create the configuration if your access to create the required IAM roles is also disrupted\. Also, test this configuration periodically to ensure that your team understands what to do if IAM Identity Center is disrupted\.

## Summary of emergency access configuration<a name="emergency-access-implementation"></a>

To configure emergency access, you must complete the following tasks:

1. [Create an emergency operations account in your organization in AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts_create.html)\.

1. Connect your IdP to the emergency operations account by using [SAML 2\.0\-based federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_saml.html)\.

1. In the emergency operations account, [create a role for third\-party identity provider federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp.html)\. Also, create an emergency operations role in each of your workload accounts, with your required permissions\.

1. [Delegate access to your workload accounts for the IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html) that you created in the emergency operations account\. To authorize access to your emergency operations account, create an emergency operations group in your IdP, with no members\. 

1. Enable the emergency operations group in your IdP to use the emergency operations role by creating a rule in your IdP that [enables SAML 2\.0 federated access to the AWS Management Console](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html)\.

During normal operations, no one has access to the emergency operations account because the emergency operations group in your IdP has no members\. In the event of an IAM Identity Center disruption, use your IdP to add trusted users to the emergency operations group in your IdP\. These users can then sign in to your IdP, navigate to the AWS Management Console, and assume the emergency operations role in the emergency operations account\. From there, these users can [switch roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-console.html) to the emergency access role in your workload accounts where they need to perform operations work\.

## How to design your critical operations roles<a name="emergency-access-implementation-design"></a>

With this design, you configure a single AWS account in which you federate through IAM, so that users can assume critical operations roles\. The critical operations roles have a trust policy that enables users to assume a corresponding role in your workload accounts\. The roles in the workload accounts provide the permissions that users require to perform essential work\. The following diagram provides a design overview\.

![\[IAM Identity Center workflow for setting up a trust policy and emergency operations role to provide permissions for essential work in an emergency operations account.\]](http://docs.aws.amazon.com/singlesignon/latest/userguide/images/emergency-access-design.png)

## How to plan your access model<a name="emergency-access-planning"></a>

Before you configure emergency access, create a plan for how the access model will work\. Use the following process to create this plan\.

1. Identify the AWS accounts where emergency operator access is essential during a disruption to IAM Identity Center\. For example, your production accounts are probably essential, but your development and test accounts might not be\.

1. For that collection of accounts, identify the specific critical roles that you need in your accounts\. Across these accounts, be consistent in defining what the roles can do\. This simplifies work in your emergency access account where you create cross\-account roles\. We recommend that you start with two distinct roles in these accounts: Read Only \(RO\) and Operations \(Ops\)\. If required, you can create more roles and map these roles to a more distinct group of emergency access users in your setup\.

1. Identify and create emergency access groups in your IdP\. The group members are the users to whom you are delegating access to emergency access roles\.

1. Define which roles these groups can assume in the emergency access account\. To do this, define rules in your IdP that generate claims that list which roles the group can access\. These groups can then assume your Read Only or Operations roles in emergency access account\. From those roles, they can assume corresponding roles in your workload accounts\. 

## How to design emergency role, account, and group mapping<a name="emergency-access-mapping-design"></a>

The following diagram shows how to map your emergency access groups to roles in your emergency access account\. The diagram also shows the cross\-account role trust relationships that enable emergency access account roles to access corresponding roles in your workload accounts\. We recommend that your emergency plan design use these mappings as a starting point\.

![\[IAM Identity Center workflow for mapping your emergency access groups to roles in your emergency access account.\]](http://docs.aws.amazon.com/singlesignon/latest/userguide/images/emergency-access-mapping.png)

## How to create your emergency access configuration<a name="emergency-access-role-idp-group-creation-mapping-plan"></a>

Use the following mapping table to create your emergency access configuration\. This table reflects a plan that includes two roles in the workload accounts: Read Only \(RO\) and Operations \(Ops\) , with corresponding trust policies and permissions policies\. The trust policies enable the emergency access account roles to access the individual workload account roles\. The individual workload account roles also have permissions policies for what the role can do in the account\. The permissions policies can be [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) or [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies)\.


****  

| Account | Roles to create | Trust policy | Permissions policy | 
| --- | --- | --- | --- | 
| Account 1 | EmergencyAccess\_RO | EmergencyAccess\_Role1\_RO |  arn:aws:iam::aws:policy/ReadOnlyAccess  | 
| Account 1 | EmergencyAccess\_Ops | EmergencyAccess\_Role1\_Ops |  arn:aws:iam::aws:policy/job\-function/SystemAdministrator  | 
| Account 2 | EmergencyAccess\_RO | EmergencyAccess\_Role2\_RO |  arn:aws:iam::aws:policy/ReadOnlyAccess  | 
| Account 2 | EmergencyAccess\_Ops | EmergencyAccess\_Role2\_Ops |  arn:aws:iam::aws:policy/job\-function/SystemAdministrator  | 
| Emergency access account |  EmergencyAccess\_Role1\_RO EmergencyAccess\_Role1\_Ops EmergencyAccess\_Role2\_RO EmergencyAccess\_Role2\_Ops  | IdP |  AssumeRole for role resource in account  | 

In this mapping plan, the emergency access account contains two read\-only roles and two operations roles\. These roles trust your IdP to authenticate and authorize your selected groups to access the roles by passing the names of the roles in assertions\. There are corresponding read\-only and operations roles in workload Account 1 and Account 2\. For workload Account 1, the `EmergencyAccess_RO` role trusts the `EmergencyAccess_Role1_RO` role that resides in the emergency access account\. The table specifies similar trust patterns between the workload account read\-only and operations roles and the corresponding emergency access roles\.

## Emergency preparation tasks<a name="emergency-access-prepare-configuration"></a>

To prepare your emergency access configuration, we recommend that you perform the following tasks before an emergency occurs\. 

1. Set up a direct IAM federation application in your IdP\. For more information, see [One\-time setup of a direct IAM federation application in Okta](#emergency-access-one-time-setup-direct-IAM-federation-application-in-idp)\.

1. Create an IdP connection in the emergency access account that can be accessed during the event\.

1. Create emergency access roles in the emergency access accounts as described in the mapping table above\.

1. Create temporary operations roles with trust and permission policies in each of the workload accounts\.

1. Create temporary operations groups in your IdP\. The group names will depend on the names of the temporary operations roles\.

1. Test direct IAM federation\.

1. Disable the IdP federation application in your IdP to prevent regular usage\.

## Emergency failover process<a name="emergency-access-failover-steps"></a>

When an IAM Identity Center instance isn't available and you determine that you must provide emergency access to the AWS Management Console, we recommend the following failover process\.

1. The IdP administrator enables the direct IAM federation application in your IdP\.

1. Users request access to the temporary operations group through your existing mechanism, such as an email request, Slack channel, or other form of communication\.

1. Users that you add to your emergency access groups sign in to the IdP, select the emergency access account, and, users choose a role to use in the emergency access account\. From these roles, they can assume roles in corresponding workload accounts that have cross\-account trust with the emergency account role\.

## Return to normal operations<a name="emergency-access-return-to-normal-operations"></a>

Check the [AWS Health Dashboard](https://health.aws.amazon.com/health/status)to confirm when the health of the IAM Identity Center service is restored\. To return to normal operations, perform the following steps\.

1. After the status icon for the IAM Identity Center service indicates that the service is healthy, sign in to IAM Identity Center\.

1. If you can sign in to IAM Identity Center successfully, communicate to emergency access users that IAM Identity Center is available\. Instruct these users to sign out and use the AWS access portal to sign back in to IAM Identity Center\.

1. After all emergency access users sign out, in the IdP, disable the IdP federation application\. We recommend that you perform this task after working hours\.

1. Remove all users from the emergency access group in the IdP\.

Your emergency access role infrastructure remains in place as a backup access plan, but it is now disabled\.

## One\-time setup of a direct IAM federation application in Okta<a name="emergency-access-one-time-setup-direct-IAM-federation-application-in-idp"></a>

1. Sign in to your Okta account as a user with administrative permissions\.

1. In the Okta Admin Console, under **Applications**, choose **Applications\.**

1. Choose **Browse App Catalog**\. Search for and choose **AWS Account Federation**\. Then choose **Add integration**\.

1. Set up direct IAM federation with AWS by following the steps in [ How to Configure SAML 2\.0 for AWS Account Federation](https://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-for-Amazon-Web-Service.html)\.

1. On the **Sign\-On Options** tab, select SAML 2\.0 and enter **Group Filter** and **Role Value Pattern** settings\. The name of the group for the user directory depends on the filter that you configure\.  
![\[Two different options that show where your accountid and role can be found in a group filter or role value pattern.\]](http://docs.aws.amazon.com/singlesignon/latest/userguide/images/emergency-access-group-filter-role-value-pattern.png)

   In the figure above, the `role` variable is for the emergency operations role in your emergency access account\. For example, if you create the `EmergencyAccess_Role1_RO` role \(as described in the mapping table\) in AWS account `123456789012`, and if your group filter setting is configured as shown in the figure above, your group name should be `aws#EmergencyAccess_Role1_RO#123456789012`\.

1. In your directory \(for example, your directory in Active Directory\), create the emergency access group and specify a name for the directory \(for example, `aws#EmergencyAccess_Role1_RO#123456789012`\)\. Assign your users to this group by using your existing provisioning mechanism\.

1. In the emergency access account, [configure a custom trust policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-custom.html) that provides the permissions required for the emergency access role to be assumed during a disruption\. Following is an example statement for a custom **trust policy** that is attached to the `EmergencyAccess_Role1_RO` role\. For an illustration, see the emergency account in the diagram under [How to design emergency role, account, and group mapping](#emergency-access-mapping-design)\.

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
         {
            "Effect":"Allow",
            "Principal":{
               "Federated":"arn:aws:iam::123456789012:saml-provider/Okta"
            },
            "Action":[
               "sts:AssumeRoleWithSAML",
               "sts:SetSourceIdentity",
               "sts:TagSession"
            ],
            "Condition":{
               "StringEquals":{
                  "SAML:aud":"https:~/~/signin.aws.amazon.com/saml"
               }
            }
         }
      ]
   }
   ```

1. The following is an example statement for a **permissions policy** that is attached to the `EmergencyAccess_Role1_RO` role\. For an illustration, see the emergency account in the diagram under [How to design emergency role, account, and group mapping](#emergency-access-mapping-design)\.

   ```
   {
       "Version": "2012-10-17",
       "Statement":[
         {
            "Effect":"Allow",
            "Action":"sts:AssumeRole",
            "Resource":[
               "arn:aws:iam::<account 1>:role/EmergencyAccess_RO",
               "arn:aws:iam::<account 2>:role/EmergencyAccess_RO"
            ]
         }
      ]
   }
   ```

1. On the workload accounts, configure a custom trust policy\. Following is an example statement for a **trust policy** that is attached to the `EmergencyAccess_RO` role\. In this example, account `123456789012` is the emergency access account\. For an illustration, see workload account in the diagram under [How to design emergency role, account, and group mapping](#emergency-access-mapping-design)\.

   ```
   {
       "Version": "2012-10-17",
       "Statement":[
         {
            "Effect":"Allow",
            "Principal":{
               "AWS":"arn:aws:iam::123456789012:root"
            },
            "Action":"sts:AssumeRole"
         }
      ]
   }
   ```
**Note**  
Most IdPs enable you to keep an application integration deactivated until required\. We recommend that you keep the direct IAM federation application deactivated in your IdP until required for emergency access\.
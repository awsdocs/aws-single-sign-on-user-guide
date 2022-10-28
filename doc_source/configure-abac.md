# Enable and configure attributes for access control<a name="configure-abac"></a>

To use ABAC in all cases, you must first enable ABAC using the IAM Identity Center console or the IAM Identity Center API\. If you choose to use IAM Identity Center to select attributes, you use the **Attributes for access control** page in the IAM Identity Center console or the IAM Identity Center API\. If you use an external identity provider \(IdP\) as an identity source and choose to send attributes through the SAML assertions, you configure your IdP to pass the attributes\. If a SAML assertion passes any of these attributes, IAM Identity Center will replace the attribute value with the value from the IAM Identity Center identity store\. Only attributes configured in IAM Identity Center will be sent over for making access control decisions when users federate into their accounts\. 

**Note**  
You cannot view attributes configured and sent by an external IdP from the **Attributes for access control** page in the IAM Identity Center console\. If you are passing access control attributes in the SAML assertions from your external IdP, then those attributes are directly sent to the AWS account when users federate in\. The attributes won’t be available in IAM Identity Center for mapping\.

## Enable attributes for access control<a name="enable-abac"></a>

Use the following procedure to enable the attributes for access \(ABAC\) control feature using the IAM Identity Center console\.

**Note**  
 If you have existing permission sets and you plan to enable ABAC in your IAM Identity Center instance, additional security restrictions require you to first have the `iam:UpdateAssumeRolePolicy` policy\. These additional security restrictions are not required if you do not have any permission sets created in your account\.

**To enable Attributes for access control**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**

1. On the **Settings** page, locate the **Attributes for access control** information box, and then choose **Enable**\. Continue to the next procedure to configure it\.

## Select your attributes<a name="configure-abac-attributes"></a>

Use the following procedure to set up attributes for your ABAC configuration\. 

**To select your attributes using the IAM Identity Center console**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**

1. On the **Settings** page, choose the **Attributes for access control** tab, and then choose **Manage attributes**\.

1. On the **Attributes for access control** page, choose **Add attribute** and enter the **Key** and **Value** details\. This is where you will be mapping the attribute coming from your identity source to an attribute that IAM Identity Center passes as a session tag\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/singlesignon/latest/userguide/images/abac_key_value.png)

   **Key** represents the name you are giving to the attribute for use in policies\. This can be any arbitrary name, but you need to specify that exact name in the policies you author for access control\. For example, lets say that you are using Okta \(an external IdP\) as your identity source and need to pass your organization's cost center data along as session tags\. In **Key**, you would enter a similarly matched name like **CostCenter** as your key name\. It's important to note that whichever name you choose here, it must also be named exactly the same in your `aws:PrincipalTag condition key` \(that is, `"ec2:ResourceTag/CostCenter": "${aws:PrincipalTag/CostCenter}"`\)\.

   **Value** represents the content of the attribute coming from your configured identity source\. Here you can enter any value from the appropriate identity source table listed in [Attribute mappings](attributemappingsconcept.md)\. For example, using the context provided in the above mentioned example, you would review the list of supported IdP attributes and determine that the closest match of a supported attribute would be **`${path:enterprise.costCenter}`** and you would then enter it in the **Value** field\. See the screenshot provided above for reference\. Note, that you can’t use external IdP attribute values outside of this list for ABAC unless you use the option of passing attributes through the SAML assertion\.

1. Choose **Save changes**\.

Now that you have configured mapping your access control attributes, you need to complete the ABAC configuration process\. To do this, author your ABAC rules and add them to your permission sets and/or resource\-based policies\. This is required so that you can grant user identities access to AWS resources\. For more information, see [Create permission policies for ABAC in IAM Identity Center](configure-abac-policies.md)\.

## Disable attributes for access control<a name="disable-abac"></a>

Use the following procedure to disable the ABAC feature and delete all of the attribute mappings that have been configured\. 

**To disable Attributes for access control**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**

1. On the **Settings** page, choose the **Attributes for access control** tab, and then choose **Disable**\.

1. In the **Disable attributes for access control** dialog, review the information and when ready enter DELETE, and then choose **Confirm**\.
**Important**  
This step deletes all attributes that have been configured\. Once deleted, any attributes that are received from an identity source and any custom attributes you have previously configured will not be passed\.
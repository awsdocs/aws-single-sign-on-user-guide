# Rotate an AWS SSO Certificate<a name="rotatecert"></a>

Rotating an AWS SSO certificate is a multistep process that involves the following:
+ Generating a new certificate
+ Adding the new certificate to the service provider’s website
+ Setting the new certificate to active
+ Deleting the inactive certificate

Use all of the following procedures in the following order to complete the certificate rotation process for a given application\.

**Step 1: Generate a new certificate\.**

New AWS SSO certificates that you generate can be configured to use the following properties:
+ **Validity period** – Specifies the time allotted \(in months\) before a new AWS SSO certificate expires\.
+ **Key size** – Determines the number of bits that a key must use with its cryptographic algorithm\. You can set this value to either 1024\-bit RSA or 2048\-bit RSA\. For general information about how key sizes work in cryptography, see [Key size](https://en.wikipedia.org/wiki/Key_size)\.
+ **Algorithm** – Specifies the algorithm that AWS SSO uses when signing the SAML assertion/response\. You can set this value to either SHA\-1 or SHA\-256\. AWS recommends using SHA\-256 when possible, unless your service provider requires SHA\-1\. For general information about how cryptography algorithms work, see [Public\-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography)\.

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. In the list of applications, choose the application that you want to generate a new certificate for\.

1. On the application details page, choose the **Configuration** tab\. Under **AWS SSO metadata**, choose **Manage certificate**\.

1. On the **AWS SSO certificate** page, choose **Generate new certificate**\.

1. In the **Generate new AWS SSO certificate** dialog box, specify the appropriate values for **Validity period**, **Algorithm**, and **Key size**\. Then choose **Generate**\.

**Step 2: Update the service provider's website\.**

Use the following procedure to reestablish the trust with the application's service provider\. 

**Important**  
When you upload the new certificate to the service provider, your users might not be able to get authenticated\. To correct this situation, set the new certificate as active as described in the next step\.

1. In the [AWS SSO console](https://console.aws.amazon.com/singlesignon), choose the application that you just generated a new certificate for\.

1. On the application details page, choose **Edit configuration**\.

1. Choose **View instructions**, and then follow the instructions for your specific application service provider’s website to add the newly generated certificate\. 

**Step 3: Set the new certificate to active\.**

An application can have up to two certificates assigned to it\. Whichever certificate is set as active, AWS SSO will use it to sign all SAML assertions\.

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. In the list of applications, choose your application\.

1. On the application details page, choose the **Configuration** tab\. Under **AWS SSO metadata**, choose **Manage certificate**\.

1. On the **AWS SSO certificate** page, select the certificate you want to set to active, choose **Actions**, and then choose **Set as active**\.

1. In the **Set the selected certificate as active** dialog, confirm that you understand that setting a certificate to active may require you to re\-establish the trust, and then choose **Make active**\.

**Step 4: Delete the old certificate\.**

Use the following procedure to complete the certificate rotation process for your application\. You can only delete a certificate that is in an **Inactive** state\.

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Applications**\.

1. In the list of applications, choose your application\.

1. On the application details page, select the **Configuration** tab\. Under **AWS SSO metadata**, choose **Manage certificate**\.

1. On the **AWS SSO certificate** page, select the certificate you want to delete\. Choose **Actions** and then choose **Delete**\.

1. In the **Delete certificate** dialog box, choose **Delete**\.
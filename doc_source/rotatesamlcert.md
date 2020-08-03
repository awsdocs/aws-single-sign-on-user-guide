# Rotate a SAML 2\.0 Certificate<a name="rotatesamlcert"></a>

You may need to import certificates periodically in order to rotate invalid or expired certificates issued by your identity provider\. This helps to prevent authentication disruption or downtime\. All imported certificates are automatically active\. Certificates should only be deleted after ensuring that they are no longer in use with the associated identity provider\.

You should also consider that some IdPs might not support multiple certificates\. In this case, the act of rotating certificates with these IdPs might mean a temporary service disruption for your users\. Service is restored when the trust with that IdP has been successfully reestablished\. Plan this operation carefully during off peak hours if possible\.

**Note**  
As a security best practice, upon any signs of compromise or mishandling of an existing SAML certificate, you should immediately remove and rotate the certificate\.

Rotating an AWS SSO certificate is a multistep process that involves the following:
+ Obtaining a new certificate from the IdP
+ Importing the new certificate into AWS SSO
+ Activating the new certificate in the IdP
+ Deleting the older certificate

Use all of the following procedures to complete the certificate rotation process while avoiding any authentication downtime\.

**Step 1: Obtain a new certificate from the IdP**

Go to the IdP website and download their SAML 2\.0 certificate\. Make sure that the certificate file is downloaded in PEM encoded format\. Most providers allow you to create multiple SAML 2\.0 certificates in the IdP\. It is likely that these will be marked as disabled or inactive\. 

**Step 2: Import the new certificate into AWS SSO**

Use the following procedure to import the new certificate using the AWS SSO console\.

1. In the [AWS SSO console](https://console.aws.amazon.com/singlesignon), choose **Settings**\.

1. On the **Settings** page, under **Identity source**, next to **Authentication**, choose **View details**\.

1. On the **SAML 2\.0 authentication** page, under **Identity provider metadata**, choose **Manage certificates**\.

1. On the **Manage SAML 2\.0 certificates** page, choose **Import Certificate**\.

At this point, AWS SSO will trust all incoming SAML messages signed from both of the certificates that you have imported\.

**Step 3: Activate the new certificate in the IdP**

Go back to the IdP website and mark the new certificate that you created earlier as primary or active\. At this point all SAML messages signed by the IdP should be using the new certificate\.

**Step 4: Delete the old certificate**

Use the following procedure to complete the certificate rotation process for your IdP\. There must always be at least one valid certificate listed, and it cannot be removed\.

**Note**  
Make sure that your identity provider is no longer signing SAML responses with this certificate before deleting it\. 

1. On the **Manage SAML 2\.0 certificates** page, select the certificate that you want to delete\. Choose **Delete**\.

1. In the **Delete SAML 2\.0 certificate** dialog box, type **DELETE** to confirm, and then choose **Delete**\.

1. Return to the IdP’s website and perform the necessary steps to remove the older inactive certificate\.
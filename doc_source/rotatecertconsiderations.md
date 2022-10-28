# Considerations before rotating a certificate<a name="rotatecertconsiderations"></a>

Before you start the process of rotating a certificate in IAM Identity Center, consider the following:
+ The certification rotation process requires that you reestablish the trust between IAM Identity Center and the service provider\. To reestablish the trust, use the procedures provided in [Rotate an IAM Identity Center certificate](rotatecert.md)\.
+ Updating the certificate with the service provider may cause a temporary service disruption for your users until the trust has been successfully reestablished\. Plan this operation carefully during off peak hours if possible\.
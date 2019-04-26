# Considerations Before Rotating a Certificate<a name="rotatecertconsiderations"></a>

Before you start the process of rotating a certificate in AWS SSO, consider the following:
+ The certification rotation process requires that you reestablish the trust between AWS SSO and the service provider\. To reestablish the trust, use the procedures provided in [Rotate an AWS SSO Certificate](rotatecert.md)\.
+ Updating the certificate with the service provider may cause a temporary service disruption for your users until the trust has been successfully reestablished\. Plan this operation carefully during off peak hours if possible\.
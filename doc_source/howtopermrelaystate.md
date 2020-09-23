# Set Relay State<a name="howtopermrelaystate"></a>

During the federation authentication process, the relay state redirects users within the AWS Management Console\. You can specify a relay state URL to redirect links to any service in the AWS Management Console\. For example, the below illustration shows the process for redirecting to the S3 console \(https://s3\.console\.aws\.amazon\.com/s3/home?region=us\-east\-1\#\)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/singlesignon/latest/userguide/images/permission_sets_relay_state.png)

Use the following procedure to modify the relay state URL for a given permission set\.

**To set the relay state**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **AWS accounts**\.

1. Choose the **Permission sets** tab\.

1. Choose the name of the permission set where you want to change the new relay state URL\.

1. On the **Permissions** tab, under the **General** section, choose **Edit**\.

1. Next to **Relay state**, type a URL value for any of the AWS services, and then choose **Continue**\.

1. Select the AWS accounts in the list that you want the new relay state value to apply to, and then choose **Reprovision**\.
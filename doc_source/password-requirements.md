# Password requirements when managing identities in AWS SSO<a name="password-requirements"></a>

When you use AWS SSO as your identity source, users must adhere to the following password requirements to set or change their password:
+ Passwords are case\-sensitive\.
+ Passwords must be between 8 and 64 characters in length\.
+ Passwords must contain at least one character from each of the following four categories:
  + Lowercase letters \(a\-z\)
  + Uppercase letters \(A\-Z\)
  + Numbers \(0\-9\)
  + Non\-alphanumeric characters \(\~\!@\#$%^&\*\_\-\+=`\|\\\(\)\{\}\[\]:;"'<>,\.?/\)
+ The last three passwords cannot be reused\.

**Note**  
These requirements apply only to users created in the AWS SSO identity store\. If you have configured an identity source other than AWS SSO for authentication, such as Active Directory or an external identity provider, the password policies for your users are defined and enforced in those systems, not in AWS SSO\.
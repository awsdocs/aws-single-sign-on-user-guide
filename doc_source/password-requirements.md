# Password requirements when managing identities in IAM Identity Center<a name="password-requirements"></a>

**Note**  
These requirements apply only to users created in the Identity Center directory\. If you have configured an identity source other than IAM Identity Center for authentication, such as Active Directory or an external identity provider, the password policies for your users are defined and enforced in those systems, not in IAM Identity Center\.

When you use IAM Identity Center as your identity source, users must adhere to the following password requirements to set or change their password:
+ Passwords are case\-sensitive\.
+ Passwords must be between 8 and 64 characters in length\.
+ Passwords must contain at least one character from each of the following four categories:
  + Lowercase letters \(a\-z\)
  + Uppercase letters \(A\-Z\)
  + Numbers \(0\-9\)
  + Non\-alphanumeric characters \(\~\!@\#$%^&\*\_\-\+=`\|\\\(\)\{\}\[\]:;"'<>,\.?/\)
+ The last three passwords cannot be reused\.
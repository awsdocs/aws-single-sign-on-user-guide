# Password Requirements for the AWS SSO Identity Store<a name="password-requirements"></a>

When you create an AWS SSO identity store, a default password policy is created and applied to the store\. Users who sign in to the user portal must adhere to the requirements in this policy when they set or change their password\. The default password policy includes the following requirements:
+ Passwords are case\-sensitive
+ Passwords must be between 8 and 64 characters in length
+ Passwords must contain at least one character from each of the following four categories:
  + Lowercase letters \(a\-z\)
  + Uppercase letters \(A\-Z\)
  + Numbers \(0\-9\)
  + Non\-alphanumeric characters \(\~\!@\#$%^&\*\_\-\+=`\|\\\(\)\{\}\[\]:;"'<>,\.?/\)

**Note**  
These requirements apply only to users created in the AWS SSO identity store\. If you have configured an identity source other than AWS SSO for authentication, such as Active Directory or an external identity provider, the password policies for your users are defined and enforced in those systems, not in AWS SSO\.
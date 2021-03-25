# Understanding AWS SSO sign\-in events<a name="understanding-sign-in-events"></a>

AWS CloudTrail logs successful and unsuccessful sign\-in events for all AWS Single Sign\-On identity sources\. Native SSO and Active Directory \(AD Connector and AWS Managed Microsoft AD\) sourced identities will include additional sign\-in events that are captured each time a user is prompted to solve a specific credential challenge or factor, as well as the status of that particular credential verification request\. Only after a user has completed all required credential challenges will the user be signed in, which will result in a `UserAuthentication` event being logged\.

The following table captures each of the AWS SSO sign\-in CloudTrail event names, their purpose, and applicability to different identity sources\.


| Event name | Event purpose | Identity source applicability | 
| --- | --- | --- | 
| CredentialChallenge | Used to notify that AWS SSO has requested the user to solve a specific credential challenge and specifies the CredentialType that was required \(For example, PASSWORD or TOTP\)\. | Native AWS SSO users, AD Connector, and AWS Managed Microsoft AD | 
| CredentialVerification | Used to notify that the user has attempted to solve a specific CredentialChallenge request and specifies whether that credential succeeded or failed\. | Native AWS SSO users, AD Connector, and AWS Managed Microsoft AD | 
| UserAuthentication | Used to notify that all authentication requirements the user was challenged with have been successfully completed and that the user was successfully signed in\. Users failing to successfully complete the required credential challenges will result in no UserAuthentication event being logged\. | All identity sources | 

The following table captures additional useful event data fields contained within specific sign\-in CloudTrail events\.


| Event name | Event purpose | Sign\-in event applicability | Example values | 
| --- | --- | --- | --- | 
| AuthWorkflowID | Used to correlate all events emitted across an entire sign\-in sequence\. For each user sign\-in, multiple events may be emitted by AWS SSO\.  | CredentialChallenge, CredentialVerification, UserAuthentication | "AuthWorkflowID": "9de74b32\-8362\-4a01\-a524\-de21df59fd83" | 
| CredentialType | Used to specify the credential or factor that was challenged\. UserAuthentication events will include all of the CredentialType values that were successfully verified across the user's sign\-in sequence\. | CredentialChallenge, CredentialVerification, UserAuthentication | CredentialType": "PASSWORD" or "CredentialType": "PASSWORD,TOTP" \(possible values include: PASSWORD, TOTP, WEBAUTHN, EXTERNAL\_IDP, RESYNC\_TOTP\) | 
| DeviceEnrollmentRequired | Used to specify that the user was required to register an MFA device during sign\-in, and that the user successfully completed that request\. | UserAuthentication | "DeviceEnrollmentRequired": "true" | 
| LoginTo | Used to specify the redirect location following a successful sign\-in sequence\. | UserAuthentication | "LoginTo": "https://mydirectory\.awsapps\.com/start/\.\.\.\.\." | 

## Example events for AWS SSO sign\-in scenarios<a name="sign-in-events-examples"></a>

The following examples show the expected sequence of CloudTrail events for different sign\-in scenarios\.

**Topics**
+ [Successful sign\-in when authenticating with only a password](#sign-in-events-examples-1)
+ [Successful sign\-in when authenticating with an external identity provider](#sign-in-events-examples-2)
+ [Successful sign\-in when authenticating with a password and a TOTP authenticator app](#sign-in-events-examples-3)
+ [Successful sign\-in when authenticating with a password and forced MFA registration is required](#sign-in-events-examples-4)
+ [Failed sign\-in when authenticating with only a password](#sign-in-events-examples-5)

### Successful sign\-in when authenticating with only a password<a name="sign-in-events-examples-1"></a>

The following sequence of events captures an example of a successful password only sign\-in\.

**CredentialChallenge \(Password\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-07T20:33:58Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialChallenge",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"9de74b32-8362-4a01-a524-de21df59fd83",
      "CredentialType":"PASSWORD"
   },
   "requestID":"5be44ffb-6946-4f47-acaf-1adebd4afead",
   "eventID":"27ea7725-c1fd-4355-bdba-d0e628e0e604",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialChallenge":"Success"
   }
}
```

**Successful CredentialVerification \(Password\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-07T20:34:09Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialVerification",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"9de74b32-8362-4a01-a524-de21df59fd83",
      "CredentialType":"PASSWORD"
   },
   "requestID":"f3cf52ad-fd3d-4889-8c15-f18d1a7c7393",
   "eventID":"c49640f6-0c8a-43d3-a6e0-900e3bb188d4",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialVerification":"Success"
   }
}
```

**Successful UserAuthentication \(Password Only\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-07T20:34:09Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"UserAuthentication",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"9de74b32-8362-4a01-a524-de21df59fd83",
      "LoginTo":"https://d-1234567890.awsapps.com/start/?state=QVlBQmVGMHFiS0wzWlp1SFgrR25BRnFobU5nQUlnQUJBQk5FWVhSaFVHeGhibVZUZEdGMFpWQmhjbUZ0QUFsUVpYSmxaM0pwYm1VQUFRQUhZWGR6TFd0dGN3QkxZWEp1T21GM2N6cHJiWE02ZFhNdFpXRnpkQzB4T2pjNE9ETTJNVFUxTWpnM056cHJaWGt2TjJOa056Um1PR1l0TnpNME5TMDBabUUxTFdFeU5Ea3RZV0kwTVRreE9UTmhOakkxQUxnQkFnRUFlTDJaOW85cm0xUHNKME05RjZtemdJSXczVU81a0trQy8yZktUWHNUbkx4b0FldytIdzFCK1NuM2NVWitsbncxdGdBQUFBQitNSHdHQ1NxR1NJYjNEUUVIQnFCdk1HMENBUUF3YUFZSktvWklodmNOQVFjQk1CNEdDV0NHU0FGbEF3UUJMakFSQkF5TFJxUDNsUUR6b0txUmlKQUNBUkNBTzRhalR4UUM3cUMvUG1ZUHBJWnRLS2ZlQkRHdmVsNXVJS1REdTkvekRNd2JxRFcxcVBTMDRkZUxST2NGYk96K2xzeGdTdUlKZTVYdiswZWdBZ0FBQUFBTUFBQVFBQUFBQUFBQUFBQUFBQUFBQVB5NEdEdUtWYnBzZWRTYTgvL3MrdEQvLy8vL0FBQUFBUUFBQUFBQUFBQUFBQUFBQVFBQUFGTXNzY3Q2V1QrZjg4N3AvbnlXQUNuQzFweGZaVGZvSjNSVWdhREJOKzNjK2F2NEI5WENxRDM2NkxmcTBzaDIrM3RDQ2J0N2VzMmw0Y1lDcXhwRFM3Y1JnRUxxMjQrVGdZSndvZXZkWW83eFV1bG9sVkJkTWFhcVBSenFyb2ZzNGpFR1FjUT0%3D&auth_code=11OawSqh1qmg4ePRn3DGfmBkWhJ5kYC4t6eFTprUDe8A_h_E75G3iwMNuAvLOs73v5vOaP_xA_PYJikGpt9UJ8kX92vRBCZPubpGegAoz__1fHKwL207gI6MVYEQvMKb2xfMf4qCKedRe0i-BshlIc5OBAA6ftz73M6LsfLWDlfOxviO2K3wet946lC30f_iWdilx-zv__4pSHf7mcUIs&wdc_csrf_token=srAzW1jK4GPYYoR452ruZ38DxEsDY9x81q1tVRSnno5pUjISvP7TqziOLiBLBUSxEjOmQk2XoLlcYolXjOMdiaBoVVBL482Q6iShpDgQcm271KWlODotVsoVADe1tixLr694N70foOPUAuIdi6RxxBSteidgAU7SBZDdfAxeJdqTg45kc4XpnCTKlQiIsrdFShisDnocFsj6EQRDTtEggww2MCXuJBByhpCfUIwg14znJwpR4F9wBw76xyTBBQOv&organization=d-9067230c03&region=us-east-1",
      "CredentialType":"PASSWORD"
   },
   "requestID":"f3cf52ad-fd3d-4889-8c15-f18d1a7c7393",
   "eventID":"e959a95a-2b33-478d-906c-4fe303e8a9f1",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "UserAuthentication":"Success"
   }
}
```

### Successful sign\-in when authenticating with an external identity provider<a name="sign-in-events-examples-2"></a>

The following sequence of events captures an example of a successful sign\-in when authenticated through the SAML protocol using an external identity provider\. 

**Successful UserAuthentication \(External Identity Provider\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-07T20:34:09Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"UserAuthentication",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"9de74b32-8362-4a01-a524-de21df59fd83",
      "LoginTo":"https://d-1234567890.awsapps.com/start/?state=QVlBQmVGMHFiS0wzWlp1SFgrR25BRnFobU5nQUlnQUJBQk5FWVhSaFVHeGhibVZUZEdGMFpWQmhjbUZ0QUFsUVpYSmxaM0pwYm1VQUFRQUhZWGR6TFd0dGN3QkxZWEp1T21GM2N6cHJiWE02ZFhNdFpXRnpkQzB4T2pjNE9ETTJNVFUxTWpnM056cHJaWGt2TjJOa056Um1PR1l0TnpNME5TMDBabUUxTFdFeU5Ea3RZV0kwTVRreE9UTmhOakkxQUxnQkFnRUFlTDJaOW85cm0xUHNKME05RjZtemdJSXczVU81a0trQy8yZktUWHNUbkx4b0FldytIdzFCK1NuM2NVWitsbncxdGdBQUFBQitNSHdHQ1NxR1NJYjNEUUVIQnFCdk1HMENBUUF3YUFZSktvWklodmNOQVFjQk1CNEdDV0NHU0FGbEF3UUJMakFSQkF5TFJxUDNsUUR6b0txUmlKQUNBUkNBTzRhalR4UUM3cUMvUG1ZUHBJWnRLS2ZlQkRHdmVsNXVJS1REdTkvekRNd2JxRFcxcVBTMDRkZUxST2NGYk96K2xzeGdTdUlKZTVYdiswZWdBZ0FBQUFBTUFBQVFBQUFBQUFBQUFBQUFBQUFBQVB5NEdEdUtWYnBzZWRTYTgvL3MrdEQvLy8vL0FBQUFBUUFBQUFBQUFBQUFBQUFBQVFBQUFGTXNzY3Q2V1QrZjg4N3AvbnlXQUNuQzFweGZaVGZvSjNSVWdhREJOKzNjK2F2NEI5WENxRDM2NkxmcTBzaDIrM3RDQ2J0N2VzMmw0Y1lDcXhwRFM3Y1JnRUxxMjQrVGdZSndvZXZkWW83eFV1bG9sVkJkTWFhcVBSenFyb2ZzNGpFR1FjUT0%3D&auth_code=11OawSqh1qmg4ePRn3DGfmBkWhJ5kYC4t6eFTprUDe8A_h_E75G3iwMNuAvLOs73v5vOaP_xA_PYJikGpt9UJ8kX92vRBCZPubpGegAoz__1fHKwL207gI6MVYEQvMKb2xfMf4qCKedRe0i-BshlIc5OBAA6ftz73M6LsfLWDlfOxviO2K3wet946lC30f_iWdilx-zv__4pSHf7mcUIs&wdc_csrf_token=srAzW1jK4GPYYoR452ruZ38DxEsDY9x81q1tVRSnno5pUjISvP7TqziOLiBLBUSxEjOmQk2XoLlcYolXjOMdiaBoVVBL482Q6iShpDgQcm271KWlODotVsoVADe1tixLr694N70foOPUAuIdi6RxxBSteidgAU7SBZDdfAxeJdqTg45kc4XpnCTKlQiIsrdFShisDnocFsj6EQRDTtEggww2MCXuJBByhpCfUIwg14znJwpR4F9wBw76xyTBBQOv&organization=d-9067230c03&region=us-east-1",
      "CredentialType":"EXTERNAL_IDP"
   },
   "requestID":"f3cf52ad-fd3d-4889-8c15-f18d1a7c7393",
   "eventID":"e959a95a-2b33-478d-906c-4fe303e8a9f1",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "UserAuthentication":"Success"
   }
}
```

### Successful sign\-in when authenticating with a password and a TOTP authenticator app<a name="sign-in-events-examples-3"></a>

The following sequence of events captures an example where multi\-factor authentication was required during sign\-in and the user successfully signed in using a password and a TOTP authenticator app\.

**CredentialChallenge \(Password\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-08T20:40:13Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialChallenge",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"303486b5-fce1-4d59-ba1d-eb3acb790729",
      "CredentialType":"PASSWORD"
   },
   "requestID":"e454ea66-1027-4d00-9912-09c0589649e1",
   "eventID":"d89cc0b5-a23a-4b88-843a-89329aeaef2e",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialChallenge":"Success"
   }
}
```

**Successful CredentialVerification \(Password\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-08T20:40:20Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialVerification",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"303486b5-fce1-4d59-ba1d-eb3acb790729",
      "CredentialType":"PASSWORD"
   },
   "requestID":"92c4ac90-0d9b-452d-95d5-728487612f5e",
   "eventID":"4533fd49-6669-4d0b-b272-a0b2139309a8",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialVerification":"Success"
   }
}
```

**CredentialChallenge \(TOTP\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-08T20:40:20Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialChallenge",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"303486b5-fce1-4d59-ba1d-eb3acb790729",
      "CredentialType":"TOTP"
   },
   "requestID":"92c4ac90-0d9b-452d-95d5-728487612f5e",
   "eventID":"29202f08-f240-40cc-b789-c0cea8a27847",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialChallenge":"Success"
   }
}
```

**Successful CredentialVerification \(TOTP\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-08T20:40:27Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialVerification",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"303486b5-fce1-4d59-ba1d-eb3acb790729",
      "CredentialType":"TOTP"
   },
   "requestID":"c40a691f-eeb1-4352-b286-5e909f96f318",
   "eventID":"e889ff1d-fcaf-454f-805d-7132cf2362a4",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialVerification":"Success"
   }
}
```

**Successful UserAuthentication \(Password \+ TOTP\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-08T20:40:27Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"UserAuthentication",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"303486b5-fce1-4d59-ba1d-eb3acb790729",
      "LoginTo":"https://d-1234567890.awsapps.com/start/?state\u003dQVlBQmVLeFhWeDRmZFJmMmxHcWYwdzhZck5RQUlnQUJBQk5FWVhSaFVHeGhibVZUZEdGMFpWQmhjbUZ0QUFsUVpYSmxaM0pwYm1VQUFRQUhZWGR6TFd0dGN3QkxZWEp1T21GM2N6cHJiWE02ZFhNdFpXRnpkQzB4T2pjNE9ETTJNVFUxTWpnM056cHJaWGt2TjJOa056Um1PR1l0TnpNME5TMDBabUUxTFdFeU5Ea3RZV0kwTVRreE9UTmhOakkxQUxnQkFnRUFlTDJaOW85cm0xUHNKME05RjZtemdJSXczVU81a0trQy8yZktUWHNUbkx4b0FjT3lLZ2RQUFBTRzN6d2l0WmJOSFVRQUFBQitNSHdHQ1NxR1NJYjNEUUVIQnFCdk1HMENBUUF3YUFZSktvWklodmNOQVFjQk1CNEdDV0NHU0FGbEF3UUJMakFSQkF3aHFPL1ZoaFU4bmJFaEoxZ0NBUkNBTzJYZ0xpem12MlJoM3lnRGJaQ2dUcUZlbk5iWGN2ZWVzUjV6WmpLeXZUVnBwTjk2ZGVUZ3plcURod3hRMmNTR1pkTnBVd1RWWWFxbGp2akRBZ0FBQUFBTUFBQVFBQUFBQUFBQUFBQUFBQUFBQUxhZjZTVnRvMlFKWWt0Q0crWjd6NnIvLy8vL0FBQUFBUUFBQUFBQUFBQUFBQUFBQVFBQUFGUFhUR3dad0NheXAwUlZBQjJOelZsZnJ1aEdEOUNPeDNqMENBakdseU9DSWxFejlnZWRqcUZxUHZnUzIrN1ltZE84R1BvN21FQ0sybnBqdm13enozWEdBdnJFcVNzZ2RVQVBReXFpcS9oWTdFaUxhZHBYclhYZDlKeUkxZGJ4K3k3Wk80WT0%3D\u0026auth_code\u003d11Fir1mCVJ-4Y5UY6RI10UCXvRePCHd6195xvYg1rwo1Pj7B-7UGIGlYUUVe31Nkzd7ihxKn6DMdnFfO01O8qc3RFR8FUd1w8Z91Txh_4i9y47-Sx-pjBXKG_jUcvBk_UILdGytV4o1u97h42B-TA_6uwdmJiw1dcCz_Rv44d_BS0PkulW-5LVJy1oeP1H0FPPMeheyuk5Uy48d5of9-c\u0026wdc_csrf_token\u003dNMlui44guoVnxRd0qu2tYJIdyyFPX6SDRNTspIScfMM0AgFbho1nvvCaxPTghHbgHCRIXdffFtzH0sL1ow419BobnmqBsnJNx17h3kujsGzt9DJFaJCgbZQOF7pSbr1pHVMGg1MOOvniFekN6YmJ2CB1FeKUBbfNAz2bGZYnXrXQe6bTenIh5f0Pu9lhZJZ5KDQVka7afWFqOaQCzLEFwgATcJ44N6YcmmZBJbKHx3gyEDMzkwRuNJrwjoVpkmDH\u0026organization\u003dd-9067230c03\u0026region\u003dus-east-1",
      "CredentialType":"PASSWORD,TOTP"
   },
   "requestID":"c40a691f-eeb1-4352-b286-5e909f96f318",
   "eventID":"7a8c8725-db2f-488d-a43e-788dc6c73a4a",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "UserAuthentication":"Success"
   }
}
```

### Successful sign\-in when authenticating with a password and forced MFA registration is required<a name="sign-in-events-examples-4"></a>

The following sequence of events captures an example of a successful password sign in, but the user was required and successfully completed registering an MFA device before completing their sign\-in\.

**CredentialChallenge \(Password\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-09T01:24:02Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialChallenge",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"76d8a26d-ad9c-41a4-90c3-d607cdd7155c",
      "CredentialType":"PASSWORD"
   },
   "requestID":"321f4b13-42b5-4005-a0f7-826cad26d159",
   "eventID":"8c707b0f-e45a-4a9c-bee2-ff68638d2f1b",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialChallenge":"Success"
   }
}
```

**Successful CredentialVerification \(Password\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-09T01:24:09Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialVerification",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"76d8a26d-ad9c-41a4-90c3-d607cdd7155c",
      "CredentialType":"PASSWORD"
   },
   "requestID":"12b57efa-0a92-4479-91a3-5b6641817c21",
   "eventID":"783b0c89-7142-4942-8b84-6ee0de1b992e",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialVerification":"Success"
   }
}
```

**Successful UserAuthentication \(Password \+ MFA Registration Required\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-09T01:24:14Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"UserAuthentication",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"76d8a26d-ad9c-41a4-90c3-d607cdd7155c",
      "LoginTo":"https://d-1234567890.awsapps.com/start/?state\u003dQVlBQmVGQ3VqdHF5aW9CUDdrNXRTVTJUaWNnQUlnQUJBQk5FWVhSaFVHeGhibVZUZEdGMFpWQmhjbUZ0QUFsUVpYSmxaM0pwYm1VQUFRQUhZWGR6TFd0dGN3QkxZWEp1T21GM2N6cHJiWE02ZFhNdFpXRnpkQzB4T2pjNE9ETTJNVFUxTWpnM056cHJaWGt2TjJOa056Um1PR1l0TnpNME5TMDBabUUxTFdFeU5Ea3RZV0kwTVRreE9UTmhOakkxQUxnQkFnRUFlTDJaOW85cm0xUHNKME05RjZtemdJSXczVU81a0trQy8yZktUWHNUbkx4b0FSOVdDcXQ5bUxQeUJ2dFhJNTNFaGhvQUFBQitNSHdHQ1NxR1NJYjNEUUVIQnFCdk1HMENBUUF3YUFZSktvWklodmNOQVFjQk1CNEdDV0NHU0FGbEF3UUJMakFSQkF6Y0FYakw5TE1mdjh5a3owc0NBUkNBT3p5cTd4TXdzTFh3WnJ4dFNvVUF0MXVEU3J1WVBPWGc0UGFhNTNZQWxqamI2VFVyOGRYNjhpRDVoRCs3VVIrWVZUck1YOThsRGJCMmNHNHpBZ0FBQUFBTUFBQVFBQUFBQUFBQUFBQUFBQUFBQU03N1hhMlp4R1MzRUppT2xSY3ZRUnYvLy8vL0FBQUFBUUFBQUFBQUFBQUFBQUFBQVFBQUFGTVNpc3RSRGR6c0FmZmgwbHhsYks2RjZSNTg1NmdOZTRsaWxsT2x1QmVKZVRSRGtrVkVJRVl0Y0t4eFliRDJoV0JsUG9VbElCb01UYy9XbVNyRE1WU2JzcEl0ZXFMMVdxN2MrT2RRUXZFWEdHRUdkRXFpNHFpdmlmQmJhU2V1bGtmSERBOD0%3D\u0026auth_code\u003d11eZ80S_maUsZ7ABETjeQhyWfvIHYz52rgR28sYAKN1oEk2G07czrwzXvE9HLlN2K9De8LyBEV83SFeDQfrWpkwXfaBc2kNR125q_9JkiAeID3_5NkgvDEastjRV_mpFk0sf__0jRcr8vRm-FJyJqkoGrt_w6rm_MpAn0uyrVq8udY EgU3fhOL3QWvWiquYnDPMyPmmy_qkZgR9rz__BI\u0026wdc_csrf_token\u003dJih9U62o5LQDtYLNqCK8a6xj0gJg5BRWq2tbl75y8vAmwZhAqrgrgbxXat2M646UZGp93krw7WYQdHIgi5OYI9QSckf4aovh0maPetDfTj5twOa6FcUKKzMSMBkhJEwiMKgQ1ncaZTPRhdV8o53cyzTYPtZNp0KgrmxlLyZVscVnECUKogJxllWy67XU7po8K68iFqOCq5IGuAbv6zdblbQpaIR2OjgdHZgCjrPNFTUhaabhpOFtXdQNPDArJna1\u0026organization\u003dd-9067230c03\u0026region\u003dus-east-1",
      "CredentialType":"PASSWORD",
      "DeviceEnrollmentRequired":"true"
   },
   "requestID":"74d24604-a365-4237-8c4a-350795494b92",
   "eventID":"a15bf257-7f37-46c0-b67c-fea5fa6166be",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "UserAuthentication":"Success"
   }
}
```

### Failed sign\-in when authenticating with only a password<a name="sign-in-events-examples-5"></a>

The following sequence of events captures an example of a failed password only sign\-in\. 

**CredentialChallenge \(Password\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-08T18:56:15Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialChallenge",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"adbf67c4-8188-4e2b-8527-fe539e328fa7",
      "CredentialType":"PASSWORD"
   },
   "requestID":"f54848ea-b1aa-402f-bf0d-a54561a2ffcc",
   "eventID":"d96f1d6c-dbd9-4a0b-9a45-6a2b66078c78",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialChallenge":"Success"
   }
}
```

**Failed CredentialVerification \(Password\)**

```
{
   "eventVersion":"1.08",
   "userIdentity":{
      "type":"Unknown",
      "principalId":"111122223333",
      "arn":"",
      "accountId":"111122223333",
      "accessKeyId":"",
      "userName":"user1"
   },
   "eventTime":"2020-12-08T18:56:21Z",
   "eventSource":"signin.amazonaws.com",
   "eventName":"CredentialVerification",
   "awsRegion":"us-east-1",
   "sourceIPAddress":"203.0.113.0",
   "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36",
   "requestParameters":null,
   "responseElements":null,
   "additionalEventData":{
      "AuthWorkflowID":"adbf67c4-8188-4e2b-8527-fe539e328fa7",
      "CredentialType":"PASSWORD"
   },
   "requestID":"04528c82-a678-4a1f-a56d-ea2c6445a72a",
   "eventID":"9160fe06-fc2a-474f-9b78-000ee067a09d",
   "readOnly":false,
   "eventType":"AwsServiceEvent",
   "managementEvent":true,
   "eventCategory":"Management",
   "recipientAccountId":"111122223333",
   "serviceEventDetails":{
      "CredentialVerification":"Failure"
   }
}
```
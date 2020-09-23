# AWS SSO Console and API Authorization<a name="security-authorization"></a>

Existing AWS SSO console APIs support dual authorization\. If you have existing AWS SSO instances that were created prior to October 15th 2020, you can use the following table to determine witch API operations now map to newer API operations that were released after that date\.

SSO Instances created before October 15th 2020 will honor both old and new API actions as long as there is no explicit deny on any one of the actions\. SSO Instances created after October 15th 2020 will use the newer API actions for authorization in the AWS SSO console\. 


****  

| Operation name | API actions used before October 15th, 2020 | API actions used after October 15th, 2020 | 
| --- | --- | --- | 
| AssociateProfile | AssociateProfile | CreateAccountAssignment | 
| AttachManagedPolicy | PutPermissionsPolicy | AttachManagedPolicyToPermissionSet | 
| CreatePermissionSet | CreatePermissionSet | CreatePermissionSet | 
| DeleteApplicationInstanceForAWsAccount | DeleteApplicationInstance \| DeleteTrust | DeleteAccountAssignment | 
| DeleteApplicationProfileForAwsAccount | DeleteProfile | DeleteAccountAssignment | 
| DeletePermissionsPolicy | DeletePermissionsPolicy | DeleteInlinePolicyFromPermissionSet | 
| DeletePermissionSet | DeletePermissionSet | DeletePermissionSet | 
| DescribePermissionsPolicies | DescribePermissionsPolicies | ListManagedPoliciesInPermissionSet | 
| DetachManagedPolicy | DeletePermissionsPolicy | DetachManagedPolicyFromPermissionSet | 
| DisassociateProfile | DisassociateProfile | DeleteAccountAssignment | 
| GetApplicationInstanceForAWSAccount | GetApplicationInstance | ListAccountAssignments | 
| GetAWSAccountProfileStatus | GetProfile | ListPermissionSetsProvisionedToAccount | 
| GetPermissionSet | GetPermissionSet | DescribePermissionSet | 
| GetPermissionsPolicy | GetPermissionsPolicy | GetInlinePolicyForPermissionSet | 
| ListAccountsWithProvisionedPermissionSet | ListApplicationInstances \| GetApplicationInstance | ListAccountsForProvisionedPermissionSet | 
| ListAWSAccountProfiles | ListProfiles \| GetProfile | ListPermissionSetsProvisionedToAccount | 
| ListPermissionSets | ListPermissionSets | ListPermissionSets | 
| ListProfileAssociations | ListProfileAssociations | ListAccountAssignments | 
| ProvisionApplicationInstanceForAWSAccount | GetApplicationInstance \| CreateApplicationInstance | CreateAccountAssignment | 
| ProvisionApplicationProfileForAWSAccountInstance | GetProfile \| CreateProfile \| UpdateProfile | CreateAccountAssignment | 
| ProvisionSAMLProvider | GetTrust \| CreateTrust \| UpdateTrust | CreateAccountAssignment | 
| PutPermissionsPolicy | PutPermissionsPolicy | PutInlinePolicyToPermissionSet | 
| UpdatePermissionSet | UpdatePermissionSet | UpdatePermissionSet | 
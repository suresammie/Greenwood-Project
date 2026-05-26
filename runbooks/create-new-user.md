# Runbook — Create a New User

## Prerequisites
- User Administrator role
- Microsoft Graph PowerShell connected
- Department and manager confirmed before starting

## Steps

### 1. Connect
```powershell
Connect-MgGraph -Scopes "User.ReadWrite.All", "Directory.Read.All"
```

### 2. Create the User
```powershell
$passwordProfile = @{
  Password = "TempPass123!"
  ForceChangePasswordNextSignIn = $true
}

New-MgUser `
  -DisplayName "Firstname Greenwood" `
  -UserPrincipalName "firstname.greenwood@christtech.co.uk" `
  -MailNickname "firstname.greenwood" `
  -JobTitle "Job Title" `
  -Department "Department" `
  -AccountEnabled:$true `
  -PasswordProfile $passwordProfile
```

### 3. Set Manager
```powershell
$userId = (Get-MgUser -Filter "UserPrincipalName eq 'firstname.greenwood@christtech.co.uk'").Id
$managerId = (Get-MgUser -Filter "UserPrincipalName eq 'manager.greenwood@christtech.co.uk'").Id

Set-MgUserManagerByRef -UserId $userId -BodyParameter @{ "@odata.id" = "https://graph.microsoft.com/v1.0/users/$managerId" }
```

### 4. Add to Department Security Group
```powershell
$groupId = (Get-MgGroup -Filter "DisplayName eq 'SG-Finance-Greenwood'").Id
New-MgGroupMember -GroupId $groupId -DirectoryObjectId $userId
```

### 5. Assign Licence
See `assign-licence.md`

### 6. Verify
```powershell
Get-MgUser -UserId $userId | Select-Object DisplayName, UserPrincipalName, JobTitle, Department, AccountEnabled
```

## Notes
- UPN conflicts: apply tie-breaker rules from naming-convention.md before creating
- Inform user of temporary password and require change on first sign-in
- SG-AllStaff-Greenwood dynamic group will include the user within 5–30 minutes automatically
- Exchange mailbox provisioning takes up to 30 minutes after licence assignment

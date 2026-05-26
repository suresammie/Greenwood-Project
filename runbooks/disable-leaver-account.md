# Runbook — Disable Leaver Account

## Prerequisites
- User Administrator role
- Written confirmation from HR that the employee has left
- Line manager notified

## Steps

### 1. Connect
```powershell
Connect-MgGraph -Scopes "User.ReadWrite.All", "Group.ReadWrite.All"
```

### 2. Disable the Account Immediately
```powershell
$userId = (Get-MgUser -Filter "UserPrincipalName eq 'leaver.greenwood@christtech.co.uk'").Id

Update-MgUser -UserId $userId -AccountEnabled:$false
Write-Host "Account disabled"
```

### 3. Revoke All Active Sessions
```powershell
Revoke-MgUserSignInSession -UserId $userId
Write-Host "All sessions revoked"
```

### 4. Reset Password
```powershell
$passwordProfile = @{
  Password = "Rand0mP@ss$(Get-Random)!"
  ForceChangePasswordNextSignIn = $true
}
Update-MgUser -UserId $userId -PasswordProfile $passwordProfile
```

### 5. Remove from All Security Groups
```powershell
$groups = Get-MgUserMemberOf -UserId $userId
foreach ($group in $groups) {
  Remove-MgGroupMemberByRef -GroupId $group.Id -DirectoryObjectId $userId
  Write-Host "Removed from $($group.Id)"
}
```

### 6. Remove Admin Roles (if applicable)
```powershell
$assignments = Get-MgRoleManagementDirectoryRoleAssignment -Filter "principalId eq '$userId'"
foreach ($a in $assignments) {
  Remove-MgRoleManagementDirectoryRoleAssignment -UnifiedRoleAssignmentId $a.Id
  Write-Host "Role removed"
}
```

### 7. Verify
```powershell
Get-MgUser -UserId $userId | Select-Object DisplayName, AccountEnabled, UserPrincipalName
```

## After Disabling
- Notify IT Manager that account has been disabled
- If access to the leaver's mailbox is needed, follow the leaver mailbox access runbook (requires HR and legal approval)
- Retain the account for 30 days before deletion — allows recovery if needed
- Document the leaver in the change record

## Notes
- Do not delete the account immediately — disable first and wait 30 days
- Exchange mailbox is retained while the account exists
- Licence can be removed immediately to free it for a new starter

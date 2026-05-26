# Runbook — Add User to Group

## Prerequisites
- User Administrator or Groups Administrator role
- User account must already exist
- Group must already exist

## Steps

### 1. Connect
```powershell
Connect-MgGraph -Scopes "Group.ReadWrite.All", "User.Read.All"
```

### 2. Get User and Group IDs
```powershell
$userId = (Get-MgUser -Filter "UserPrincipalName eq 'firstname.greenwood@christtech.co.uk'").Id
$groupId = (Get-MgGroup -Filter "DisplayName eq 'SG-Finance-Greenwood'").Id
```

### 3. Add User to Group
```powershell
New-MgGroupMember -GroupId $groupId -DirectoryObjectId $userId
Write-Host "Added user to group successfully"
```

### 4. Verify
```powershell
Get-MgGroupMember -GroupId $groupId | ForEach-Object {
  Get-MgUser -UserId $_.Id | Select-Object DisplayName, UserPrincipalName
}
```

## Notes
- Dynamic groups (SG-AllStaff-Greenwood) cannot have members added manually — membership is automatic
- If the filter returns multiple groups with the same name, use the specific Group ID instead
- Group membership changes take effect immediately for static groups
- Conditional Access policies targeting the group apply to new members within minutes

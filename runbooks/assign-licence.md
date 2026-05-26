# Runbook — Assign a Licence

## Prerequisites
- User Administrator role
- Available licences confirmed before starting

## Steps

### 1. Connect
```powershell
Connect-MgGraph -Scopes "User.ReadWrite.All", "Directory.Read.All"
```

### 2. Find Available Licence SKUs
```powershell
Get-MgSubscribedSku | Select-Object SkuPartNumber, SkuId, ConsumedUnits, @{N="Available";E={$_.PrepaidUnits.Enabled - $_.ConsumedUnits}}
```

### 3. Assign Licence to User
```powershell
$userId = (Get-MgUser -Filter "UserPrincipalName eq 'firstname.greenwood@christtech.co.uk'").Id
$skuId = (Get-MgSubscribedSku | Where-Object { $_.SkuPartNumber -eq "SPB" }).SkuId

Set-MgUserLicense -UserId $userId `
  -AddLicenses @{ SkuId = $skuId } `
  -RemoveLicenses @()
```

### 4. Verify
```powershell
Get-MgUserLicenseDetail -UserId $userId | Select-Object SkuPartNumber, SkuId
```

## Notes
- Exchange mailbox provisioning takes up to **30 minutes** after licence assignment
- Inform the user and helpdesk of this delay — it is the most common source of Day 1 tickets
- Do not raise a support ticket for missing mailbox until 30 minutes have passed
- If no licences are available, escalate to the IT Manager before creating the account

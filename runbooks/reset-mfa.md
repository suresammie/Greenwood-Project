# Runbook — Reset MFA for a User

## Prerequisites
- User Administrator role
- Confirm user identity before resetting — do not reset MFA based on email request alone

## Steps

### Option A — Reset via Entra Admin Centre (GUI)
1. Go to https://entra.microsoft.com
2. Click **Users** → find the user
3. Click **Authentication methods**
4. Click **Require re-register multifactor authentication**
5. Confirm the action
6. User will be prompted to register MFA on next sign-in

### Option B — Reset via PowerShell
```powershell
Connect-MgGraph -Scopes "UserAuthenticationMethod.ReadWrite.All"

$userId = (Get-MgUser -Filter "UserPrincipalName eq 'firstname.greenwood@christtech.co.uk'").Id

# List current authentication methods
Get-MgUserAuthenticationMethod -UserId $userId

# Remove Microsoft Authenticator (replace method ID with actual value)
Remove-MgUserAuthenticationMicrosoftAuthenticatorMethod -UserId $userId -MicrosoftAuthenticatorAuthenticationMethodId "<methodId>"
```

### Verify
```powershell
Get-MgUserAuthenticationMethod -UserId $userId
```

## After Reset
- Inform the user they must re-register MFA on next sign-in
- User will be directed to https://aka.ms/mfasetup
- If the user has an older device, enable SMS as a fallback method and log the exception

## Exception Process — SMS Fallback
1. User reports inability to install Microsoft Authenticator
2. Enable SMS authentication method for the user
3. Log exception in the conditional-access-register.md exception table
4. Set a review date no more than 90 days out

# Troubleshooting Guide — Microsoft Entra ID Identity Foundation

## Issue 1: MFA Registration Failure

**Symptom:** User cannot complete MFA registration on first sign-in.

**Cause A:** User has an older phone that cannot install Microsoft Authenticator.
**Fix:** Enable SMS as a fallback authentication method and log the exception.
```powershell
Connect-MgGraph -Scopes "UserAuthenticationMethod.ReadWrite.All"
# Enable SMS for the user via Entra Admin Centre:
# Users → Authentication methods → Add method → Phone
```

**Cause B:** User did not receive the MFA registration prompt.
**Fix:** Require re-registration via Entra Admin Centre.
1. Go to https://entra.microsoft.com
2. Users → find the user → Authentication methods
3. Click Require re-register multifactor authentication

---

## Issue 2: SSPR Not Working for User

**Symptom:** User cannot reset their password at https://aka.ms/sspr.

**Cause A:** User has not registered authentication methods for SSPR.
**Fix:** Ask user to register at https://aka.ms/mysecurityinfo before attempting a reset.

**Cause B:** User only registered one method but two are required.
**Fix:** User must register a second authentication method at https://aka.ms/mysecurityinfo.

**Cause C:** Admin view shows SSPR enabled but user cannot access it.
**Fix:** Test the SSPR flow yourself as a real end user at https://aka.ms/sspr — the admin view does not always reflect the user experience accurately.

---

## Issue 3: Dynamic Group Not Populating

**Symptom:** New user not appearing in SG-AllStaff-Greenwood after creation.

**Cause:** Dynamic group membership evaluation takes 5–30 minutes.
**Fix:** Wait up to 30 minutes. Verify the rule is active:
```powershell
Get-MgGroup -Filter "DisplayName eq 'SG-AllStaff-Greenwood'" |
  Select-Object DisplayName, MembershipRule, MembershipRuleProcessingState
```
If MembershipRuleProcessingState is not "On", re-enable it:
```powershell
Update-MgGroup -GroupId "<groupId>" -MembershipRuleProcessingState "On"
```

---

## Issue 4: Conditional Access Policy Not Applying to New User

**Symptom:** New user can sign in without MFA despite CA policy being enabled.

**Cause:** User not yet in SG-AllStaff-Greenwood — dynamic group has not evaluated yet.
**Fix:** Wait 5–30 minutes for dynamic group to include the user. Do not assign the policy to individual users as a workaround.

---

## Issue 5: User Not Receiving Exchange Mailbox After Licence Assignment

**Symptom:** User cannot access email on Day 1 after licence assigned.

**Cause:** Exchange mailbox provisioning takes up to 30 minutes after licence assignment.
**Fix:** Wait 30 minutes. Do not raise a support ticket until 30 minutes have passed. This is the most common source of Day 1 helpdesk tickets — document it in the onboarding communication sent to new starters.

---

## Issue 6: Duplicate Group ID Error When Adding Members

**Symptom:** `Cannot convert value to type System.String` when running Get-MgGroupMember.

**Cause:** Filter returned multiple groups with the same display name — PowerShell cannot convert an array to a single string.
**Fix:** Use the specific Group ID instead of filtering by name:
```powershell
$groupId = "paste-exact-group-id-here"
Get-MgGroupMember -GroupId $groupId
```

---

## Issue 7: Admin Role Wrong Scope Assigned

**Symptom:** Admin has more permissions than expected — Global Admin assigned instead of User Admin.

**Fix:** Remove the incorrect role assignment immediately:
```powershell
$userId = (Get-MgUser -Filter "UserPrincipalName eq 'admin@christtech.co.uk'").Id
$assignments = Get-MgRoleManagementDirectoryRoleAssignment -Filter "principalId eq '$userId'"
foreach ($a in $assignments) {
  Remove-MgRoleManagementDirectoryRoleAssignment -UnifiedRoleAssignmentId $a.Id
}
```
Then reassign the correct least-privilege role. Review the audit log for any actions taken under the over-privileged role.

---

## Propagation Time Reference

| Action | Expected Time |
|---|---|
| Dynamic group membership evaluation | 5–30 minutes |
| Conditional Access policy applying to new group member | 5–15 minutes |
| Exchange mailbox after licence assignment | Up to 30 minutes |
| MFA registration prompt on next sign-in | Immediate |
| Admin role assignment taking effect | Near immediate |
| Password reset via SSPR taking effect | Immediate |

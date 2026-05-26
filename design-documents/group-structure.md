# Group Structure Design — Greenwood Accountants

## Overview
Security groups control access to resources and are the target for Conditional Access policies, licence assignments, and role scoping. All groups follow the naming convention defined in `naming-convention.md`.

## Security Groups

| Group Name | Type | Members | Purpose |
|---|---|---|---|
| SG-Finance-Greenwood | Static Security | Sarah Greenwood, Rachel Greenwood | Finance department access control |
| SG-HR-Greenwood | Static Security | James Greenwood, Tom Greenwood | HR department access control |
| SG-IT-Greenwood | Static Security | Michael Greenwood, Lisa Greenwood | IT admin access control |
| SG-Management-Greenwood | Static Security | David Greenwood, Claire Greenwood | Management access control |
| SG-AllStaff-Greenwood | Dynamic Security | All enabled Member accounts | Tenant-wide policy assignment |

## Dynamic Group Rule — SG-AllStaff-Greenwood
```
(user.userType -eq "Member") and (user.accountEnabled -eq true)
```
This rule automatically includes all enabled Member-type accounts. New users are added within 5–30 minutes of account creation.

## Microsoft 365 Groups

| Group Name | Purpose | Auto-Creates |
|---|---|---|
| M365-Finance | Finance team collaboration | Teams channel, SharePoint site, mailbox |
| M365-HR | HR team collaboration | Teams channel, SharePoint site, mailbox |
| M365-All-Company | Organisation-wide communication | Teams channel, SharePoint site, mailbox |

## Design Decisions
- Permissions and policies are assigned to groups, never to individual users
- The dynamic group SG-AllStaff-Greenwood is used for tenant-wide Conditional Access
- Static groups are used for department-specific access control
- Microsoft 365 Groups are separate from security groups — they serve collaboration, not access control

## Key Challenge — Dynamic Group Population Delay
After creating SG-AllStaff-Greenwood, newly created users do not appear as members immediately. Entra ID evaluates dynamic membership rules every 5 to 30 minutes. Any Conditional Access policy targeting this group will not apply to new users until the evaluation cycle completes.

**Mitigation:** Always create and populate dynamic groups before assigning policies. Verify membership using PowerShell before assuming policy coverage is active.

```powershell
Get-MgGroup -Filter "DisplayName eq 'SG-AllStaff-Greenwood'" |
  Select-Object DisplayName, MembershipRule, MembershipRuleProcessingState
```

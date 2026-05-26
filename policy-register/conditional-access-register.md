# Conditional Access Policy Register

| Policy Name | Target Users | Target Apps | Condition | Grant Control | State | Created By | Date |
|---|---|---|---|---|---|---|---|
| CA-MFA-AllUsers | SG-AllStaff-Greenwood | All cloud apps | Any location, any device | Require MFA | Enabled | Member 5 | May 2026 |

## Policy Detail — CA-MFA-AllUsers

| Setting | Value |
|---|---|
| Policy Name | CA-MFA-AllUsers |
| Assignments — Users | SG-AllStaff-Greenwood |
| Assignments — Cloud Apps | All cloud apps |
| Conditions — Locations | Any |
| Conditions — Device Platforms | Any |
| Grant | Require multi-factor authentication |
| Session | None |
| Policy State | Enabled |

## MFA Exception Register

| User | Reason | Fallback Method | Approved By | Date | Review Date |
|---|---|---|---|---|---|
| [Add as needed] | | | | | |

## Notes
- Policy targets SG-AllStaff-Greenwood dynamic group
- New users are automatically included after group evaluation cycle (5–30 minutes)
- Do not assign policy before confirming dynamic group is populated
- SMS fallback exceptions must be logged in the exception register above and reviewed quarterly

# Change Record — Identity Foundation Build

## Change Details

| Field | Detail |
|---|---|
| Change Title | Microsoft 365 Identity Foundation — Greenwood Accountants |
| Change Reference | CR-001 |
| Change Type | Standard |
| Priority | High |
| Raised By | Member 1 |
| Date Raised | May 2026 |
| Date Implemented | May 2026 |
| Implemented By | Project Team (Members 1–10) |
| Environment | Microsoft 365 — Microsoft Entra ID |
| Tenant Domain | christtech.co.uk |

## Business Driver
Greenwood Accountants failed a cyber insurance assessment due to the absence of MFA, unstructured user accounts, and no identity governance. The insurer gave 60 days to implement a secure identity foundation. This change record documents the full implementation.

## Scope of Change

| Item | Description | Owner |
|---|---|---|
| User Accounts | 10 test users across Finance, HR, IT, Sales, Management | Member 2 |
| Security Groups | 4 static groups + 1 dynamic group | Member 3 |
| M365 Groups | Finance, HR, All-Company — auto-creates Teams and SharePoint | Member 4 |
| MFA | Conditional Access policy requiring MFA on all apps | Member 5 |
| SSPR | Self-service password reset with two methods required | Member 6 |
| Password Protection | Custom banned password list with company-specific terms | Member 7 |
| Admin Roles | User Admin, Exchange Admin, Teams Admin — least privilege | Member 8 |
| Documentation | GitHub repository with all design documents and runbooks | Members 9 & 10 |

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Dynamic group not populated before policy assigned | Medium | High | Create groups first, verify population, then assign policies |
| MFA locks out users with older phones | Medium | High | Configure SMS fallback and document exception process |
| Global Admin accidentally assigned | Low | High | Verify role scope before every assignment |
| UPN conflicts from duplicate names | Low | Medium | Apply tie-breaker rules from naming convention before creation |
| Mailbox not available on Day 1 | High | Medium | Document 30-minute delay in onboarding runbook |

## Challenges Encountered

| Challenge | Resolution |
|---|---|
| Dynamic group population delay | Documented 5–30 minute wait — create groups before policies |
| MFA on older phones | SMS configured as fallback with exception process documented |
| Global Admin assigned accidentally | Removed and replaced with User Administrator |
| UPN conflict from duplicate names | Tie-breaker rule added to naming convention |
| Mailbox delay after licence assignment | Documented in onboarding runbook as Day 1 prevention measure |

## Lessons Learned
- Always create dynamic groups before assigning policies
- Least privilege is not theoretical — enforce it from day one
- Naming conventions must cover edge cases before deployment
- Test SSPR as a real end user before enabling for everyone
- Document the licence-to-mailbox delay in the onboarding runbook

## Rollback Plan
- Conditional Access policy can be disabled without affecting user accounts
- Security group membership can be reverted manually
- Admin role assignments can be removed immediately via PowerShell
- User accounts can be disabled if needed — do not delete

## Sign-Off

| Role | Name | Date |
|---|---|---|
| IT Manager | | |
| Project Lead | | |

## Status
✅ Complete — May 2026

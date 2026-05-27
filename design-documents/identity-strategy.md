# Identity Strategy — Greenwood Accountants

## Business Context
Greenwood Accountants is migrating from on-premises Active Directory to Microsoft 365. The firm has 80 staff across two offices. The IT manager had been creating accounts manually with no MFA in place. The firm recently failed a cyber insurance assessment and has been given 60 days to implement a secure identity foundation.

## Objectives
- Provision 10 test user accounts across all departments with correct UPN format
- Build security groups for each department and a dynamic all-staff group
- Create Microsoft 365 Groups for Finance, HR, and All-Company
- Enable MFA for all users via Conditional Access
- Configure Self-Service Password Reset with two authentication methods
- Implement custom banned password list with company-specific terms
- Assign least-privilege admin roles to IT staff only

## Scope
| In Scope | Out of Scope |
|---|---|
| Microsoft Entra ID configuration | On-premises Active Directory |
| 10 test user accounts | Full 80-user migration |
| Security and M365 groups | SharePoint site customisation |
| MFA and SSPR | Intune device management |
| Admin role assignments | Third-party app integrations |

## Admin Role Used
- Exchange Administrator (least privilege — not Global Admin)
- Global Admin used only where strictly required and revoked immediately after

## Key Principles
- Least privilege from day one — no Global Admin for routine tasks
- Dynamic groups created and populated before policies are assigned
- Naming conventions defined and edge cases covered before deployment
- All changes documented in the change record before implementation

## Tenant Details
| Field | Value |
|---|---|
| Tenant Domain | christtech.co.uk |
| Admin Centre | https://entra.microsoft.com |
| UPN Format | firstname.greenwood@christtech.co.uk |
| Licence | Microsoft 365 Business Premium|

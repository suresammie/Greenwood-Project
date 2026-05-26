# Role Assignments Register

## Admin Role Assignments

| User | UPN | Role | Scope | Assigned By | Date |
|---|---|---|---|---|---|
| Michael Greenwood | michael.greenwood@christtech.co.uk | User Administrator | Tenant-wide | Member 8 | May 2026 |
| Lisa Greenwood | lisa.greenwood@christtech.co.uk | Exchange Administrator | Tenant-wide | Member 8 | May 2026 |
| Femi Ugboma | femi.ugbomagreenwood@christtech.co.uk | User Administrator | Tenant-wide | Member 8 | May 2026 |
| Grace Ewere | grace.eweregreenwood@christtech.co.uk | Exchange Administrator | Tenant-wide | Member 8 | May 2026 |
| Michael Greenwood | michael.greenwood@christtech.co.uk | Teams Administrator | Tenant-wide | Member 8 | May 2026 |

## Role Scope Reference

| Role | Permitted Actions | What It Cannot Do |
|---|---|---|
| User Administrator | Create, edit, delete users and groups | Manage Exchange, Teams, billing |
| Exchange Administrator | Manage mailboxes, mail flow, distribution lists | Manage users, Teams, licences |
| Teams Administrator | Manage Teams policies, channels, meetings | Manage users, Exchange, licences |
| Global Administrator | Everything | Nothing — avoid for routine tasks |

## Key Lessons
- Always verify role scope before assigning — Global Administrator was accidentally assigned during early testing
- Global Admin for routine tasks creates an audit log full of over-privileged actions
- Least privilege must be enforced from day one
- Role assignments should be reviewed quarterly and revoked when no longer needed

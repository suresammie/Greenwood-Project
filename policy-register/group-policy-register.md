# Group Policy Register

## Security Groups

| Group Name | Type | Members | Created By | Date |
|---|---|---|---|---|
| SG-Finance-Greenwood | Static Security | Sarah Greenwood, Rachel Greenwood | Member 3 | May 2026 |
| SG-HR-Greenwood | Static Security | James Greenwood, Tom Greenwood | Member 3 | May 2026 |
| SG-IT-Greenwood | Static Security | Michael Greenwood, Lisa Greenwood | Member 3 | May 2026 |
| SG-Management-Greenwood | Static Security | David Greenwood, Claire Greenwood | Member 3 | May 2026 |
| SG-AllStaff-Greenwood | Dynamic Security | All enabled Members (auto) | Member 3 | May 2026 |

## Dynamic Membership Rule
```
(user.userType -eq "Member") and (user.accountEnabled -eq true)
```

## Microsoft 365 Groups

| Group Name | Purpose | Created By | Date |
|---|---|---|---|
| M365-Finance | Finance collaboration — Teams, SharePoint, mailbox | Member 4 | May 2026 |
| M365-HR | HR collaboration — Teams, SharePoint, mailbox | Member 4 | May 2026 |
| M365-All-Company | All-company communication | Member 4 | May 2026 |

## Notes
- Dynamic group population delay: 5–30 minutes after user creation
- Always verify SG-AllStaff-Greenwood membership before assigning Conditional Access policies
- Static group membership must be updated manually when staff join or leave

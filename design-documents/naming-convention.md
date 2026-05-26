# Naming Convention — Greenwood Accountants

## UPN Format
```
firstname.greenwood@christtech.co.uk
```

All test users share the surname Greenwood — matching the company name — for instant recognition in the tenant.

## Test User Accounts

| Display Name | UPN | Department | Job Title |
|---|---|---|---|
| Sarah Greenwood | sarah.greenwood@christtech.co.uk | Finance | Finance Analyst |
| Rachel Greenwood | rachel.greenwood@christtech.co.uk | Finance | Senior Finance Analyst |
| James Greenwood | james.greenwood@christtech.co.uk | HR | HR Manager |
| Tom Greenwood | tom.greenwood@christtech.co.uk | HR | HR Coordinator |
| Michael Greenwood | michael.greenwood@christtech.co.uk | IT | IT Administrator |
| Lisa Greenwood | lisa.greenwood@christtech.co.uk | IT | IT Support Analyst |
| Emma Greenwood | emma.greenwood@christtech.co.uk | Sales | Sales Executive |
| Mark Greenwood | mark.greenwood@christtech.co.uk | Sales | Senior Sales Executive |
| David Greenwood | david.greenwood@christtech.co.uk | Management | Operations Manager |
| Claire Greenwood | claire.greenwood@christtech.co.uk | Management | Managing Director |

## Edge Case Tie-Breaker Rules

| Scenario | Rule | Example |
|---|---|---|
| Duplicate first name | Add middle initial | james.a.greenwood@christtech.co.uk |
| No middle initial available | Add department suffix | james.greenwood.hr@christtech.co.uk |
| Three or more duplicates | Middle initial + department suffix | james.a.greenwood.it@christtech.co.uk |

## Group Naming Convention

| Type | Format | Example |
|---|---|---|
| Security Group | SG-[Department]-[Role] | SG-Finance-Users |
| Dynamic Security Group | SG-All-[Scope] | SG-AllStaff-Greenwood |
| Microsoft 365 Group | M365-[Department] | M365-Finance |

## Display Name Format
- Format: `Firstname Greenwood`
- No department suffix in the display name
- Job titles written in full — no abbreviations

## Lessons Learned
- Naming conventions must cover edge cases before deployment, not after
- Two users with the same name discovered the gap immediately during testing
- The tie-breaker rule must be documented and shared with all members before user creation begins

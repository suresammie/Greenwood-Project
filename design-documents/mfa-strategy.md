# MFA Strategy — Greenwood Accountants

## Overview
Multi-Factor Authentication is enforced for all users via a Conditional Access policy targeting the SG-AllStaff-Greenwood dynamic group. MFA is required on all cloud applications with no exceptions.

## Conditional Access Policy

| Setting | Value |
|---|---|
| Policy Name | CA-MFA-AllUsers |
| Target Users | SG-AllStaff-Greenwood |
| Target Apps | All cloud apps |
| Conditions | Any location, any device |
| Grant Control | Require MFA |
| Policy State | Enabled |

## Authentication Methods

| Method | Status | Notes |
|---|---|---|
| Microsoft Authenticator | Primary | Push notification and TOTP |
| SMS | Fallback | For users unable to install Authenticator |
| Voice call | Available | Last resort fallback |

## Fallback for Older Devices
Users with older phones who cannot install Microsoft Authenticator are permitted to use SMS as a fallback method. This must be documented as an exception and reviewed periodically.

**Exception Process:**
1. User reports inability to install Microsoft Authenticator
2. IT Admin enables SMS as authentication method for that user
3. Exception logged in the policy register
4. Reviewed at next quarterly access review

## MFA Registration
All users must register MFA before the Conditional Access policy is enforced. Registration is triggered on first sign-in after policy activation.

## Key Challenge
Users with older phones could not install Microsoft Authenticator during rollout. SMS was configured as a fallback and the exception process was documented.

## Lessons Learned
- Always communicate MFA rollout to users before enabling the policy
- SMS is a weaker form of MFA than Authenticator — treat it as a temporary fallback, not a permanent solution
- Test MFA registration as a real end user before enabling tenant-wide

# Self-Service Password Reset Design — Greenwood Accountants

## Overview
SSPR allows users to reset their own passwords without contacting the helpdesk. Two authentication methods are required to verify identity before a reset is permitted.

## Configuration

| Setting | Value |
|---|---|
| SSPR Enabled | All users |
| Authentication Methods Required | 2 |
| Available Methods | Mobile app notification, mobile app code, email, mobile phone (SMS) |
| Registration Required | Yes — on next sign-in |
| Registration Expiry | 180 days |
| Notifications | User notified on password reset |
| Admin Notified | Yes — on user password reset |

## Authentication Methods Available to Users

| Method | Type |
|---|---|
| Microsoft Authenticator app notification | Strong |
| Microsoft Authenticator app code | Strong |
| Email (alternate) | Moderate |
| Mobile phone SMS | Moderate |

## User Registration Flow
1. User signs in and is prompted to register for SSPR
2. User registers two authentication methods
3. Registration is valid for 180 days before re-registration is required

## Password Reset Flow (End User)
1. User goes to https://aka.ms/sspr
2. Enters their UPN (firstname.greenwood@christtech.co.uk)
3. Completes two verification challenges
4. Sets a new password
5. Signs in with new password

## Admin vs User Experience
The admin view in Entra ID shows SSPR as configured and enabled. The user experience at https://aka.ms/sspr is entirely different — it must be tested as a real end user before enabling for everyone. The admin view does not reveal registration gaps or method failures.

## Key Lesson
Always test the SSPR flow as a real end user before enabling it for everyone. During testing, one authentication method was unavailable to users despite appearing configured in the admin panel. This would have locked users out of self-service reset entirely.

## Licence Requirement
SSPR requires Microsoft Entra ID P1 or P2, or Microsoft 365 Business Premium.

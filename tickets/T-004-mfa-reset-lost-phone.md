# T-004 - MFA reset after a lost phone

**Status:** ☐
**Priority:** P2
**Request type:** Access request
**Channel:** Phone
**Reported by:** jacobpapadopoulos
**Date opened:** YYYY-MM-DD
**Date resolved:** YYYY-MM-DD
**Time taken:** ~30 minutes

## Scenario

Jacob Papadopoulos lost his phone over the weekend. His Authenticator methods are on that device, so he cannot approve sign-ins. He still knows his password. He has a replacement phone and has been identity-verified by his manager, Aisha Rahman.

## Symptoms

- Sign-in prompts for MFA approval that never arrives
- Authenticator app is on the lost device
- Password is known and correct

## Impact

One user fully blocked from all Microsoft 365 services. P2 - no workaround, but a single user.

## Troubleshooting

1. Confirm the identity verification has happened before touching anything. This is a security control, not a formality.
2. List the registered methods: **Entra admin centre → Users** → select the user → **Authentication methods**. Note each method type and the detail behind it, such as the phone number.
3. Identify the methods to remove - Microsoft Authenticator, phone, and any security keys that were also lost - and remove them from that page.
4. Check the sign-in logs for any attempts from the lost device since it went missing: **Entra admin centre → Monitoring → Sign-in logs** → filter by the user.

## Root cause

The only registered MFA methods were on the lost device. No backup method had been registered, so there was no self-service recovery path.

## Resolution

1. Verified identity with the manager.
2. Removed the Authenticator method and the registered phone number.
3. Reviewed sign-in logs for the preceding 72 hours - nothing suspicious.
4. Had the user register the replacement phone on next sign-in.
5. Required a second method (office phone) so a single lost device cannot block access again.

## Verification

User completed MFA registration and signed in to Outlook successfully.

## Escalation decision

Any sign of suspicious activity in the sign-in logs would have gone immediately to Tier 2 / security, with the account disabled pending investigation.

## Knowledge base

KB-01, KB-04.

## Evidence

- Methods list before and after
- Registration confirmation
- Sign-in log review, redacted

![Authentication methods](../evidence/T-004_mfa-reset_01-methods.png)

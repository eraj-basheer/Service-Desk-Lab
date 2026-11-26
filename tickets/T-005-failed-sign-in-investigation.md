# T-005 - Failed sign-in investigation

**Status:** ☐
**Priority:** P3
**Request type:** Access request
**Channel:** Phone
**Reported by:** olivergrant
**Date opened:** YYYY-MM-DD
**Date resolved:** YYYY-MM-DD
**Time taken:** ~20 minutes

## Scenario

Oliver Grant reports that he was "kicked out" of Outlook three times this morning and had to sign in again each time. He is worried his account has been compromised.

## Symptoms

- Repeated sign-in prompts
- Sessions ending unexpectedly
- No obvious password change by the user

## Impact

One user degraded and concerned. P3, but a suspected compromise is treated as P2 until ruled out.

## Troubleshooting

1. Pull recent sign-ins: **Entra admin centre → Monitoring → Sign-in logs** → filter by the user and set the time range to cover the reported morning. Read the status, client app, IP address and Conditional Access result on each entry.
2. Compare IP addresses to the user's usual location. Look for unfamiliar countries, impossible travel, or unusual clients.
3. Check whether the failures cluster around one app - a stale token in one client looks different from an attacker.
4. Check whether Conditional Access is blocking, and which policy.
5. Ask the user what changed: new device, password manager, re-installed app.

## Root cause

A mobile mail client had a stale refresh token after a password change. Each retry failed, and the repeated failures invalidated the session on the desktop client too.

## Resolution

1. Reviewed 20 sign-ins - all from the user's usual city and devices, no anomalies.
2. Identified the failing client from the client app column in the sign-in log.
3. Revoked sessions and had the user remove and re-add the account on the phone.
4. Re-registered MFA on the replacement device.

## Verification

No failed sign-ins in the following 24 hours, and the user confirmed stable sessions.

## Escalation decision

Any sign-in from an unexpected country, or an `unfamiliar sign-in properties` risk flag, would have gone to security immediately - account disabled, then investigated.

## Knowledge base

No article - but a "why do I keep getting signed out" article would be useful.

## Evidence

- Sign-in log table, IP addresses redacted
- The failing client identified
- The 24-hour follow-up

![Sign-in log](../evidence/T-005_signin-investigation_01-log.png)

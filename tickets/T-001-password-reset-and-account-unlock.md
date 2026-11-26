# T-001 - Password reset and account unlock

**Status:** 
**Priority:** P3
**Request type:** Password Reset
**Channel:** Phone
**Reported by:** priyaraman
**Date opened:** 2026-11-26
**Date resolved:** 2026-11-26
**Time taken:** ~20 minutes

## Scenario

Priya Raman returns from leave and cannot sign in. She tried several times and is now locked out. She still has her phone and can approve MFA, so she is a good candidate for self-service - but she has not registered for it yet.

## Symptoms

- Sign-in fails with "Your account has been locked"
- Password is not accepted
- MFA approval still works

## Impact

One user fully blocked. P3 because a workaround exists - she can reach email on her phone - and no other users are affected.

## Troubleshooting

1. Confirm the account exists and is enabled: **Microsoft 365 admin centre → Users → Active users** → select the user → check the account state, and re-enable sign-in there if it is blocked.
2. Check the failure reason: **Entra admin centre → Monitoring → Sign-in logs** → filter by the user → open the latest failures. This distinguishes a lockout from a wrong password.
3. Open the most recent successful sign-in in the same log and note its time, app and source.
4. Confirm the MFA methods are still registered: **Entra admin centre → Users** → select the user → **Authentication methods**.

## Root cause

Three failed attempts from an old saved password triggered the lockout threshold. The phone mail client was retrying the old credential in the background, extending it.

## Resolution

1. Unlocked the account.
2. Reset the password and required a change at next sign-in.
3. Removed the stale credential from the phone's mail client.
4. Walked the user through self-service registration so the next lockout is self-serviceable.

## Verification

User confirmed sign-in on the phone and the web. No further lockouts in the following 24 hours.

## Escalation decision

Not escalated. A lockout loop that survives a password reset would go to Tier 2 to inspect the client's saved credentials.

## Knowledge base

KB-02, KB-04.

## Evidence

- Sign-in log showing the lockout and the failure reason
- Account state before and after
- User confirmation

![Sign-in log](../evidence/T-001_password-reset_01-signin-log.png)

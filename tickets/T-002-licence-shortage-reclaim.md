# T-002 - Licence shortage: 26th user, reclaim from a leaver

**Status:** ☐
**Priority:** P2
**Request type:** New starter
**Channel:** Portal
**Reported by:** helencartwright
**Date opened:** YYYY-MM-DD
**Date resolved:** YYYY-MM-DD
**Time taken:** ~35 minutes

## Scenario

Ryan Costa starts Monday. Helen Cartwright raised the joiner request, but there are no free Business Premium seats: all 25 are assigned. The account cannot be created with a licence, and the start date is fixed.

## Symptoms

- The new account can be created but has no licence
- The Business Premium licence page shows every purchased seat already assigned
- Adding the user to the licensing group cannot grant a seat

## Impact

A new starter cannot work. P2 - scheduled, and blocking someone's first day, but not affecting existing staff.

## Troubleshooting

1. Confirm the cap in the **Microsoft 365 admin centre → Billing → Licences** → Business Premium: compare purchased, assigned and available seats.
2. Identify who holds a seat and should not: **Entra admin centre → Groups → SG-Licence-BusinessPremium → Members**. Check each member's account state under **Users → Active users**.
3. Cross-check against the leaver list. A leaver whose account was disabled but never removed from the licensing group is the usual cause.

## Root cause

The previous leaver was disabled but not removed from the licensing group, so the seat was never reclaimed. The leaver runbook's licence step had been skipped because the mailbox was converted first and the process was considered finished.

## Resolution

1. Confirmed the leaver's last day had passed and the mailbox handover was complete.
2. Removed the leaver from `SG-Licence-BusinessPremium`.
3. Added Ryan to the group.
4. Confirmed the seat was assigned and Ryan could sign in.

## Verification

The licence page showed all 25 purchased seats assigned, with Ryan now holding the seat reclaimed from the leaver. Ryan confirmed sign-in.

## Escalation decision

Would go to the licence owner in Finance if a reclaim could not be found - buying a seat is a commercial decision, not a service desk one.

## Knowledge base

Updated `runbooks/leaver.md` so licence reclaim cannot be skipped.

## Evidence

- Unlicensed state of the new account
- Assigned/available seat counts before and after
- Leaver still listed as a group member

![Licence counts](../evidence/T-002_licence-shortage_01-consumed-units.png)

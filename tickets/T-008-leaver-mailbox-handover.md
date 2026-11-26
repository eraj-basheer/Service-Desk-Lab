# T-008 - Leaver with mailbox handover, asset return and licence reclaim

**Status:** ☐
**Priority:** P2
**Request type:** Leaver
**Channel:** Portal
**Reported by:** fionamcallister
**Date opened:** YYYY-MM-DD
**Date resolved:** YYYY-MM-DD
**Time taken:** ~45 minutes

## Scenario

Imogen Doyle's last day is Friday. Her manager, Fiona McAllister, needs ongoing access to Imogen's mailbox for an open marketing matter, and the laptop must come back.

## Symptoms

Not applicable - scheduled request.

## Impact

Access must be removed at end of business; the mailbox must remain accessible to the manager. P2.

## Steps

Do this one manually first, in this exact order:

1. Block sign-in and revoke active sessions: **Microsoft 365 admin centre → Users → Active users** → select Imogen → **Block sign-in** and **Revoke sessions**.
2. Convert the mailbox and delegate it: **Exchange admin centre → Recipients → Mailboxes** → select Imogen → **Convert to shared**, then under **Delegation** grant the manager Full Access with automapping.
3. Hide the converted mailbox from the address list in its mailbox properties.
4. Remove the user from `SG-Licence-BusinessPremium`: **Entra admin centre → Groups** → select the licensing group → **Members** → remove Imogen.
5. Mark the asset `Returned` with no assignee in the asset register.

> The mailbox must be converted **before** the licence is removed. Removing the licence first soft-deletes the mailbox.

## Troubleshooting

1. If the mailbox conversion fails, confirm the user still has a licence at that moment.
2. If the licence does not free up, confirm the user was a member of the licensing group before removal.
3. If the manager cannot open the mailbox, check Full Access was granted with automapping.

## Resolution

Record: account disabled, mailbox converted and delegated, licence reclaimed, asset returned, remaining access removed.

## Verification

- [ ] Sign-in as the leaver fails
- [ ] Manager can open the mailbox
- [ ] Assigned licence count dropped by one
- [ ] Asset shows `Returned` with no assignee
- [ ] Leaver absent from the department group

## Escalation decision

A litigation hold or retention requirement would go to the legal team before the mailbox is converted. Do not proceed without their confirmation.

## Knowledge base

`runbooks/leaver.md` updated with the ordering warning.

## Evidence

- Account disabled
- Mailbox delegated
- Licence count
- Asset register row

![Leaver summary](../evidence/T-008_leaver_01-summary.png)

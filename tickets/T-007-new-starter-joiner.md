# T-007 - New starter (joiner)

**Status:** ☐
**Priority:** P2
**Request type:** New starter
**Channel:** Portal
**Reported by:** helencartwright
**Date opened:** YYYY-MM-DD
**Date resolved:** YYYY-MM-DD
**Time taken:** ~40 minutes

## Scenario

Nadia Haddad starts Monday as an Accounts Receivable Officer in Finance. Department, title, office and manager are confirmed. A spare laptop is in the asset register.

## Symptoms

Not applicable - this is a scheduled request.

## Impact

A new starter cannot work if not completed. P2 by default: scheduled, but blocking.

## Pre-checks

- [ ] Start date and manager confirmed
- [ ] Spare laptop recorded in the asset register
- [ ] Licence seat available

## Steps

Follow `runbooks/joiner.md`:

1. Create the account: **Microsoft 365 admin centre → Users → Active users → Add a user**. Enter the confirmed name, username, department, job title, office and manager, set the usage location to Australia, and generate a temporary password.
2. Confirm the dynamic department group resolved: **Entra admin centre → Groups → SG-Dept-Finance → Members**.
3. Add the user to `SG-Licence-BusinessPremium` in the Entra admin centre.
4. Set the manager on the user's Entra profile.
5. Record the spare laptop against the user in the asset register.
6. Add any shared mailbox access needed.
7. Send the welcome email with the temporary password and KB-01.

## Troubleshooting

1. If user creation fails with a licence error, check the usage location - it must be set to Australia before a licence can be assigned.
2. If the department group is empty, check the department string matches the rule exactly.
3. If the licence does not assign, check the group is the licensing group and not just any security group.

## Resolution

Record what was created: UPN, licence, asset tag, mailbox access.

## Verification

- [ ] User signs in at `portal.office.com`
- [ ] MFA registration prompt appears
- [ ] Mailbox reachable
- [ ] Correct group membership resolved
- [ ] Laptop recorded against the user

## Escalation decision

Not escalated. A licence purchase decision would go to Finance.

## Knowledge base

KB-01 sent in the welcome email.

## Evidence

- User in Entra with department and title
- Licence assigned
- Asset record updated
- Welcome email sent

![New user](../evidence/T-007_joiner_01-user.png)

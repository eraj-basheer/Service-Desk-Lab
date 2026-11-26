# Microsoft 365 Service Desk Lab

## What the lab models

Cove Consult is an invented firm with two offices and seven departments. Its tenant contains 25 licensed users, dynamic department groups, group-based licensing, two shared mailboxes, MFA and self-service password reset, three Conditional Access policies, and one Intune-managed Windows 11 endpoint. A Jira service desk carries ten incident and request cases.


## How the lab was carried out

The lab was built in four stages:

1. Identity and licensing - create users, departments, groups and licence assignments.
2. Mail and access - set up shared mailboxes, MFA and self-service password reset, and learn to read sign-in logs and message traces.
3. Endpoints and security - join a Windows 11 VM to Entra, enrol it in Intune, apply a compliance policy, deploy apps and add Conditional Access rules.
4. Service desk - set up Jira with request types, priorities and queues, then raise, resolve and document all ten cases.

See [`LAB-GUIDE.md`](LAB-GUIDE.md) for a brief outline of each stage. 

<br>

## Repository contents

- `README.md`: short project overview and repository map.
- `LAB-GUIDE.md`: brief outline of the build stages.
- `tickets/`: the ten written-up cases and a ticket template.
- `runbooks/`: joiner and leaver procedures.
- `kb/`: five end-user self-service guides.
- `scripts/`: the joiner and leaver automation, retained as evidence of scripting ability.
- `evidence/`: screenshot placeholders referenced by the tickets.

The fictional staff roster and asset register were kept outside the published repository, so no personal data is included.

<br>

## Skills practised

| Area                         | What was practised                                                                                      | Evidence                                            |
| ---------------------------- | ------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| Microsoft 365 administration | Bulk user provisioning, dynamic groups by department attribute, group-based licensing                   | T-002, T-007, `scripts/New-LabUsers.ps1`            |
| Identity and access          | MFA registration and reset, SSPR, sign-in log analysis, break-glass admin planning                      | T-001, T-004, T-005                                 |
| Exchange Online              | Shared mailboxes, Full Access versus Send As, automapping behaviour, message trace                      | T-003, T-006, `kb/03-accessing-a-shared-mailbox.md` |
| Endpoint management          | Entra join, Intune enrolment, compliance policy, remote Microsoft 365 Apps deployment                   | T-009                                               |
| Security                     | Three Conditional Access policies and the device to compliance to access chain                          | T-009                                               |
| Service desk practice        | Request types, impact-based P1-P4 priorities, SLAs, queues, self-service portal                         | All ten tickets                                     |
| Incident writing             | Symptoms, impact, troubleshooting including dead ends, root cause, resolution, verification, escalation | `tickets/`                                          |
| Procedural documentation     | Repeatable joiner and leaver runbooks, five plain-language user guides                                  | `runbooks/`, `kb/`                                  |
| Automation                   | Joiner provisioning and leaver closeout, including licence reclaim and mailbox conversion               | `scripts/`                                          |


## What the ten cases demonstrate

| Case | Skill on show |
|---|---|
| T-001 Password reset and account unlock | Identity verification, log-driven diagnosis, user communication |
| T-002 Licence shortage | Seat capacity, identifying a stale licence holder, reclaiming it safely |
| T-003 Shared mailbox missing in Outlook | Separating a correct permission from client-side propagation |
| T-004 MFA reset after a lost phone | Secure recovery after manager verification, adding a second method |
| T-005 Repeated sign-outs | Reading sign-in logs and ruling out compromise |
| T-006 Missing invoice email | Message trace evidence and inbox-rule diagnosis |
| T-007 New starter | End-to-end onboarding and verification |
| T-008 Leaver with mailbox handover | Operational sequencing: convert the mailbox before reclaiming the licence |
| T-009 Compliance failure blocking access | Intune compliance feeding Conditional Access, then restoring access |
| T-010 Printer offline | Client-side triage of a queue, port and driver |




# Lab Guide

A short outline of the stages used to build the lab. See `README.md` for the skills it demonstrates.

## 1. Identity and licensing

- Create 25 users with department, title, office and usage location.
- Build seven dynamic department groups from the `department` attribute.
- Create one licensing group, add the 25 staff, and assign Business Premium to the group.

## 2. Mail and access

- Create the Accounts Payable and Reception shared mailboxes, then delegate Full Access and Send As.
- Register MFA on a test user, reset it, and enable self-service password reset for all users.
- Work through the joiner and leaver runbooks, converting the mailbox before reclaiming the licence.
- Trace a test email and review sign-in logs for failures.

## 3. Endpoint and security

- Build a Windows 11 VM, set the MDM scope to All, join it to Entra and enrol it in Intune.
- Create a compliance policy covering BitLocker, firewall, antivirus and minimum OS, then confirm the device reports Compliant.
- Deploy Microsoft 365 Apps to all users.
- Create three Conditional Access policies: require MFA, block legacy authentication and require a compliant device, excluding admin accounts.
- Break compliance, confirm access is blocked, then restore the device to Compliant.

## 4. Service desk

- Create a Jira Service Management project with six request types, P1-P4 priorities, SLAs and queues.
- Raise, work and resolve all ten cases, capturing screenshots as evidence.

## 5. Tickets

The `tickets/` folder holds ten written-up cases, each following the same structure from symptoms and impact through troubleshooting, root cause, resolution, verification and escalation.

- T-001 password reset and unlock
- T-002 licence reclaim
- T-003 shared mailbox
- T-004 MFA reset
- T-005 sign-in investigation
- T-006 message trace
- T-007 joiner
- T-008 leaver
- T-009 compliance block
- T-010 printer fault

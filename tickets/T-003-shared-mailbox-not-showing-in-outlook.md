# T-003 - Shared mailbox not showing in Outlook

**Status:** ☐
**Priority:** P3
**Request type:** Access request
**Channel:** Email
**Reported by:** rebeccatan
**Date opened:** YYYY-MM-DD
**Date resolved:** YYYY-MM-DD
**Time taken:** ~25 minutes, including a 30-minute wait

## Scenario

Rebecca Tan was granted access to the Accounts Payable shared mailbox an hour ago. She can see it in Outlook on the web but not in Outlook on her desktop. She can send from the address when she types it manually, which suggests the permission is correct and the client is the problem.

## Symptoms

- Shared mailbox missing from the desktop folder pane
- Visible in Outlook on the web
- Send As appears to work

## Impact

One user degraded - the workaround exists, so P3.

## Troubleshooting

1. Confirm the permission is actually granted: **Exchange admin centre → Recipients → Mailboxes** → open Accounts Payable → **Delegation** → check the Full Access and Send As entries for Rebecca.
2. Check whether automapping is enabled on the permission and whether any explicit deny entry overrides it.
3. Check Outlook's cached mode and whether the client has been fully restarted (not just closed to the tray).
4. Check the account's automapping setting if the client has been configured with a policy.

## Root cause

The permission was correct, but automapping had not propagated to the Outlook profile yet. Automapping is delivered through Active Directory and can take up to 30 minutes, and a full Outlook restart is required afterwards.

## Resolution

1. Confirmed the permission and automapping flag.
2. Told the user to close Outlook completely, wait, and reopen.
3. When it still had not appeared after 30 minutes, added the mailbox manually:
   **File → Account Settings → Change → More Settings → Advanced → Add**.
4. Restarted Outlook.

## Verification

The mailbox appeared in the folder pane and the user could open it. Send As was tested with a message to the user's own address.

## Escalation decision

Not escalated. If the permission were missing or denied, this would go to the Exchange administrator.

## Knowledge base

KB-03.

## Evidence

- Delegation entry in the Exchange admin centre
- The manual Add dialog
- The mailbox visible in the folder pane

![Mailbox permissions](../evidence/T-003_shared-mailbox_01-permissions.png)

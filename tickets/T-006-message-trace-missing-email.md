# T-006 - Message trace for a missing email

**Status:** ☐
**Priority:** P3
**Request type:** Software / email issue
**Channel:** Email
**Reported by:** callumfraser
**Date opened:** YYYY-MM-DD
**Date resolved:** YYYY-MM-DD
**Time taken:** ~15 minutes

## Scenario

Callum Fraser says an invoice email from a supplier never arrived. The supplier insists it was sent yesterday. He needs it for month-end.

## Symptoms

- No message in the inbox, junk folder or deleted items
- Sender claims successful delivery
- Other mail from the same sender arrives normally

## Impact

One user degraded; a business process is delayed. P3.

## Troubleshooting

1. Ask for the sender address and an approximate time - a trace without both is guesswork.
2. Run the trace: **Exchange admin centre → Mail flow → Message trace** → **New trace** → enter the sender address, the recipient address and the date range covering the previous three days → run the trace and open the result.
3. Read the Status and Detail columns:
   - `Delivered` - it reached the mailbox; look at rules, junk and Focused/Other.
   - `FilteredAsSpam` - quarantine or junk.
   - `Failed` - read the detail for the SMTP error.
   - No result at all - the message never reached the tenant; the problem is upstream, at the sender.
4. Check the user's inbox rules and the quarantine.

## Root cause

The message was delivered but an inbox rule moved it to a subfolder, so the user did not see it. The rule had been created months earlier for a different supplier with a similar address.

## Resolution

1. Showed the user the trace proving delivery.
2. Located the message in the rule's destination folder.
3. Deleted the stale rule after confirming it was no longer needed.
4. Moved the message back to the inbox.

## Verification

User confirmed the invoice was found, and confirmed that a new message from the same sender now arrives in the inbox.

## Escalation decision

A `Failed` status with a persistent SMTP error would go to Tier 2 with the trace output. A rejected message due to a blocklist would go to security.

## Knowledge base

No article - too specific to this mailbox. A general "check your inbox rules" article would be worth writing later.

## Evidence

- Trace output with status and detail
- The inbox rule
- The message in the folder

![Message trace](../evidence/T-006_message-trace_01-trace.png)

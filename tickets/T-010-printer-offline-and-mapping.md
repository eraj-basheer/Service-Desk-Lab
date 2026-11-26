# T-010 - Printer offline and mapping a network printer

**Status:** ☐
**Priority:** P3
**Request type:** Hardware fault
**Channel:** Portal
**Reported by:** zoemitchell
**Date opened:** YYYY-MM-DD
**Date resolved:** YYYY-MM-DD
**Time taken:** ~30 minutes

## Scenario

Zoe Mitchell cannot print to the third-floor shared printer. It shows as "Offline" in her printer list. Other staff on the same floor can print. She is the only user affected.

## Symptoms

- Printer shows Offline
- Print jobs stay in the queue
- Other users on the same printer are working

## Impact

One user degraded - a workaround exists (print to the second-floor printer). P3.

## Environment

Windows 11, Outlook and Word, network printer shared from the print server.

## Troubleshooting

1. Confirm whether the printer itself is working for someone else. If nobody can print, the fault is the printer, not the client - stop and check the device.
2. On the affected machine, open **Settings → Bluetooth & devices → Printers & scanners** → select the printer → **Open print queue**. Note the printer status and any stuck jobs.
3. Check the printer's port and driver under **Printer properties → Ports** and **Advanced**. Compare them with a working colleague's machine.
4. Check that the print server is reachable from the machine, for example by opening `\\<print-server>` in File Explorer.
5. Check that the **Print Spooler** service is running in `services.msc`, and whether the driver changed after an update.

## Root cause

The print queue was pointing at an old port left behind by a driver update, so the spooler could not reach the device. The printer itself was healthy - other users were printing through a different port.

## Resolution

1. Confirmed the device was online and reachable.
2. Cleared the stuck jobs.
3. Removed the stale printer entry.
4. Re-added the printer from the print server, which used the current port and driver.
5. Printed a test page.

## Verification

Test page printed, and the user printed a real document successfully.

## Escalation decision

If the print server were the problem, this would go to Tier 2 / infrastructure. If the device were faulty, it would go to the managed print provider.

## Knowledge base

A short "how to clear a stuck print job" article would be worth writing.

## Evidence

- Printer status showing Offline
- The stale port
- The re-added printer
- Test page

![Printer status](../evidence/T-010_printer_01-status.png)

> If the hardware path was simulated with a virtual PDF printer, say so here. Do not claim a physical repair.

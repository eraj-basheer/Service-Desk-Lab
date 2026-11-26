# KB-05 - How to map a printer

**Status:** ☐ Draft
**Audience:** all staff
**Last reviewed:** 2026-11

## What this fixes

You need to print to a shared office printer, or the printer disappeared from your list after a change.

## Before you start

- The name of the printer, or the floor it is on
- Your laptop connected to the office network or VPN

## Steps - add a printer on Windows

1. Open **Settings → Bluetooth & devices → Printers & scanners**.
2. Choose **Add device**.
3. Wait for the list to populate and select the printer, for example `CC-Finance-MFP01`.
4. Choose **Add device**. Windows installs the driver automatically.
5. Print a test page: select the printer → **Printer properties** → **Print Test Page**.

## Steps - find a printer that is not listed

1. Choose **Add device → Add manually**.
2. Select **Add a printer using an IP address or hostname**.
3. Device type: **TCP/IP Device**.
4. Hostname or IP address: ask the service desk for the printer's address.
5. Keep the driver selection automatic and choose **Next**.

## If it prints to the wrong printer

The default printer is the one Windows picks when you press Ctrl+P. To change it:

1. **Settings → Bluetooth & devices → Printers & scanners**.
2. Select the correct printer.
3. Turn on **Set as default printer** (or turn off **Let Windows manage my default printer** first).

## If it still does not work

- **The printer shows Offline:** check it is powered on and on the same network. If it is, the queue may be stuck - the service desk can clear it.
- **Jobs sit in the queue:** cancel the queue, restart the **Print Spooler** service, and try again.
- **The printer is missing after a rebuild:** it will not come back automatically unless it was deployed by policy. Ask the service desk to re-add it.

## Related

- KB-04 - What to do when you are locked out

# T-009 - Intune compliance failure blocked by Conditional Access

**Status:** ☐
**Priority:** P2
**Request type:** Access request
**Channel:** Portal
**Reported by:** samueldlamini
**Date opened:** YYYY-MM-DD
**Date resolved:** YYYY-MM-DD
**Time taken:** ~35 minutes

## Scenario

After a policy change, Samuel Dlamini cannot open Outlook on the web or SharePoint. Sign-in succeeds, then he is blocked with "You can't get there from here" or a device-compliance message. The device shows as not compliant in Intune.

## Symptoms

- Browser access to Microsoft 365 blocked after authentication
- Intune shows the device as **Not compliant**
- Sign-in log shows Conditional Access failure

## Impact

One user fully blocked from cloud services on the affected device. P2.

## Troubleshooting

1. Confirm the device's compliance state: **Intune admin centre → Devices** → select the device → **Compliance** → read the per-setting status to find the failing setting.
2. Confirm which policy blocked the sign-in: **Entra admin centre → Monitoring → Sign-in logs** → filter by the user → open a failed entry → **Conditional Access**, and read the policy name and failure reason.
3. Identify the specific compliance setting that failed - BitLocker, firewall, antivirus, or OS version.
4. Confirm the device has synced recently: **Settings → Accounts → Access work or school** → select the connection → **Info → Sync**. A device that has not checked in reports stale state.

## Root cause

The compliance policy's minimum OS version had been raised above the device's build, so the device was correctly marked non-compliant and Conditional Access correctly blocked access to Office 365. Nothing was broken - the policy was working as designed, against an unexpected device build.

## Resolution

1. Confirmed the block was policy-driven, not a fault.
2. Checked whether the device was eligible for an update. It was.
3. Updated the device to a supported build and synced it.
4. Confirmed the device returned to **Compliant** and access was restored.
5. Recorded the policy change as the trigger, so the same block would be expected and explained next time.

## Verification

Device shows **Compliant**, and the user can open Outlook on the web and SharePoint.

## Escalation decision

If the device could not be updated, it would go to Tier 2 to add a documented exception to the policy - with the manager's approval, not by switching the policy off.

## Knowledge base

No article yet. A "why am I blocked from Microsoft 365 on my device" article would reduce repeat tickets.

## Evidence

- Compliance state and the failing setting
- Sign-in log with the CA policy applied
- The block page
- Restored compliant state

![Compliance state](../evidence/T-009_ca-block_01-compliance.png)

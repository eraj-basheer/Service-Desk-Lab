# Runbook - Leaver

**Trigger:** a signed-off leaver request, raised as the *Leaver* request type in Jira.

**Owner:** service desk.

**Target:** access removed at the end of the last working day; mailbox handed over; laptop returned and re-imaged.

## Pre-checks

- [ ] Last working day and manager confirmed
- [ ] Manager named as the mailbox delegate
- [ ] Asset tag recorded in the asset register
- [ ] Any shared mailboxes they own are delegated

## Steps

### 1. Disable and revoke

```powershell
Connect-MgGraph -Scopes 'User.ReadWrite.All','Group.ReadWrite.All'

$leaver = Get-MgUser -Filter "userPrincipalName eq 'imogendoyle@coveconsult.onmicrosoft.com'"
Update-MgUser -UserId $leaver.Id -AccountEnabled:$false
Revoke-MgUserSignInSession -UserId $leaver.Id
```

Revoking sessions matters: without it, an existing token keeps working for up to an hour.

### 2. Convert the mailbox - before touching the licence

```powershell
Connect-ExchangeOnline
Set-Mailbox -Identity 'imogendoyle@coveconsult.onmicrosoft.com' -Type Shared
Add-MailboxPermission -Identity 'imogendoyle@coveconsult.onmicrosoft.com' `
    -User 'fionamcallister@coveconsult.onmicrosoft.com' `
    -AccessRights FullAccess -InheritanceType All -AutoMapping $true
Set-Mailbox -Identity 'imogendoyle@coveconsult.onmicrosoft.com' `
    -HiddenFromAddressListsEnabled $true
```

> **Order matters.** Removing the licence first soft-deletes the mailbox and the handover is lost. Convert first, reclaim last.

If a litigation hold or retention policy is required, confirm with the manager before converting.

### 3. Reclaim the licence

```powershell
$gid = (Get-MgGroup -Filter "displayName eq 'SG-Licence-BusinessPremium'").Id
Remove-MgGroupMemberByRef -GroupId $gid -DirectoryObjectId $leaver.Id
```

Confirm the seat is free:

```powershell
Get-MgSubscribedSku | Select SkuPartNumber, ConsumedUnits
```

### 4. Recover the asset

In the asset register:

| Column | Value |
|---|---|
| AssignedTo | blank |
| Status | `Returned` |

Then physically:

- [ ] Laptop collected and logged
- [ ] Charger and any peripherals collected
- [ ] Device signed out of the user's account
- [ ] Device wiped before reissue

### 5. Remove remaining access

- [ ] Shared mailboxes they owned: delegate to the manager, then remove the leaver
- [ ] Any distribution lists they administered

### 6. Verify

- [ ] Sign-in attempt as the leaver fails
- [ ] Mailbox is accessible to the manager
- [ ] Consumed licence count dropped by one
- [ ] Asset shows `Returned` with no assignee
- [ ] The leaver is absent from the department group

## Running it by hand first

Do the steps above manually the first time. Once you can explain why the mailbox is converted before the licence is removed, `scripts/Disable-Leaver.ps1` performs steps 1-4 in that same order:

```powershell
.\scripts\Disable-Leaver.ps1 `
    -UserPrincipalName imogendoyle@coveconsult.onmicrosoft.com `
    -ManagerUpn fionamcallister@coveconsult.onmicrosoft.com `
    -AssetTag LT-025
```

## Rollback

A disabled account can be re-enabled within the retention period:

```powershell
Update-MgUser -UserId $leaver.Id -AccountEnabled:$true
Set-Mailbox -Identity '<upn>' -Type Regular
```

A reclaimed licence must be reassigned before the mailbox becomes usable again. If the seat was given to someone else, this is not a quick rollback - raise it with the manager immediately.

## Records to update

| Record | Update |
|---|---|
| Asset register | Status `Returned`, assignee cleared |
| Jira | Leaver ticket resolved |
| `runbooks/joiner.md` | Nothing |

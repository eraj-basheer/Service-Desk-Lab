# Runbook - New starter (joiner)

**Trigger:** a signed-off new starter request, raised as the *New starter* request type in Jira.

**Owner:** service desk.

**Target:** all access working before the start date. P2 by default, because a failed joiner blocks someone's first day.

## Pre-checks

- [ ] Start date, department, job title, office and manager confirmed
- [ ] Manager has approved the request in Jira
- [ ] A spare laptop is recorded in the asset register
- [ ] A Business Premium licence seat is free (`Get-MgSubscribedSku`)

If no seat is free, raise a licence reclaim before proceeding. See T-002.

## Steps

### 1. Create the account

Create the account in the Microsoft 365 admin centre with the confirmed name, username, department, job title, office, manager and usage location, then generate a temporary password. The fictional roster is not published in this repository; `scripts/New-LabUsers.ps1` shows how the same provisioning can be automated when a roster is available.

Create the single user directly:

```powershell
Connect-MgGraph -Scopes 'User.ReadWrite.All','Group.ReadWrite.All'
$passwordProfile = @{ ForceChangePasswordNextSignIn = $true; Password = '<generated>' }

$user = New-MgUser `
    -DisplayName 'Nadia Haddad' `
    -GivenName 'Nadia' -Surname 'Haddad' `
    -UserPrincipalName 'nadiahaddad@coveconsult.onmicrosoft.com' `
    -MailNickname 'nadiahaddad' `
    -Department 'Finance' -JobTitle 'Accounts Receivable Officer' -OfficeLocation 'Sydney CBD' `
    -UsageLocation 'AU' -AccountEnabled `
    -PasswordProfile $passwordProfile
```

### 2. Confirm group membership

Department groups are dynamic - membership follows the `department` attribute, so no manual action is needed. Confirm it resolved:

```powershell
Get-MgGroupMember -GroupId (Get-MgGroup -Filter "displayName eq 'SG-Dept-Finance'").Id -All |
    Select-Object Id
```

### 3. Assign the licence

Add the user to the licensing group:

```powershell
$gid = (Get-MgGroup -Filter "displayName eq 'SG-Licence-BusinessPremium'").Id
New-MgGroupMember -GroupId $gid -DirectoryObjectId $user.Id
```

### 4. Set the manager

```powershell
$manager = Get-MgUser -Filter "userPrincipalName eq 'rebeccatan@coveconsult.onmicrosoft.com'"
Set-MgUserManagerByRef -UserId $user.Id `
    -BodyParameter @{ '@odata.id' = "https://graph.microsoft.com/v1.0/users/$($manager.Id)" }
```

### 5. Assign an asset

In the asset register, set the spare laptop to:

| Column | Value |
|---|---|
| AssignedTo | the user's username |
| Department | their department |
| Status | `In use` |

### 6. Hand over access

- [ ] Add them to any shared mailbox they need (see `kb/03-accessing-a-shared-mailbox.md`)
- [ ] Send the welcome email with the temporary password and MFA registration instructions (KB-01)

### 7. Verify

- [ ] User can sign in at `portal.office.com`
- [ ] MFA registration prompt appears
- [ ] Mailbox has a licence and is reachable
- [ ] Laptop is issued and recorded against the user

## Close the ticket

Record in Jira: account created, licence assigned, asset tag issued, welcome email sent, and the verification results.

## Rollback

If the start is cancelled after provisioning:

1. Follow `runbooks/leaver.md`, with the manager as the mailbox delegate.
2. Set the asset back to `Spare` in the asset register.
3. Note the cancellation in the ticket.

## Records to update

| Record | Update |
|---|---|
| Fictional staff roster | Not published; details held outside the repository |
| Asset register | Assign the laptop |
| `temp-passwords.csv` | Generated automatically, never committed |
| Jira | Joiner ticket resolved |

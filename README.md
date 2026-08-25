# Active Directory User & Access Management Lab

## Executive Summary
This repository documents a hands-on Active Directory lab simulating real-world enterprise IT support tickets. Each ticket scenario was executed and verified using both **Manual GUI Administration** (Active Directory Users and Computers) and **Automated PowerShell Scripting**, with ticket lifecycle tracking managed in Jira Service Management.

* **Full Step-by-Step Walkthrough:** [Download Complete PDF Documentation](./Project%201_%20Active%20Directory%20User%20%26%20Access%20Management%20Lab.pdf)

---

## Technical Stack & Environment
* **Directory Services:** Active Directory Domain Services (AD DS) on Windows Server 2022
* **Cloud Infrastructure:** AWS EC2
* **Scripting & Automation:** PowerShell
* **ITSM / Ticketing:** Jira Service Management

---

## Simulated Ticket Matrix

| Ticket ID | Issue / Request | Primary Method (GUI) | Automation Method (PowerShell) | Status |
| :--- | :--- | :--- | :--- | :--- |
| **AD-001** | Create New User / Add User to Security Group | ADUC Console | `New-ADUser` / `Add-ADGroupMember` | Resolved |
| **AD-002** | Password Reset / Unlock User Account | ADUC Console | `Set-ADAccountPassword` / `Unlock-ADAccount` | Resolved |
| **AD-003** | Remove User from Security Group | ADUC Console | `Remove-ADGroupMember` | Resolved |
| **AD-004** | Disable Former Employee Account | ADUC Console | `Disable-ADAccount` | Resolved |
| **AD-005** | Bulk User Creation via CSV | ADUC Console | PowerShell Script (`Import-Csv`) | Resolved |

---

## Ticket Execution Workflow Example

### Featured Ticket AD-001: Create New User / Add User to Security Group

#### Method 1: Manual GUI Execution
1. **Scenario & Intake:** Reviewed ticket request in Jira Service Management queue for new hire Jon Doe.
2. **Step-by-Step Implementation:** Navigated to the designated Organizational Unit (`Lab-Objects`) in ADUC, provisioned the user account, and assigned security group memberships via object properties.
3. **Verification:** Verified account status and group membership in ADUC.

#### Method 2: PowerShell Automation
1. **Script Development:** Executed `New-ADUser` to create the account programmatically and `Add-ADGroupMember` to assign group permissions.
2. **Execution & Audit:** Verified object creation and membership attributes using `Get-ADUser` and `Get-ADGroupMember`.

#### Resolution Summaries

**Ticket Resolution Summary (GUI Method)**
* **Issue Description:** User account creation and group membership assignment requested for new hire Jon Doe.
* **Actions Taken (GUI):**
  1. Opened ADUC and navigated to the `Lab-Objects` Organizational Unit.
  2. Created a new user object for Jon Doe (`jdoe`) and configured account credentials.
  3. Accessed Jon Doe Properties, navigated to the **Member Of** tab, and added Jon Doe to the `IT-Staff` security group.
* **Resolution:** Jon Doe's Active Directory account was successfully provisioned via GUI and added to the required security group. Ticket closed in Jira.

**Ticket Resolution Summary (PowerShell Method)**
* **Issue Description:** Provision user account and assign security group membership for Jon Doe via command line.
* **Actions Taken (PowerShell):**
  1. Executed `New-ADUser` to create user Jon Doe (`jdoe`) in `OU=Lab-Objects,DC=mydclab,DC=local`.
  2. Verified user account creation using `Get-ADUser -Identity jdoe | Select-Object Name, DistinguishedName`.
  3. Added account to security group using `Add-ADGroupMember -Identity "IT-Staff" -Members "jdoe"`.
  4. Verified membership assignment using `Get-ADGroupMember -Identity "IT-Staff"`.
* **Resolution:** Account provisioned and group assignment verified successfully via PowerShell. Ticket closed in Jira.

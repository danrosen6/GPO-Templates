# Group Policy Objects - DAN.LOCAL Domain

> **Portfolio Project:** Enterprise-grade Group Policy templates developed for Windows Active Directory home lab environment. These GPOs demonstrate security hardening, compliance controls, and administrative management best practices.

This repository contains comprehensive Group Policy Object (GPO) configurations for the DAN.LOCAL domain, showcasing enterprise security baseline implementations, user access controls, and system hardening policies.

## Table of Contents

- [Overview](#overview)
- [GPO Architecture](#gpo-architecture)
- [T-Administrator-Workstation-Policy](#t-administrator-workstation-policy)
- [T-Domain-Security-Baseline](#t-domain-security-baseline)
- [T-Kerberos-Authentication-Policy](#t-kerberos-authentication-policy)
- [T-Server-Hardening-Policy](#t-server-hardening-policy)
- [T-Standard-User-Restrictions](#t-standard-user-restrictions)
- [T-Workstation-Security-Policy](#t-workstation-security-policy)
- [Common Settings](#common-settings)
- [Implementation Notes](#implementation-notes)

## Overview

The DAN.LOCAL domain implements a comprehensive security framework through 6 strategically designed Group Policy Objects. Each GPO serves a specific purpose in the overall security architecture:

- **Security Baselines:** Domain-wide password policies, audit settings, and authentication controls
- **Administrative Controls:** Enhanced security for privileged workstations and server systems  
- **User Restrictions:** Limiting user interface access and preventing unauthorized system modifications
- **System Hardening:** Firewall configuration, device restrictions, and update management

### Key Security Features Implemented
-  **Strong Password Policies** (12+ characters, complexity requirements)
-  **Enhanced Audit Logging** (PowerShell, file system, registry)
-  **User Interface Restrictions** (Control Panel, Command Prompt, Registry Editor)
-  **Windows Firewall Management** with domain profile enforcement
-  **Kerberos Security** with delegation controls
-  **Device Installation Controls** preventing unauthorized removable devices

---

## GPO Architecture

```
DAN.LOCAL Domain Security Framework
├── T-Domain-Security-Baseline (94 revisions)
│   └── Foundation: Password policy, audit logging, user rights
├── T-Administrator-Workstation-Policy (28 revisions)  
│   └── Enhanced security for admin workstations
├── T-Workstation-Security-Policy (29 revisions)
│   └── Standard workstation hardening and controls
├── T-Server-Hardening-Policy (32 revisions)
│   └── Server-specific security configurations
├── T-Standard-User-Restrictions (7 revisions)
│   └── User interface and system access limitations
└── T-Kerberos-Authentication-Policy (26 revisions)
    └── Authentication protocol security enhancements
```

---

## T-Administrator-Workstation-Policy

<details>
<summary><strong> Administrative Workstation Security Template</strong></summary>

**Purpose:** Enhanced security controls for privileged administrator workstations  
**Domain:** dan.local  
**Owner:** DAN\Domain Admins  
**Created:** 6/29/2025 9:27:16 AM  
**Modified:** 6/29/2025 2:01:22 PM  
**Data Collected:** 6/29/2025 2:01:46 PM  
**Status:** Enabled  
**Unique ID:** {A8F9B6EE-714E-42F4-B753-EFC59E09FF92}  
**Revisions:** User: 4 (AD), 4 (SYSVOL) | Computer: 28 (AD), 28 (SYSVOL)  
**Links:** None

### Computer Configuration

<details>
<summary><strong>Security Settings</strong></summary>

#### Kerberos Policy
- **Maximum lifetime for service ticket:** 480 minutes
- **Maximum lifetime for user ticket:** 8 hours  
- **Maximum lifetime for user ticket renewal:** 10 days
- **Maximum tolerance for computer clock synchronization:** 5 minutes

#### Security Options - User Account Control
- **User Account Control: Admin Approval Mode for the Built-in Administrator account:** Enabled
- **User Account Control: Run all administrators in Admin Approval Mode:** Enabled

</details>

<details>
<summary><strong>Administrative Templates</strong></summary>

#### Event Log Service/Security
- **Control Event Log behavior when the log file reaches its maximum size:** Enabled
- **Specify the maximum log file size (KB):** Enabled (51200 KB)

#### Remote Desktop Services/Remote Desktop Session Host/Security
- **Always prompt for password upon connection:** Enabled
- **Require secure RPC communication:** Enabled
- **Set client connection encryption level:** Enabled (High Level)

#### Windows PowerShell
- **Turn on PowerShell Script Block Logging:** Enabled (Invocation logging disabled)
- **Turn on PowerShell Transcription:** Enabled
  - Output directory: C:\PowerShellLogs
  - Include invocation headers: Enabled

</details>

### User Configuration

<details>
<summary><strong>Administrative Templates</strong></summary>

#### System/Ctrl+Alt+Del Options
- **Remove Change Password:** Enabled
- **Remove Lock Computer:** Disabled
- **Remove Logoff:** Disabled

</details>

</details>

---

## T-Domain-Security-Baseline

<details>
<summary><strong> Enterprise Security Foundation</strong></summary>

**Purpose:** Domain-wide security baseline implementing enterprise-grade password policies, audit logging, and access controls  
**Domain:** dan.local  
**Owner:** DAN\Domain Admins  
**Created:** 6/29/2025 7:43:46 AM  
**Modified:** 6/29/2025 10:54:50 AM  
**Data Collected:** 6/29/2025 2:02:43 PM  
**Status:** Enabled  
**Unique ID:** {684FC932-6394-43FF-BD46-6267E0185F0D}  
**Revisions:** User: 0 (AD), 0 (SYSVOL) | Computer: 94 (AD), 94 (SYSVOL)  
**Links:** None

### Computer Configuration

<details>
<summary><strong>Security Settings</strong></summary>

#### Password Policy
- **Enforce password history:** 12 passwords remembered
- **Maximum password age:** 45 days
- **Minimum password age:** 1 day
- **Minimum password length:** 12 characters
- **Password must meet complexity requirements:** Enabled
- **Store passwords using reversible encryption:** Disabled

#### Account Lockout Policy
- **Account lockout duration:** 30 minutes
- **Account lockout threshold:** 5 invalid logon attempts
- **Reset account lockout counter after:** 30 minutes

#### Audit Policy
- **Audit account logon events:** Success, Failure
- **Audit logon events:** Success, Failure
- **Audit object access:** Success, Failure
- **Audit policy change:** Success, Failure
- **Audit privilege use:** Success, Failure
- **Audit system events:** Success, Failure

#### User Rights Assignment
- **Access this computer from the network:** DAN\IT-Administrators, DAN\Domain Admins
- **Allow log on locally:** DAN\Server-Administrators, DAN\IT-Administrators, DAN\Domain Admins, BUILTIN\Administrators
- **Back up files and directories:** DAN\Server-Administrators
- **Log on as a service:** (Empty)
- **Restore files and directories:** DAN\Server-Administrators
- **Shut down the system:** DAN\Server-Administrators, DAN\Domain Admins

#### Security Options

<details>
<summary><strong>Microsoft Network Client</strong></summary>

- **Microsoft network client: Digitally sign communications (always):** Enabled

</details>

<details>
<summary><strong>Microsoft Network Server</strong></summary>

- **Microsoft network server: Digitally sign communications (always):** Enabled

</details>

<details>
<summary><strong>Network Access</strong></summary>

- **Network access: Do not allow anonymous enumeration of SAM accounts:** Enabled

</details>

<details>
<summary><strong>Network Security</strong></summary>

- **Network security: LAN Manager authentication level:** Send NTLMv2 response only. Refuse LM & NTLM

</details>

<details>
<summary><strong>Other</strong></summary>

- **Interactive logon: Machine inactivity limit:** 900 seconds

</details>

#### Advanced Audit Configuration

<details>
<summary><strong>Account Logon</strong></summary>

- **Audit Kerberos Authentication Service:** Success, Failure
- **Audit Kerberos Service Ticket Operations:** Success, Failure

</details>

<details>
<summary><strong>Logon/Logoff</strong></summary>

- **Audit Account Lockout:** Success, Failure

</details>

<details>
<summary><strong>Policy Change</strong></summary>

- **Audit Audit Policy Change:** Success, Failure

</details>

</details>

### User Configuration
*No settings defined*

</details>

---

## T-Kerberos-Authentication-Policy

<details>
<summary><strong> Kerberos Security Enhancement</strong></summary>

**Purpose:** Enhanced Kerberos authentication security with delegation controls  
**Domain:** dan.local  
**Owner:** DAN\Domain Admins  
**Created:** 6/29/2025 11:01:12 AM  
**Modified:** 6/29/2025 11:04:40 AM  
**Data Collected:** 6/29/2025 1:34:54 PM  
**Status:** Enabled  
**Unique ID:** {A1D5366D-82AC-451B-884D-9FFDE3FD5022}  
**Revisions:** User: 0 (AD), 0 (SYSVOL) | Computer: 26 (AD), 26 (SYSVOL)  
**Links:** None

### Computer Configuration

<details>
<summary><strong>Security Settings</strong></summary>

#### Kerberos Policy
- **Maximum lifetime for service ticket:** 480 minutes
- **Maximum lifetime for user ticket:** 8 hours
- **Maximum lifetime for user ticket renewal:** 7 days
- **Maximum tolerance for computer clock synchronization:** 5 minutes

#### Audit Policy
- **Audit account logon events:** Success, Failure
- **Audit logon events:** Success, Failure

#### User Rights Assignment
- **Enable computer and user accounts to be trusted for delegation:** DAN\Domain Admins

</details>

### User Configuration
*No settings defined*

</details>

---

## T-Server-Hardening-Policy

<details>
<summary><strong> Server Security Hardening</strong></summary>

**Purpose:** Server-specific security configurations and access restrictions  
**Domain:** dan.local  
**Owner:** DAN\Domain Admins  
**Created:** 6/29/2025 9:04:00 AM  
**Modified:** 6/29/2025 1:41:30 PM  
**Data Collected:** 6/29/2025 1:42:51 PM  
**Status:** Enabled  
**Unique ID:** {014E3764-02E3-4B47-9C62-859779353161}  
**Revisions:** User: 0 (AD), 0 (SYSVOL) | Computer: 32 (AD), 32 (SYSVOL)  
**Links:** None

### Computer Configuration

<details>
<summary><strong>Security Settings</strong></summary>

#### Kerberos Policy
- **Enforce user logon restrictions:** Enabled
- **Maximum lifetime for service ticket:** 600 minutes
- **Maximum lifetime for user ticket:** 10 hours
- **Maximum lifetime for user ticket renewal:** 10 days
- **Maximum tolerance for computer clock synchronization:** 5 minutes

#### User Rights Assignment
- **Access this computer from the network:** BUILTIN\Administrators, NT AUTHORITY\Authenticated Users
- **Allow log on locally:** BUILTIN\Administrators
- **Allow log on through Terminal Services:** DAN\Server-Administrators, DAN\Domain Admins
- **Deny access to this computer from the network:** NT AUTHORITY\ANONYMOUS LOGON, BUILTIN\Guests
- **Log on as a service:** (Empty)

#### Security Options

<details>
<summary><strong>System Objects</strong></summary>

- **System objects: Strengthen default permissions of internal system objects (e.g. Symbolic Links):** Enabled

</details>

#### System Services
- **Remote Registry:** Disabled

</details>

### User Configuration
*No settings defined*

</details>

---

## T-Standard-User-Restrictions

<details>
<summary><strong> User Interface Access Controls</strong></summary>

**Purpose:** Comprehensive user interface restrictions preventing unauthorized system access  
**Domain:** dan.local  
**Owner:** DAN\Domain Admins  
**Created:** 6/29/2025 8:44:24 AM  
**Modified:** 6/29/2025 8:52:44 AM  
**Data Collected:** 6/29/2025 1:42:46 PM  
**Status:** Enabled  
**Unique ID:** {16A8898D-3250-40A1-A09A-03A736A8C88E}  
**Revisions:** User: 7 (AD), 7 (SYSVOL) | Computer: 0 (AD), 0 (SYSVOL)  
**Links:** None

### Computer Configuration
*No settings defined*

### User Configuration

<details>
<summary><strong>Administrative Templates</strong></summary>

#### Control Panel
- **Prohibit access to Control Panel and PC settings:** Enabled

#### Start Menu and Taskbar
- **Remove Run menu from Start Menu:** Enabled
- **Remove Search link from Start Menu:** Enabled

#### System
- **Prevent access to registry editing tools:** Enabled (Disable regedit from running silently: Yes)
- **Prevent access to the command prompt:** Enabled (Disable script processing: No)

#### Windows PowerShell
- **Turn on PowerShell Script Block Logging:** Enabled (Invocation logging disabled)
- **Turn on Script Execution:** Disabled

</details>

</details>

---

## T-Workstation-Security-Policy

<details>
<summary><strong> Workstation Security & Management</strong></summary>

**Purpose:** Standard workstation security controls including firewall management, device restrictions, and update policies  
**Domain:** dan.local  
**Owner:** DAN\Domain Admins  
**Created:** 6/29/2025 8:13:36 AM  
**Modified:** 6/29/2025 1:50:38 PM  
**Data Collected:** 6/29/2025 1:51:20 PM  
**Status:** Enabled  
**Unique ID:** {B54BF6C8-06B3-4148-8367-BB35D0404ECE}  
**Revisions:** User: 0 (AD), 0 (SYSVOL) | Computer: 29 (AD), 29 (SYSVOL)  
**Links:** None

### Computer Configuration

<details>
<summary><strong>Security Settings</strong></summary>

#### Security Options

<details>
<summary><strong>Interactive Logon</strong></summary>

- **Interactive logon: Do not require CTRL+ALT+DEL:** Disabled

</details>

<details>
<summary><strong>Network Access</strong></summary>

- **Network access: Do not allow anonymous enumeration of SAM accounts:** Enabled

</details>

<details>
<summary><strong>Network Security</strong></summary>

- **Network security: LAN Manager authentication level:** Send NTLMv2 response only

</details>

<details>
<summary><strong>User Account Control</strong></summary>

- **User Account Control: Admin Approval Mode for the Built-in Administrator account:** Enabled
- **User Account Control: Run all administrators in Admin Approval Mode:** Enabled

</details>

<details>
<summary><strong>Other</strong></summary>

- **Interactive logon: Display user information when the session is locked:** Do not display user information

</details>

#### Windows Firewall with Advanced Security

<details>
<summary><strong>Global Settings</strong></summary>

- **Policy version:** Not Configured
- **Disable stateful FTP:** Not Configured
- **Disable stateful PPTP:** Not Configured
- **IPsec exempt:** Not Configured
- **IPsec through NAT:** Not Configured
- **Preshared key encoding:** Not Configured
- **SA idle time:** Not Configured
- **Strong CRL check:** Not Configured

</details>

<details>
<summary><strong>Domain Profile Settings</strong></summary>

- **Firewall state:** On
- **Inbound connections:** Not Configured
- **Outbound connections:** Not Configured
- **Apply local firewall rules:** Not Configured
- **Apply local connection security rules:** Not Configured
- **Display notifications:** Not Configured
- **Allow unicast responses:** Not Configured
- **Log dropped packets:** Not Configured
- **Log successful connections:** Not Configured
- **Log file path:** Not Configured
- **Log file maximum size (KB):** Not Configured

</details>

#### Advanced Audit Configuration

<details>
<summary><strong>Detailed Tracking</strong></summary>

- **Audit Process Creation:** Success, Failure

</details>

<details>
<summary><strong>Object Access</strong></summary>

- **Audit File System:** Success, Failure
- **Audit Registry:** Success, Failure

</details>

</details>

<details>
<summary><strong>Administrative Templates</strong></summary>

#### Windows Defender Firewall/Domain Profile
- **Windows Defender Firewall: Do not allow exceptions:** Disabled
- **Windows Defender Firewall: Protect all network connections:** Enabled

#### Device Installation/Device Installation Restrictions
- **Allow administrators to override Device Installation Restriction policies:** Enabled
- **Prevent installation of removable devices:** Enabled

#### Windows Update
- **Configure Automatic Updates:** Enabled (3 - Auto download and notify for install)
  - Install during automatic maintenance: Disabled
  - Scheduled install day: Every day
  - Scheduled install time: 03:00
  - Every week: Enabled
  - Install updates for other Microsoft products: Disabled
- **Do not display 'Install Updates and Shut Down' option in Shut Down Windows dialog box:** Enabled

</details>

### User Configuration
*No settings defined*

</details>

---

## Common Settings

<details>
<summary><strong>Security Filtering & Delegation Framework</strong></summary>

### Security Filtering
**Scope:** All GPOs apply to **NT AUTHORITY\Authenticated Users**

### Delegation Model
All GPOs implement consistent delegation:
- **DAN\Domain Admins:** Edit settings, delete, modify security
- **DAN\Enterprise Admins:** Edit settings, delete, modify security  
- **NT AUTHORITY\Authenticated Users:** Read (from Security Filtering)
- **NT AUTHORITY\ENTERPRISE DOMAIN CONTROLLERS:** Read
- **NT AUTHORITY\SYSTEM:** Edit settings, delete, modify security

</details>

---

## Implementation Notes

### **Home Lab Architecture**
This GPO framework demonstrates enterprise Active Directory administration in a controlled home lab environment, showcasing:

- **Layered Security Approach:** Multiple GPOs targeting different system roles and user types
- **Revision Control:** Active management with revision tracking (94 revisions on baseline policy)
- **Compliance Focus:** Implementation of security controls aligned with enterprise best practices
- **Operational Security:** PowerShell logging, audit controls, and access restrictions

### **Key Learning Outcomes**
- Group Policy design and implementation
- Windows security baseline configuration  
- User access control and interface restrictions
- Audit logging and compliance monitoring
- Enterprise authentication and authorization models

### **Maintenance Strategy**
- Regular revision updates tracked through AD and SYSVOL
- Comprehensive documentation for change management
- Structured approach to security policy development

---

**Project Status:** Active Development | **Lab Environment:** Windows Server 2019/2022 + Windows 10/11 Clients  
**Technologies:** Active Directory, Group Policy Management, Windows Security, PowerShell  

[↑ Back to top](#group-policy-objects---danlocal-domain)
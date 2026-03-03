# 2060 — Windows Engineering Basics: Technical Knowledge Base


## Global Technical Command Reference

### Windows PowerShell

| Command | Context / Protocol | Functional Description |
|---|---|---|
| `Install-WindowsFeature DHCP -IncludeManagementTools` | PowerShell / Server Roles | Installs the DHCP Server role with management tooling on Windows Server |
| `Get-NetIPConfiguration` | PowerShell / Networking | Displays the current IP address, gateway, and DNS configuration of all network adapters |
| `New-ADUser -Name ... -SamAccountName ... -UserPrincipalName ... -Path ... -AccountPassword ... -Enabled $true` | PowerShell / Active Directory | Creates a new user account object in Active Directory with specified attributes |
| `Import-Csv <path> -Encoding utf8` | PowerShell / Scripting | Imports a CSV file into a PowerShell pipeline for bulk data operations |
| `ConvertTo-SecureString '<password>' -AsPlainText -Force` | PowerShell / Security | Converts a plaintext string into a SecureString object for use with credential parameters |
| `New-Item -Path 'C:\NewFolder' -ItemType Directory` | PowerShell / File System | Creates a new directory at the specified path |
| `Invoke-WebRequest -Uri "http://example.com"` | PowerShell / Networking | Sends an HTTP/HTTPS GET request to a specified URI and returns the response |
| `Get-Help` | PowerShell / General | Displays help documentation for PowerShell cmdlets and modules |
| `Get-Member` | PowerShell / General | Retrieves the properties and methods of .NET objects passed through the pipeline |
| `Get-ChildItem -Path C:\Documents` | PowerShell / File System | Lists the contents of a specified directory (equivalent to `ls` or `dir`) |

### Windows Command Prompt (cmd.exe)

| Command | Context / Protocol | Functional Description |
|---|---|---|
| `cd C:\Windows\System32\drivers\etc\` | CMD / File System | Changes the working directory to the hosts file location |
| `notepad.exe hosts` | CMD / File System | Opens the Windows hosts file in Notepad for manual DNS entry editing |
| `copy` | CMD / File System | Copies one or more files from a source to a destination path |
| `move` | CMD / File System | Moves one or more files from a source to a destination path |
| `ping` | CMD / Networking (ICMP) | Sends ICMP echo request packets to a target host to verify connectivity |

### Windows Run Dialog (Windows + R)

| Command | Context / Protocol | Functional Description |
|---|---|---|
| `appwiz.cpl` | Run Dialog / Control Panel | Opens "Programs and Features" (Add/Remove Programs) directly |
| `lusrmgr.msc` | Run Dialog / User Management | Opens the Local Users and Groups management console |
| `resmon.exe` | Run Dialog / Monitoring | Launches the Resource Monitor tool |
| `regedit` | Run Dialog / Registry | Opens the Windows Registry Editor (requires administrative privileges) |
| `services.msc` | Run Dialog / Services | Opens the Windows Services management interface |
| `eventvwr.msc` | Run Dialog / Event Logging | Opens the Windows Event Viewer |
| `MMC` | Run Dialog / Administration | Opens the Microsoft Management Console (MMC) framework |

### Windows Keyboard Shortcuts

| Shortcut | Context | Functional Description |
|---|---|---|
| `Windows + R` | System-Wide | Opens the Run dialog box |
| `Windows + L` | System-Wide | Locks the current user session |
| `Windows + D` | System-Wide | Toggles display of the desktop |
| `Windows + Shift + S` | System-Wide | Opens the Snipping Tool for a partial screenshot |
| `Windows + E` | System-Wide | Opens File Explorer |
| `Windows + I` | System-Wide | Opens Windows Settings |
| `Ctrl + Shift + Esc` | System-Wide | Opens Task Manager directly |
| `Alt + F4` | Application | Closes the currently active application or window |
| `Ctrl + Z` | Application | Undoes the last action in the active application |
| `Ctrl + Shift + Enter` | Windows Search | Launches the selected application with elevated (Administrator) privileges |
| `F1` | System-Wide | Opens the help window for the active application or context |
| `Alt + Tab` | System-Wide | Switches focus between open application windows |

### Python (Comparison Examples)

| Command / Syntax | Context | Functional Description |
|---|---|---|
| `import os; os.listdir('C:/Documents')` | Python / File System | Lists directory contents using the Python `os` module |
| `os.mkdir('C:/NewFolder')` | Python / File System | Creates a new directory at the specified path |
| `import requests; requests.get("http://example.com")` | Python / Networking | Sends an HTTP GET request to a URI using the `requests` library |

### Network / Protocol References

| Value | Context / Protocol | Functional Description |
|---|---|---|
| Port `445` | SMB / Networking | Default TCP port for Server Message Block (SMB) file-sharing communication |
| Port `389` | LDAP / Networking | Default TCP port for the Lightweight Directory Access Protocol |
| Port `636` | SLDAP / Networking | Default TCP port for Secure LDAP (LDAP over TLS/SSL) |
| Port `3389` | RDP / Networking | Default TCP port for the Remote Desktop Protocol |
| Port `53` | DNS / Networking | Default port for Domain Name System queries |
| Port `67` / `68` | DHCP / Networking | UDP ports used by DHCP server (67) and client (68) |
| `\\localhost\<sharename>` | SMB / File Sharing | UNC path syntax for accessing a local network share |
| `\\<computer name>\<shared folder name>` | SMB / File Sharing | UNC path syntax for accessing a specific share on a remote host |

### File System Paths

| Path | Context | Functional Description |
|---|---|---|
| `C:\Windows\System32` | Windows / System Files | Primary directory for 64-bit system DLLs and Windows core executables |
| `C:\Windows\SysWOW64` | Windows / System Files | Directory for 32-bit system DLLs on a 64-bit Windows installation |
| `C:\Windows\System32\dhcp` | Windows Server / DHCP | Default storage location for DHCP text-based log files |
| `C:\Windows\System32\drivers\etc\hosts` | Windows / DNS | Location of the local hosts file for manual DNS resolution overrides |
| `%appdata%` | Windows / User Data | Environment variable resolving to the current user's `AppData\Roaming` folder |

---

## Module 1: Windows and Windows Server Editions

### Executive Summary

Windows is a desktop-oriented operating system designed for interactive end-user workloads, while Windows Server is engineered for continuous, headless operation as a network services platform. The two product lines share a common kernel lineage but diverge significantly in licensing, feature sets, resource optimization, and supported roles. Understanding their distinctions is foundational to infrastructure planning and workload placement.

### Technical Specifications

**Terminology**

- **Edition:** A licensed product tier within a Windows product line that determines available features, hardware support ceilings, and applicable use cases (e.g., Windows Pro, Windows Server Datacenter).
- **Domain Join:** The process of registering a Windows client or server into an Active Directory domain, enabling centralized identity management and Group Policy enforcement.
- **Volume Licensing:** A procurement model used by organizations to acquire multiple software licenses under a single agreement; required for Windows Enterprise and Education editions.
- **Hyper-V:** Microsoft's native Type-1 hypervisor, integrated into certain Windows and all Windows Server editions, enabling hardware virtualization and virtual machine (VM) hosting.
- **BitLocker:** A full-disk encryption technology available in Windows Pro and above, which protects data at rest by encrypting entire storage volumes using AES.

**Operational Logic**

1. A client purchases or receives a Windows license corresponding to their hardware tier and use case (Home, Pro, Enterprise, Education).
2. Enterprise and Education editions require Volume Licensing agreements or academic licensing, respectively.
3. Windows Server editions are selected based on virtualization density requirements: Standard (2 VMs), Datacenter (unlimited VMs), or Azure Edition (cloud-only).
4. Windows S Mode restricts application installation exclusively to the Microsoft Store, reducing the attack surface on low-cost devices.
5. Feature availability cascades upward: each tier includes all capabilities of lower tiers plus additional enterprise or workload-specific functions.

**Standard Formulas / Syntax**

Feature availability hierarchy (ascending):

```
Windows Home ⊂ Windows Pro ⊂ Windows Enterprise / Education
Windows Pro ⊂ Windows Pro for Workstations
```

Maximum hardware support (Windows Pro for Workstations):

```
Max CPUs: 4
Max RAM:  6 TB
```

### Comparative Analysis

| Feature | Windows (Desktop) | Windows Server | Key Distinction |
|---|---|---|---|
| Primary Use | Desktop productivity, gaming, multimedia | Directory services, file sharing, virtualization, web hosting | Client vs. server workload model |
| GUI | Always present | Optional (can run headless/Core) | Server supports CLI-only deployments |
| Designed Uptime | Hours per day | 24/7 continuous operation | Server is optimized for persistent availability |
| Domain Join | Pro and above | Native capability | Home edition cannot join an AD domain |
| Hyper-V | Pro and above (limited) | All editions (Standard: 2 VMs; Datacenter: unlimited) | Datacenter edition removes the VM density cap |
| Licensing Model | Consumer / OEM / Volume | Volume Licensing / CAL-based | Server requires Client Access Licenses (CALs) for users/devices |

### Practical Implications

**Industrial Application:** An enterprise deploys Windows Server Datacenter in a data center to run dozens of isolated virtual machines, each serving a distinct role (DHCP, DNS, AD DS, IIS), while field staff use Windows Pro laptops joined to the Active Directory domain.

**Technical Constraint:** Windows Home cannot be domain-joined, making it unsuitable for any managed enterprise environment. A common examination misconception is assuming that Group Policy applies to all Windows editions; the Local Group Policy Editor is absent on Windows Home.

---

## Module 2: Windows File System

### Executive Summary

The Windows file system is the architectural layer responsible for organizing, indexing, storing, and retrieving data on physical or virtual storage media. It defines how data is structured into files, directories, and metadata records. Windows has supported multiple file system formats across its history, with NTFS being the current primary standard for internal drives and exFAT dominating removable media.

### Technical Specifications

**Terminology**

- **Master File Table (MFT):** The central metadata catalog of an NTFS volume. Each file or directory entry has a corresponding MFT record containing its name, size, timestamps, permissions, and data cluster locations.
- **Partition:** A logically defined, contiguous segment of a storage device that the operating system treats as an independent storage entity, each with its own file system and drive letter.
- **Volume:** A formatted partition prepared with a specific file system (e.g., NTFS), making it accessible to the OS for read/write operations.
- **Fragmentation:** A condition in which file data is scattered across non-contiguous sectors of a storage device, degrading read performance. Applicable only to HDDs, not SSDs.
- **Metadata:** Descriptive data stored alongside a file, including its size, creation/modification timestamps, access permissions, and physical location on disk.

**Operational Logic**

1. A user creates or saves data; the OS delegates storage management to the file system driver.
2. The file system (e.g., NTFS) determines available disk clusters by consulting the Bitmap structure.
3. Data is broken into blocks and written to available sectors; the MFT record is updated with location pointers.
4. When the file is retrieved, the OS queries the MFT for cluster locations, and the storage controller reads the data back in sequence.
5. Over time, as files are written and deleted, free space becomes non-contiguous (fragmentation); a defragmentation utility can consolidate these sectors. This process is irrelevant on SSDs due to their uniform access latency.

**Standard Formulas / Syntax**

NTFS internal components:

```
MFT        → Catalog of all files and directories on the volume
Bitmap      → Map of used vs. free cluster allocation
MFT Mirror  → Redundant copy of the first MFT records for recovery
```

Storage unit hierarchy:

```
Bit → Byte (8 bits) → Kilobyte (1024 bytes) → Megabyte → Gigabyte → Terabyte
```

### Comparative Analysis

| Feature | FAT32 | NTFS | exFAT | ReFS |
|---|---|---|---|---|
| Max File Size | 4 GB | 16 EB (theoretical) | 16 EB | 16 EB |
| Permissions | None | Per-file and per-folder | None | Per-file and per-folder |
| Encryption | None | EFS (Encrypting File System) | None | Supported (with Integrity Streams) |
| Cross-Platform | High (macOS, Linux, USB) | Windows-only (native) | High (flash drives) | Windows/Server only |
| Corruption Tolerance | Low | Moderate (journaling) | Low | High (Copy-on-Write) |
| Primary Use | Removable media | Internal system drives | High-capacity flash drives | Resilient server storage |

### Practical Implications

**Industrial Application:** An enterprise uses NTFS on all internal workstation and server drives to enforce per-user file permissions, enable BitLocker encryption, and maintain audit logs. USB drives distributed to field staff are formatted as exFAT to ensure compatibility across Windows and macOS without compromising file size limits.

**Technical Constraint:** NTFS is not natively read/write compatible with macOS or Linux without third-party drivers. A common misconception is that deleting files from a partition and reinstalling Windows constitutes a complete re-initialization; formatting the volume is required to establish a clean file system state.

---

## Module 3: Windows Program Execution and Management

### Executive Summary

Windows supports multiple software delivery and execution models, including traditional installer-based applications, portable executables, and Store-distributed packages. Program installation is not merely the act of copying files; it involves registering entries in the Windows Registry, placing DLLs in shared locations, and creating service entries. Proper uninstallation must reverse all of these operations.

### Technical Specifications

**Terminology**

- **EXE (Executable):** A binary format capable of executing arbitrary code; used for both application launchers and software installers. EXE files have limited standardization and can carry malicious payloads.
- **MSI (Microsoft Installer):** A standardized package format specifically designed for software installation, providing a controlled, auditable, and transactional install process suitable for enterprise deployment.
- **User Account Control (UAC):** A Windows security mechanism that requires explicit user consent or administrative credential input before granting elevated privileges to a process.
- **Portable Application:** A self-contained executable that requires no installation, does not modify the host system's registry, and can run from removable storage media.
- **Process:** A running instance of an executable in memory, with its own dedicated address space, system resources, and execution thread context.

**Operational Logic**

1. Verify hardware and OS requirements before initiating installation.
2. Obtain the installer (EXE or MSI) from a trusted source; prefer MSI in managed environments.
3. Execute the installer; UAC prompts for consent if administrative privileges are required.
4. The setup wizard presents configuration options: installation path (default: `C:\Program Files` or `C:\Program Files (x86)` for 32-bit), shortcuts, and license acceptance.
5. The installer writes application files, creates Registry entries, registers DLLs, and may install services or scheduled tasks.
6. To uninstall, use "Programs and Features" (`appwiz.cpl`) or the application's own uninstaller; never delete program directories manually, as this leaves orphaned Registry entries and shared libraries.

**Standard Formulas / Syntax**

Default installation paths:

```
64-bit applications: C:\Program Files\<AppName>
32-bit applications: C:\Program Files (x86)\<AppName>
```

Access Programs and Features via Run dialog:

```
Windows + R → appwiz.cpl
```

### Comparative Analysis

| Feature | EXE Installer | MSI Installer | Portable Application |
|---|---|---|---|
| Standardization | Low | High (Windows Installer standard) | N/A (no install) |
| Registry Impact | Variable | Fully managed and tracked | None |
| Uninstall Reliability | Variable | Reliable, transactional rollback | N/A |
| Enterprise Suitability | Limited | High (GPO deployment capable) | Moderate |
| Security Risk | Higher (can execute arbitrary code) | Lower (structured package) | Variable (depends on source) |
| Offline Portability | No | No | Yes |

### Practical Implications

**Industrial Application:** Enterprise IT departments deploy software using MSI packages distributed via Group Policy or a Mobile Device Management (MDM) platform, ensuring silent, consistent installation across hundreds of endpoints without user interaction.

**Technical Constraint:** Deleting the directory of an installed application does not constitute uninstallation. Residual Registry entries, Start Menu shortcuts, and shared DLL registrations remain, potentially causing conflicts during future reinstallation attempts. This is a common source of examination errors.

---

## Module 4: Windows Program Monitoring

### Executive Summary

Windows provides multiple tiers of process and resource monitoring tools, ranging from the user-accessible Task Manager to the advanced Sysinternals Suite. Effective monitoring enables administrators to identify resource bottlenecks, terminate unresponsive processes, and audit running services. The choice of tool is governed by the depth of diagnostic granularity required.

### Technical Specifications

**Terminology**

- **PID (Process Identifier):** A unique numerical value assigned by the OS to each running process, used to track and manage processes at the kernel level.
- **CPU Bottleneck:** A condition in which the processor is the limiting factor on system performance, typically indicated by sustained CPU utilization near 100%.
- **Working Set:** The subset of virtual memory pages currently resident in physical RAM for a given process; high working set values indicate memory pressure.
- **Service:** A special category of Windows process that runs in the background without a user interface, starts automatically or on demand, and provides system-level functionality.
- **I/O (Input/Output) Operations:** Read and write transactions between a process and storage devices; high disk I/O can indicate disk-bound performance issues.

**Operational Logic**

1. Open Task Manager (`Ctrl + Shift + Esc`) for a high-level overview of running processes, CPU, memory, disk, and network utilization.
2. Use the Processes tab to identify resource-intensive applications; the Details tab provides PID and extended metrics.
3. For deeper diagnosis, open Resource Monitor (`resmon.exe`) to correlate specific processes with their CPU, memory, disk, and network consumption in real time.
4. To diagnose a suspected bottleneck, filter by the target process in Resource Monitor's Image column and observe the colored overlay on the utilization graph.
5. If the issue involves advanced internals (e.g., open handles, registry access, file system activity), use the Sysinternals Suite (Process Monitor, Process Explorer, Autoruns).

**Standard Formulas / Syntax**

Open Resource Monitor via Run dialog:

```
Windows + R → resmon.exe
```

Event IDs for RDP remote access audit (in Security log):

```
Event ID 4624  → Successful logon
Event ID 4672  → Special privileges assigned to new logon
Logon Type 10  → Remote Interactive (RDP)
```

### Comparative Analysis

| Feature | Task Manager | Resource Monitor | Sysinternals (Process Monitor) |
|---|---|---|---|
| Target Audience | General users, administrators | Intermediate / Advanced administrators | Expert administrators, security analysts |
| Granularity | Process-level overview | Per-process resource correlation | File, registry, and network activity trace |
| Real-Time Monitoring | Yes | Yes | Yes |
| Startup Management | Yes (Startup tab) | No | Yes (Autoruns) |
| Service Management | Yes (simplified) | No | No |
| Installation Required | Built-in | Built-in | Download from Microsoft (no install needed) |

### Practical Implications

**Industrial Application:** A systems administrator observing intermittent server slowdowns uses Process Monitor to capture all file system and registry access events during the degradation window, pinpointing a misconfigured antivirus scan that repeatedly locks a critical application database file.

**Technical Constraint:** Task Manager's Services tab provides only a simplified, read-only view of service status. Configuration changes (startup type, log-on account, recovery actions) must be performed via `services.msc`. A misconception is that ending a process in Task Manager constitutes a graceful shutdown; it forcibly terminates the process, potentially causing data loss.

---

## Module 5: Windows User Management and UAC

### Executive Summary

Windows implements a role-based access control model through user accounts and groups. Standard users operate with restricted permissions to protect system integrity, while administrators possess elevated privileges necessary for system-wide changes. User Account Control (UAC) enforces a least-privilege execution model even for administrator accounts by requiring explicit consent for privilege elevation.

### Technical Specifications

**Terminology**

- **Standard User:** A Windows account type with restricted permissions that cannot install software system-wide, modify system files, or alter configurations that affect all users.
- **Administrator:** A Windows account type with elevated privileges capable of performing system-wide changes, including software installation, user management, and security policy modification.
- **Group:** A named collection of user accounts used to simplify permission assignment; adding a user to the "Administrators" group grants administrative privileges.
- **UAC (User Account Control):** A Windows security feature that intercepts requests for administrative privileges and prompts for consent or credential entry, isolating elevated operations to the specific task at hand.
- **SYSTEM Account:** An internal Windows account used by the operating system and its services; it possesses the highest local privilege level and is not visible in User Manager.

**Operational Logic**

1. A new user is created via Computer Management → Local Users and Groups, or via `lusrmgr.msc`.
2. The user is assigned to one or more groups (e.g., "Users" for standard, "Administrators" for elevated access).
3. When a standard user or an administrator attempts an operation requiring elevation, UAC intercepts the request.
4. A UAC prompt appears requesting consent (if already an admin) or administrative credentials (if a standard user).
5. Upon approval, the process is granted a temporary elevated token isolated to that specific operation; the user's session reverts to standard permissions afterward.
6. To manually launch a process with elevation: right-click the application → "Run as administrator," or use `Ctrl + Shift + Enter` from the Windows search bar.

**Standard Formulas / Syntax**

Create a new local administrator user (procedural):

```
Computer Management → Local Users and Groups → Users → New User
Set username → Create → Open user → Member Of → Add → Administrators
```

### Comparative Analysis

| Feature | Standard User | Administrator Account |
|---|---|---|
| Install System-Wide Software | No | Yes (with UAC consent) |
| Modify System Files | No | Yes |
| Create/Delete Local Users | No | Yes |
| Run Processes Elevated | No (requires admin credentials via UAC) | Yes (via UAC consent prompt) |
| Affect Other User Profiles | No | Yes |
| Recommended for Daily Use | Yes | No (principle of least privilege) |

### Practical Implications

**Industrial Application:** An enterprise enforces a policy where all workstation users have standard accounts, with a separate, named administrator account used only when IT tasks require elevation. This limits the blast radius of malware that relies on the current user's privilege level.

**Technical Constraint:** Operating as a daily-use administrator account does not mean all processes run with administrative privileges. UAC still enforces standard-user token execution for most applications. A common misconception is that being in the Administrators group is equivalent to having SYSTEM-level access; SYSTEM is a separate, non-interactive internal principal with its own permissions.

---

## Module 6: File Access Management and Permissions

### Executive Summary

Windows uses a layered permission model based on NTFS access control lists (ACLs) and, for network resources, shared folder permissions. Every file and folder object has an associated security descriptor containing an ACL that enumerates the specific access rights granted or denied to users and groups. Permissions are additive, except for the Deny permission, which overrides all grants.

### Technical Specifications

**Terminology**

- **ACL (Access Control List):** A data structure attached to a filesystem object that contains an ordered list of Access Control Entries (ACEs) defining who can perform which operations on that object.
- **ACE (Access Control Entry):** An individual rule within an ACL specifying a security principal (user or group), the type of access (allow/deny), and the specific permissions granted or denied.
- **Inheritance:** A mechanism by which permission settings defined on a parent folder propagate automatically to all child objects (files and subfolders). Inheritance can be broken and replaced with explicit permissions.
- **Ownership:** The designation of a user or group as the owner of a file or folder. Owners retain the right to modify permissions on their objects regardless of any access restrictions applied.
- **AGDLP:** A Microsoft best-practice acronym for structuring AD permissions: Accounts → Global groups → Domain Local groups → Permissions. This model promotes scalability and manageability.

**Operational Logic**

1. A file or folder's permissions are accessible via right-click → Properties → Security tab.
2. Click "Edit" to modify permissions; "Add" to include new users or groups (use "Check Names" to validate).
3. Assign standard permissions (Full Control, Modify, Read & Execute, List Folder Contents, Read, Write) per principal.
4. For granular control, open "Advanced" to configure individual permission flags or change inheritance behavior.
5. When a user is remote (accessing via network), the effective permission is the most restrictive intersection of NTFS and shared folder permissions.
6. When a user accesses a resource locally, only NTFS permissions apply; shared permissions are irrelevant for local access.

**Standard Formulas / Syntax**

Effective permission rule for remote access:

```
Effective Permission = MOST RESTRICTIVE of (NTFS Permission ∩ Shared Permission)
```

NTFS permission is always in effect; shared permission applies only for remote access:

```
Local access:  Effective = NTFS permissions only
Remote access: Effective = min(NTFS, Shared)
```

AGDLP model:

```
A  (Accounts)           → Create user accounts
G  (Global Groups)      → Place user accounts into global groups
DL (Domain Local Groups)→ Place global groups into domain local groups
P  (Permissions)        → Assign permissions to domain local groups
```

### Comparative Analysis

| Feature | NTFS Permissions | Shared Folder Permissions |
|---|---|---|
| Applies Locally | Yes | No |
| Applies Remotely | Yes | Yes |
| Per-File Granularity | Yes | No (folder-level only) |
| Additive (Multiple Groups) | Yes | Yes |
| Deny Override | Yes | Yes |
| Default Permission | Users = Read | Administrators = Full Control |

### Practical Implications

**Industrial Application:** A finance department share is configured with NTFS Full Control for the finance group and Read-Only for auditors. The shared permission is set to Full Control for everyone, so the effective remote permission for auditors is Read-Only (the most restrictive of the two layers).

**Technical Constraint:** A user cannot remove permission entries from a folder while permission inheritance is enabled. Inheritance must first be disabled and inherited permissions converted to explicit permissions before modifications can be made. This is a frequent point of confusion during lab exercises.

---

## Module 7: Network Sharing and SMB

### Executive Summary

Windows implements network file sharing via the Server Message Block (SMB) protocol, which allows clients to access files, printers, and other resources on remote machines over a local area network. Windows creates several administrative default shares automatically to facilitate remote system management. Samba provides cross-platform interoperability by implementing SMB on non-Windows systems.

### Technical Specifications

**Terminology**

- **SMB (Server Message Block):** A client-server communication protocol used for sharing files, printers, and serial ports across a network; the dominant file-sharing protocol in Windows environments.
- **CIFS (Common Internet File System):** An older dialect of SMB that was the Windows standard prior to SMB 3; deprecated in favor of SMB 3, which provides better security and performance.
- **UNC (Universal Naming Convention):** A standard path format for identifying network resources: `\\<hostname>\<sharename>`.
- **Hidden Share:** A network share whose name ends with a `$` symbol, causing it to be excluded from network browse listings. It remains accessible by direct UNC path.
- **Samba:** An open-source implementation of the SMB protocol suite for Unix-like systems (Linux, macOS), enabling interoperability with Windows file and print sharing.

**Operational Logic**

1. Enable network sharing via File Explorer → Network → Activate network discovery and file sharing.
2. To create a share, right-click a folder → Properties → Sharing tab → Advanced Sharing → assign a share name and permissions.
3. Append `$` to the share name to create a hidden share (e.g., `SecretDocs$`).
4. Access a share via File Explorer address bar: `\\<hostname>\<sharename>`.
5. Default administrative shares are created automatically: `C$` (C drive root), `Admin$` (Windows directory), `IPC$` (interprocess communication).
6. View all shares, including hidden ones: Computer Management → Shared Folders → Shares.

**Standard Formulas / Syntax**

UNC path syntax:

```
\\<computer name>\<shared folder name>
```

Access default administrative shares:

```
\\localhost\C$        → Root of C: drive
\\localhost\Admin$    → C:\Windows directory
\\localhost\IPC$      → Interprocess communication share (no directory)
```

SMB communication port:

```
TCP Port 445
```

### Comparative Analysis

| Feature | SMB 3 (Current) | CIFS (Legacy) | Samba |
|---|---|---|---|
| Platform | Windows (native) | Windows (legacy) | Linux / Unix |
| Encryption | Yes (AES-128) | No | Supported (TLS) |
| Performance | Improved (multichannel, Direct) | Lower | Variable |
| Security | Modern, recommended | Deprecated, less secure | Comparable to SMB |
| Cross-Platform | Windows-centric | Windows-centric | Bridges Windows and Unix |

### Practical Implications

**Industrial Application:** A hybrid-OS enterprise uses Samba on a Linux NAS appliance to provide SMB file shares to Windows domain clients, enabling seamless file access without requiring a Windows Server license for each storage node.

**Technical Constraint:** Setting the network profile to "Private" enables network discovery and file sharing, but exposes the device to all hosts on the local segment. In public or untrusted networks, the profile must remain "Public" to suppress device discovery and prevent unauthorized share access.

---

## Module 8: Windows Networking and Firewall

### Executive Summary

Windows provides a comprehensive set of network configuration tools, including static and DHCP-based IP assignment, DNS resolution override via the hosts file, and a host-based stateful firewall with profile-aware rule sets. The Windows Firewall integrates IPsec for authenticated, encrypted communication and supports network profile classification to apply context-appropriate security postures.

### Technical Specifications

**Terminology**

- **NIC (Network Interface Card):** The hardware component providing physical or wireless network connectivity; each NIC has a distinct adapter configuration in Windows.
- **DNS over HTTPS (DoH):** A protocol that encrypts DNS queries by transmitting them over HTTPS, preventing interception and manipulation of DNS traffic by network observers.
- **IPsec (Internet Protocol Security):** A protocol suite for authenticating and encrypting IP communications; supported by Windows Firewall to mandate device authentication before allowing communication.
- **Firewall Profile:** A named configuration set applied based on the detected network type: Domain, Private, or Public. Each profile has independent default rules and inbound/outbound policies.
- **Inbound Rule:** A firewall rule that controls whether incoming network traffic matching specified criteria (protocol, port, program) is permitted or blocked.

**Operational Logic**

1. Access network adapter settings: Settings → Network & Internet → Ethernet (wired) or Wi-Fi → Manage known networks (wireless).
2. Under IP assignment, select DHCP (automatic) or Manual (static); input IP address, subnet mask, default gateway, and DNS servers.
3. For local DNS overrides, edit `C:\Windows\System32\drivers\etc\hosts` with administrative privileges using `notepad.exe hosts` from the directory.
4. Windows Firewall (Defender Firewall with Advanced Security) applies inbound and outbound rules based on the active network profile (Domain, Private, or Public).
5. By default, all inbound connections are blocked and all outbound connections are allowed for all three profiles.
6. Create new inbound rules by navigating to Windows Defender Firewall → Inbound Rules → New Rule; specify Program, Port, Predefined, or Custom rule type.

**Standard Formulas / Syntax**

Navigate to hosts file:

```
cmd (admin) → cd C:\Windows\System32\drivers\etc\
notepad.exe hosts
```

Hosts file entry format:

```
<IP address>    <hostname>
192.168.1.50    staging.company.local
```

Network settings path (wired):

```
Settings > Network & internet > Ethernet
```

Advanced sharing settings path:

```
Network & internet > Advanced network settings > Advanced sharing settings
```

### Comparative Analysis

| Feature | Domain Profile | Private Profile | Public Profile |
|---|---|---|---|
| Use Case | Networks with AD authentication | Home / trusted office networks | Airports, hotels, public Wi-Fi |
| Default Inbound | Block all (unless rule allows) | Block all | Block all |
| Default Outbound | Allow all | Allow all | Allow all |
| Network Discovery | Configured per AD policy | Enabled (optional) | Disabled |
| Security Level | Managed by GPO | Moderate | Highest |

### Practical Implications

**Industrial Application:** A corporate laptop automatically applies the Domain firewall profile when connected to the office network (where a domain controller is reachable), enforcing GPO-defined inbound rules. When the same laptop connects to a hotel Wi-Fi, it switches to the Public profile, blocking all inbound connections by default.

**Technical Constraint:** The local hosts file has the highest DNS resolution priority in Windows, overriding DNS server responses. While useful for testing and redirection, this creates a security risk if malicious actors can write to the hosts file, silently redirecting traffic to fraudulent hosts. The hosts file must be write-protected except during authorized administrative changes.

---

## Module 9: Windows Registry

### Executive Summary

The Windows Registry is a hierarchical, binary key-value database that serves as the central configuration store for the Windows OS, installed applications, and hardware components. It is organized into five top-level hives, each governing a distinct scope of configuration. Any modification carries significant risk of system instability; backups prior to changes are mandatory best practice.

### Technical Specifications

**Terminology**

- **Hive:** A top-level organizational node of the Registry tree. There are five hives, each containing keys, subkeys, and values pertaining to a specific configuration scope.
- **Key:** A named node within the Registry tree that can contain subkeys and value entries; analogous to a folder in a file system.
- **Value:** A named data entry within a Registry key that stores configuration information in a specified type (REG_SZ string, REG_DWORD 32-bit integer, REG_BINARY, etc.).
- **HKLM (HKEY_LOCAL_MACHINE):** The Registry hive containing system-wide settings including hardware configuration, installed software, security policies, and boot parameters. The most critical hive.
- **Registry Export (.reg file):** A human-readable text file representation of a Registry key or hive that can be imported to restore or replicate settings; can be weaponized if sourced from untrusted origins.

**Operational Logic**

1. Open Registry Editor: `Windows + R` → `regedit` (requires administrative privileges).
2. Navigate the tree to the target key or hive.
3. Before making changes, export a backup: File → Export → select scope → name and save the `.reg` file.
4. Modify, add, or delete keys and values as required.
5. To restore from backup: File → Import → locate and open the saved `.reg` file.
6. Note: Some hive-level backups may fail due to locked keys in active use; prefer targeted subkey exports.

**Standard Formulas / Syntax**

Five Registry Hives:

```
HKEY_CLASSES_ROOT  (HKCR) → File type associations and COM class registrations
HKEY_CURRENT_USER  (HKCU) → Settings for the currently logged-in user
HKEY_LOCAL_MACHINE (HKLM) → System-wide configuration (hardware, software, security)
HKEY_USERS         (HKU)  → Profiles for all loaded user accounts
HKEY_CURRENT_CONFIG       → Current hardware profile (non-persistent)
```

### Comparative Analysis

| Hive | Scope | Persistence | Key Risk if Corrupted |
|---|---|---|---|
| HKCR | File associations, COM | Persistent | Applications fail to open associated files |
| HKCU | Per-user settings | Persistent | User profile settings lost |
| HKLM | System-wide / software | Persistent | System instability or failure to boot |
| HKU | All user profiles | Persistent | User session initialization failures |
| HKEY_CURRENT_CONFIG | Hardware profile | Non-persistent | Display/hardware initialization errors |

### Practical Implications

**Industrial Application:** An IT administrator uses a `.reg` file to push a configuration change (e.g., disabling USB storage) to a large fleet of machines via login script, eliminating the need for manual Registry edits on each workstation.

**Technical Constraint:** Downloading and executing `.reg` files from unverified sources is a significant security risk. Such files can silently modify critical system settings, disable security features, or introduce persistence mechanisms for malware. Every `.reg` file must be reviewed in a text editor before execution.

---

## Module 10: Windows Services

### Executive Summary

Windows Services are specialized processes that execute in the background without a user interface. They provide the foundational functions of the OS, including networking, security, event logging, and hardware management. Services operate under defined service accounts, can be configured to start automatically or on demand, and include recovery policies that define behavior upon failure.

### Technical Specifications

**Terminology**

- **Startup Type:** A configuration attribute of a Windows Service defining when and how it starts: Automatic, Automatic (Delayed Start), Manual, or Disabled.
- **Service Account:** The user principal under which a service runs, defining its privilege scope. Options include SYSTEM, NetworkService, LocalService, or a custom domain account.
- **Recovery Action:** A configurable response to service failure; options include restarting the service, running a program, or rebooting the computer after a specified number of failures.
- **Delayed Start:** A startup type that defers service initialization until after the system has fully booted, reducing the time-to-desktop by staggering the startup load.
- **Dependency:** A service relationship where one service requires another to be running before it can start; failure of a dependency prevents the dependent service from starting.

**Operational Logic**

1. Open Services management console: `Windows + R` → `services.msc`.
2. Locate the target service in the Name column; review Status (Running/Stopped) and Startup Type.
3. Right-click a service to Start, Stop, Pause, Resume, or Restart it.
4. Double-click a service to access its Properties dialog:
   - **General tab:** Startup type configuration.
   - **Log On tab:** Service account assignment (principle of least privilege).
   - **Recovery tab:** Failure response policy (first, second, and subsequent failure actions).
   - **Dependencies tab:** View prerequisite services.
5. Services can also be viewed in Task Manager (Services tab) for status, but configuration requires `services.msc`.

**Standard Formulas / Syntax**

Startup type options:

```
Automatic          → Starts at system boot
Automatic (Delayed)→ Starts after desktop is ready (reduces boot time)
Manual             → Starts only when explicitly invoked
Disabled           → Service will not run under any condition
```

Open Services console:

```
Windows + R → services.msc
```

### Comparative Analysis

| Feature | Services UI (`services.msc`) | Task Manager Services Tab |
|---|---|---|
| View Service Status | Yes | Yes |
| Start / Stop Services | Yes | Yes |
| Configure Startup Type | Yes | No |
| Set Service Account | Yes (Log On tab) | No |
| Configure Recovery Policy | Yes (Recovery tab) | No |
| View Dependencies | Yes | No |
| Process Linkage | Indirect | Direct link to Details tab |
| Target User | IT administrators | General monitoring |

### Practical Implications

**Industrial Application:** A Windows Server running a critical database service is configured with an Automatic (Delayed Start) type to prevent resource contention during boot, and its Recovery tab is set to automatically restart the service on first and second failure, then reboot the server on the third failure to ensure high availability.

**Technical Constraint:** Disabling essential Windows services based on outdated online advice is a common cause of system instability. Services like Windows Update, Windows Defender, and the Event Log service are interdependent. Disabling one can silently break dependent services, and the failure may not manifest immediately.

---

## Module 11: Windows Server Role Management

### Executive Summary

Windows Server operates on a role-based architecture in which distinct server functions (roles) are installed as independent software modules. Each role provides a specific network service and may be composed of multiple role services. Features augment roles with supplementary capabilities. This modular approach enables right-sized deployment and reduces the attack surface by limiting installed components to those required.

### Technical Specifications

**Terminology**

- **Server Role:** A software module that enables a Windows Server to perform a specific network function (e.g., DNS Server, DHCP Server, Active Directory Domain Services).
- **Role Service:** A sub-component of a role that provides discrete, selectable functionality. For example, Remote Desktop Services contains separate role services for the Session Host, Gateway, and Licensing components.
- **Feature:** A software component that supports or augments one or more roles but is not a role itself (e.g., Failover Clustering, Telnet Client, BitLocker).
- **SPoF (Single Point of Failure):** A configuration in which a single component's failure causes total service outage; mitigated through redundancy and high-availability designs.
- **Server Manager:** The Windows Server administrative console used to install, configure, and remove roles, role services, and features on local and remote servers.

**Operational Logic**

1. Log in to Windows Server with an administrator account.
2. Open Server Manager (launches automatically on login by default).
3. Navigate to "Add Roles and Features" wizard.
4. Select the target server and choose "Role-based or feature-based installation."
5. Select the desired roles (e.g., DHCP Server, AD DS); associated role services are presented for optional inclusion.
6. Select any supporting features (e.g., Group Policy Management, Remote Server Administration Tools).
7. Complete the wizard; some roles require post-installation configuration steps (e.g., DHCP authorization in AD, AD DS domain promotion).

**Standard Formulas / Syntax**

Install DHCP Server role via PowerShell (alternative to GUI):

```powershell
Install-WindowsFeature DHCP -IncludeManagementTools
```

### Comparative Analysis

| Component | Role | Role Service | Feature |
|---|---|---|---|
| Definition | Primary server function | Sub-function of a role | Supporting capability |
| Example | Active Directory DS | AD Lightweight Directory Services | Group Policy Management |
| Standalone | Yes | No (requires parent role) | Yes |
| Directly serves users | Yes | Yes | Usually indirectly |

### Practical Implications

**Industrial Application:** A small enterprise deploys a single Windows Server that simultaneously runs the DHCP, DNS, and Active Directory Domain Services roles to minimize hardware costs. The IT architect documents this as a deliberate SPoF trade-off, with plans to introduce a second domain controller for redundancy before scaling.

**Technical Constraint:** Running multiple resource-intensive roles on a single server without redundancy creates an SPoF. If that server fails, all dependent services (DNS, DHCP, authentication) fail simultaneously. Best practice dictates separating critical roles across multiple servers or implementing role-specific failover mechanisms.

---

## Module 12: DHCP Server Configuration

### Executive Summary

The Dynamic Host Configuration Protocol (DHCP) automates the assignment of IP addresses and network configuration parameters to client devices, eliminating the administrative burden of manual static IP configuration. Windows Server provides DHCP as an installable role with a scope-based allocation model, lease management, reservation support, and failover capabilities.

### Technical Specifications

**Terminology**

- **Scope:** A defined range of IP addresses that the DHCP server is authorized to lease to clients, along with associated configuration options (gateway, DNS, lease duration).
- **Lease:** A time-limited assignment of an IP address to a DHCP client. The client must renew the lease at the midpoint of the lease period; the default Windows Server lease duration is eight days.
- **Reservation:** A static binding within the DHCP scope that always assigns a specific IP address to a client identified by its MAC address, combining DHCP convenience with static addressing predictability.
- **DORA Process:** The four-step DHCP negotiation handshake: Discover → Offer → Request → Acknowledge.
- **DHCP Snooping:** A network switch security feature that validates DHCP messages and blocks responses from unauthorized (rogue) DHCP servers on untrusted switch ports.

**Operational Logic**

1. Install the DHCP role via Server Manager or PowerShell (`Install-WindowsFeature DHCP -IncludeManagementTools`).
2. In the DHCP console, authorize the server in Active Directory (requires Enterprise Admin privileges).
3. Define a scope: specify the address range, exclusions for static devices, subnet mask, default gateway, DNS servers, and lease duration.
4. Activate the scope to begin serving leases.
5. Clients use the DORA process to obtain an IP configuration. Verify using PowerShell (`Get-NetIPConfiguration`) or `ipconfig`.
6. Monitor DHCP via Event Viewer (Applications and Services → Microsoft → Windows → DHCP-Server) and text logs at `C:\Windows\System32\dhcp`.

**Standard Formulas / Syntax**

DORA process:

```
1. Discover   → Client broadcasts to find DHCP servers
2. Offer      → Server offers an available IP configuration
3. Request    → Client formally requests the offered configuration
4. Acknowledge → Server confirms the lease assignment
```

Example scope design:

```
Network:           192.168.2.0 /24
Static range:      192.168.2.1 – 192.168.2.25
Dynamic range:     192.168.2.26 – 192.168.2.254
Default lease:     8 days
```

DHCP log path:

```
C:\Windows\System32\dhcp
```

### Comparative Analysis

| Feature | DNS | DHCP |
|---|---|---|
| Purpose | Name-to-IP resolution | Dynamic IP address allocation |
| Default Port | TCP/UDP 53 | UDP 67 (server), UDP 68 (client) |
| Transport | TCP and UDP | UDP only |
| Topology | Decentralized (hierarchical) | Centralized (per subnet) |
| Scope | Global (internet-scale) | Local network segments |
| Authorization in AD | Not required | Required (prevents rogue servers) |

### Practical Implications

**Industrial Application:** A corporate network administrator segments DHCP scopes by VLAN, placing server VLANs with static addressing outside the dynamic pool and configuring MAC-based reservations for printers and network appliances to ensure stable addressing without manual static configuration.

**Technical Constraint:** Multiple unauthorized DHCP servers on the same network cause IP address conflicts and inconsistent gateway/DNS information, leading to widespread connectivity failures. Windows DHCP servers must be authorized in Active Directory, and DHCP snooping should be enabled on network switches to prevent rogue DHCP servers from operating.

---

## Module 13: PowerShell and Headless Server Administration

### Executive Summary

PowerShell is a .NET-based task automation and configuration management shell that represents the strategic command-line interface for Windows Server administration. It supersedes the legacy Command Prompt (cmd.exe) in capability and is the exclusive management interface for Windows Server Core (headless) deployments. Its object-oriented pipeline and extensive cmdlet library enable complex automation, remote management, and Active Directory operations.

### Technical Specifications

**Terminology**

- **Cmdlet:** A .NET-based command in PowerShell following the verb-noun naming convention (e.g., `Get-Process`, `Set-Service`), returning structured .NET objects rather than plain text.
- **Pipeline:** A PowerShell construct that passes the output of one cmdlet as structured input to the next, enabling complex data transformations without intermediate storage.
- **Headless Server (Server Core):** A Windows Server installation mode that omits the graphical desktop environment, reducing memory/CPU overhead, minimizing the attack surface, and requiring management exclusively via CLI, PowerShell, or Remote Server Administration Tools (RSAT).
- **WMI (Windows Management Instrumentation):** A Windows framework for querying and managing system components; accessible natively from PowerShell through the `Get-WmiObject` and `Get-CimInstance` cmdlets.
- **PSScriptAnalyzer:** A static code analysis module for PowerShell that enforces style conventions and best practices; integrated with the PowerShell extension in Visual Studio Code.

**Operational Logic**

1. Open PowerShell with standard or elevated privileges as required.
2. Use cmdlets with the verb-noun syntax; explore available commands with `Get-Command` and documentation with `Get-Help <cmdlet>`.
3. Chain commands using the pipeline (`|`) to pass objects between cmdlets.
4. For Active Directory operations, ensure the RSAT AD DS Tools are installed; use cmdlets from the `ActiveDirectory` module.
5. For scripting, save commands in `.ps1` files; scripts can be executed interactively or scheduled via Task Scheduler.
6. On headless Server Core installations, all administration is performed via PowerShell or by connecting RSAT tools from a remote management workstation.

**Standard Formulas / Syntax**

PowerShell script to bulk-create AD users from CSV:

```powershell
$csv = Import-Csv C:\Users\student\Desktop\ADUsers.csv -Encoding utf8
foreach ($user in $csv) {
    New-ADUser -Name $user.Name `
               -GivenName $user.GivenName `
               -Surname $user.Surname `
               -SamAccountName $user.SamAccountName `
               -UserPrincipalName $user.UserPrincipalName `
               -Path $user.Path `
               -AccountPassword (ConvertTo-SecureString 'Password123' -AsPlainText -Force) `
               -Enabled $true
}
```

Single AD user creation:

```powershell
New-ADUser -Name "First Last" `
           -GivenName "First" `
           -Surname "Last" `
           -SamAccountName "flast" `
           -UserPrincipalName "flast@domain.org" `
           -Path "OU=Users,OU=Department,DC=domain,DC=org" `
           -AccountPassword (Read-Host -AsSecureString "Enter Password") `
           -Enabled $true
```

### Comparative Analysis

| Feature | cmd.exe | Windows Terminal | PowerShell |
|---|---|---|---|
| Technology Base | MS-DOS legacy | Terminal emulator (hosts shells) | .NET Framework |
| Object Output | Text strings | Depends on hosted shell | .NET objects |
| Scripting | Batch (.bat) | N/A (host only) | Full scripting language (.ps1) |
| AD Management | Limited | Via hosted PowerShell | Native (`ActiveDirectory` module) |
| Cross-Platform | No | Hosts cross-platform shells (WSL) | Yes (PowerShell Core) |
| Security | Limited | Depends on hosted shell | Execution policy, signing support |
| Remote Management | Limited | Depends on hosted shell | Full (PSRemoting, WinRM) |

### Practical Implications

**Industrial Application:** An IT team automates the onboarding of 500 new employees by executing a PowerShell script that reads a CSV export from the HR system and creates all Active Directory accounts, assigns group memberships, and provisions home directories in a single operation.

**Technical Constraint:** Errors in a PowerShell automation script are amplified at scale. A logic error that would corrupt one manual entry can corrupt thousands of records when executed in a loop. Thorough testing in a non-production environment, combined with version control and error handling (`try/catch`), is mandatory before deploying automation scripts against production AD.

---

## Module 14: Windows Event Logging

### Executive Summary

The Windows Event Log is the central logging infrastructure for Windows operating systems and servers, capturing system, application, and security events in structured EVTX format. Event logs are essential for troubleshooting, compliance auditing, security incident forensics, and monitoring. They are the primary mechanism through which system administrators establish situational awareness of server health and security posture.

### Technical Specifications

**Terminology**

- **EVTX:** The binary XML-based Event Log file format introduced in Windows Vista and Server 2008, replacing the older EVT format. Each log entry is represented as structured XML, facilitating parsing by SIEM systems.
- **Event ID:** A numeric identifier assigned to a specific type of event within an Event Log channel, used to filter and correlate log entries (e.g., Event ID 4624 = successful logon).
- **SIEM (Security Information and Event Management):** An enterprise platform that aggregates, correlates, and analyzes log data from multiple sources to detect threats and support compliance reporting.
- **Log Level:** A severity classification applied to each event entry: Information, Warning, Error, Critical (for system events); Success Audit, Failure Audit (for security events).
- **Log Channel:** A named stream of event data within the Event Log subsystem: System, Application, Security, and operational logs for specific Windows components.

**Operational Logic**

1. Open Event Viewer: `Windows + R` → `eventvwr.msc`.
2. Expand "Windows Logs" to access the System, Application, and Security channels.
3. Apply filters to isolate events: right-click a log → "Filter Current Log" → specify Event IDs, log level, time range, or source.
4. Double-click an event to view its full detail, including timestamp, source, Event ID, description, and associated data fields.
5. For security auditing of RDP access, filter the Security log for Event IDs 4624 and 4672; verify Logon Type = 10 for Remote Interactive (RDP) sessions.
6. For enterprise environments, forward relevant events to a centralized SIEM using Windows Event Forwarding (WEF) or a SIEM agent.

**Standard Formulas / Syntax**

Key Security Event IDs:

```
4624 → Successful logon
4625 → Failed logon
4672 → Special privileges assigned to logon (admin rights)
4768 → Kerberos TGT requested (AD authentication)
Logon Type 2  = Interactive (local console)
Logon Type 3  = Network
Logon Type 10 = Remote Interactive (RDP)
```

Log file location (default):

```
%SystemRoot%\System32\winevt\Logs\
```

### Comparative Analysis

| Log Channel | Primary Content | Security Relevance |
|---|---|---|
| System | OS component events, driver failures, service state changes | Hardware failures, unauthorized service stops |
| Application | Events from installed applications and programs | Application crashes, configuration errors |
| Security | Logon/logoff, object access, privilege use, policy changes | Authentication anomalies, access violations |
| Operational (e.g., DHCP) | Role-specific diagnostic and operational events | Role misconfiguration, anomalous allocations |

### Practical Implications

**Industrial Application:** A security analyst configures Windows Event Forwarding on all domain-joined servers to push Security log events (filtered to critical IDs: 4624, 4625, 4688, 4698) to a centralized SIEM. Correlation rules trigger alerts when more than five consecutive 4625 (failed logon) events occur within a 60-second window on any host, providing near-real-time brute-force detection.

**Technical Constraint:** Every Windows system generates routine error and warning events in its logs as a normal operational condition. The presence of such events does not indicate compromise. A common social engineering tactic (tech support scam) involves directing unsuspecting users to Event Viewer and misrepresenting ordinary warnings as evidence of malware, then charging for fraudulent remediation. Microsoft does not make unsolicited calls for technical support.

---

## Module 15: Remote Desktop Protocol (RDP)

### Executive Summary

The Remote Desktop Protocol (RDP), developed by Microsoft, provides a graphical remote access interface to Windows machines over a network. It enables IT administrators to manage servers without physical access and support end users remotely. RDP operates over TCP port 3389 and is integrated natively into Windows Pro, Enterprise, and Education editions. Security configurations are critical given the protocol's history as a target for credential attacks.

### Technical Specifications

**Terminology**

- **RDP (Remote Desktop Protocol):** A proprietary Microsoft protocol that transmits the display output and input events of a remote Windows session over a network connection, providing full graphical desktop access.
- **RDP Server:** The Windows machine being accessed remotely; must have Remote Desktop enabled and must be running a supported edition (Pro, Enterprise, Education, or Server).
- **RDP Client:** The device initiating the remote connection; uses the Remote Desktop Connection tool (`mstsc.exe`) or equivalent client software.
- **NAT (Network Address Translation):** A routing technique that maps internal private IP addresses to a single public address; relevant to RDP in that it can obscure client identity and provide a supplementary layer of network-level isolation.
- **SSH (Secure Shell):** A cryptographic network protocol providing secure command-line access to remote systems; text-based and lightweight, contrasting with RDP's graphical interface.

**Operational Logic**

1. Enable Remote Desktop on the target machine: Settings → System → Remote Desktop → toggle "Enable Remote Desktop."
2. Ensure the target machine is running Windows Pro, Enterprise, Education, or Server editions.
3. Configure the Windows Firewall to allow inbound TCP traffic on port 3389.
4. On the client, open "Remote Desktop Connection" (Start Menu search or `mstsc.exe`) and enter the target's hostname or IP address.
5. Authenticate with valid credentials; the remote session begins.
6. After a session, verify connection in the server's Security Event Log: filter for Event IDs 4624 and 4672 with Logon Type 10.

**Standard Formulas / Syntax**

Enable Remote Desktop via Settings:

```
Settings > System > Remote Desktop > Enable Remote Desktop [toggle ON]
```

RDP default port:

```
TCP Port 3389
```

Verify RDP access in Event Log:

```
eventvwr.msc → Windows Logs → Security
Filter: Event ID 4624, 4672 | Logon Type: 10
```

### Comparative Analysis

| Feature | RDP | SSH | PowerShell Remoting | Cloud Remote Desktop |
|---|---|---|---|---|
| Interface Type | Full graphical (GUI) | Command-line only | Command-line / scripted | Full graphical (GUI) |
| Primary Platform | Windows | Linux / Unix (also Windows) | Windows (PowerShell Core: cross-platform) | Cloud-hosted (any platform) |
| Bandwidth Usage | High (graphical rendering) | Low | Low to moderate | High |
| Native Windows Availability | Yes | Requires OpenSSH feature | Yes | Requires cloud subscription |
| Default Port | TCP 3389 | TCP 22 | TCP 5985 (HTTP) / 5986 (HTTPS) | Varies |
| Authentication | Windows credentials, NLA | Key-based or password | Windows credentials, certificates | MFA via cloud identity provider |

### Practical Implications

**Industrial Application:** A data center operations team uses RDP with Network Level Authentication (NLA) enabled to administer a fleet of Windows Servers from a central jump host, ensuring that credentials are not exposed on the wire and that sessions can only be initiated by domain-authenticated personnel.

**Technical Constraint:** Exposing RDP (TCP 3389) directly to the internet without additional controls (VPN gateway, NLA, IP allowlisting, or MFA) is a critical security misconfiguration and a common vector for ransomware deployment and credential stuffing attacks. RDP should never be accessible from the public internet without layered authentication controls.

---

## Module 16: Active Directory Domain Services

### Executive Summary

Active Directory Domain Services (AD DS) is Microsoft's directory service that provides centralized identity management, authentication, and authorization for Windows domain environments. It organizes network objects (users, computers, groups, printers) into a hierarchical structure of organizational units, domains, trees, and forests. AD DS underpins Group Policy enforcement, Kerberos-based authentication, and LDAP-based directory queries across the enterprise.

### Technical Specifications

**Terminology**

- **Domain Controller (DC):** A server running AD DS that hosts a replicated copy of the Active Directory database, processes authentication requests, and enforces Group Policy for the domain.
- **Organizational Unit (OU):** A container object within a domain used to logically group users, computers, and groups; the primary unit for delegating administrative control and applying Group Policy Objects.
- **Security Identifier (SID):** A unique immutable identifier assigned to every security principal (user, group, computer) in Active Directory; used internally for all access control decisions.
- **Group Policy Object (GPO):** A named collection of policy settings that can be linked to sites, domains, or OUs to enforce configuration and security settings on all applicable objects.
- **AGDLP:** The Microsoft-recommended permission assignment strategy in AD: assign permissions to Domain Local groups, populate them with Global groups, and place user Accounts into Global groups.

**Operational Logic**

1. Install AD DS role via Server Manager → Promote the server to a domain controller → specify domain name and forest/domain functional level.
2. After promotion, the DNS Server role is co-installed (AD DS is DNS-dependent).
3. Users and computers are created and organized into OUs using "Active Directory Users and Computers" (accessible via MMC snap-in or RSAT).
4. Group policies are created in Group Policy Management Console and linked to the appropriate OU, domain, or site.
5. GPO processing order: Local → Site → Domain → OU (LSDOU); the OU-level policy is the most authoritative (lowest precedence value wins).
6. Clients join the domain via System Properties → Domain Join (requires DNS resolution of the domain name and a valid domain administrator credential).

**Standard Formulas / Syntax**

Group Policy processing order (LSDOU):

```
1. Local Policy (lowest precedence)
2. Site Policy
3. Domain Policy
4. OU Policy (highest precedence — closest to the object wins)
```

SID format example:

```
S-1-5-21-<domain identifier>-<relative identifier>
```

AD default user container path (LDAP notation):

```
CN=Users,DC=<domain>,DC=<tld>
```

### Comparative Analysis

| Concept | Domain | Tree | Forest |
|---|---|---|---|
| Definition | Logical grouping of objects sharing a single AD database | Collection of domains sharing a common DNS namespace | Collection of domain trees; the security boundary |
| Namespace | Unique domain name (e.g., `company.local`) | Hierarchical (e.g., `zuerich.company.local`) | Multiple root domains |
| Trust | Implicit within domain | Transitive between parent and child | Transitive across trees within forest |
| Use Case | Single-site organization | Multi-site with shared namespace | Multi-company or geographically dispersed enterprise |
| Complexity | Low | Moderate | High |

### Practical Implications

**Industrial Application:** A multinational corporation structures its Active Directory with a single forest containing domain trees per geographic region. Each regional tree (e.g., `eu.corp.local`, `us.corp.local`) manages its own users and computers while sharing transitive trust relationships, enabling cross-region resource access under a unified security policy framework.

**Technical Constraint:** OUs are not security principals; they cannot be assigned permissions directly. Permission assignment in AD must follow the AGDLP model. A common misconception is that placing users in an OU grants them permissions to resources within that OU; OUs exist for organizational and GPO-application purposes only.

---

## Module 17: LDAP and Kerberos

### Executive Summary

LDAP (Lightweight Directory Access Protocol) and Kerberos are the two foundational security protocols that underpin Active Directory's authentication and directory access architecture. LDAP provides the query and modification interface for the AD directory database, while Kerberos provides the mutual authentication framework that verifies identities without transmitting credentials over the network. Together, they enforce secure, scalable identity management in Windows domain environments.

### Technical Specifications

**Terminology**

- **LDAP (Lightweight Directory Access Protocol):** A TCP/IP-based protocol for querying and modifying directory services, derived from the X.500 DAP standard. LDAPv3 (RFC 4511, 1997) is the current standard and the basis for Microsoft Active Directory's directory access layer.
- **Kerberos:** A symmetric-key network authentication protocol (developed at MIT, adopted as the default AD authentication protocol in Windows 2000) that uses a trusted third party (Key Distribution Center / KDC) to issue time-limited tickets, avoiding credential transmission over the network.
- **KDC (Key Distribution Center):** An AD component co-located on every Domain Controller, comprising the Authentication Service (AS) and the Ticket Granting Service (TGS), responsible for issuing Kerberos tickets.
- **TGT (Ticket Granting Ticket):** An encrypted Kerberos credential issued after initial authentication that allows the client to request service tickets for specific resources without re-entering credentials.
- **SLDAP (Secure LDAP):** LDAP transmitted over TLS/SSL to encrypt directory queries and data; operates on TCP port 636 and requires a valid certificate on the domain controller.

**Operational Logic**

1. A user enters credentials at domain login; the client sends an authentication request to the KDC (Authentication Service).
2. The KDC validates the user, issues a TGT encrypted with the user's password hash, and returns it to the client.
3. When the user accesses a resource (e.g., a file share), the client presents its TGT to the TGS, which issues a Service Ticket for that specific resource.
4. The client presents the Service Ticket to the target server; the server decrypts it using its own shared secret with the KDC to verify authenticity.
5. Access is granted or denied based on the user's SID and the resource's ACL; no credential is transmitted over the network in plaintext.
6. LDAP queries (e.g., group membership lookups, user attribute reads) are performed against the AD database on TCP port 389 (LDAP) or 636 (SLDAP).

**Standard Formulas / Syntax**

LDAP and SLDAP port assignments:

```
TCP 389 → Standard LDAP (unencrypted by default)
TCP 636 → Secure LDAP (LDAP over TLS/SSL)
```

LDAP distinguished name (DN) format:

```
CN=<common name>,OU=<organizational unit>,DC=<domain component>,DC=<domain component>
Example: CN=John Smith,OU=Finance,DC=company,DC=local
```

Kerberos authentication flow (simplified):

```
Client → AS (KDC): Authentication Request
AS → Client:       TGT (encrypted)
Client → TGS (KDC): TGT + Service Request
TGS → Client:      Service Ticket
Client → Server:   Service Ticket
Server → Client:   Access Granted / Denied
```

### Comparative Analysis

| Feature | LDAP | Kerberos |
|---|---|---|
| Function | Directory query and modification | Network authentication |
| Protocol Type | Application-layer (TCP/IP) | Authentication protocol (UDP/TCP) |
| Default Port | 389 (LDAP), 636 (SLDAP) | 88 (UDP/TCP) |
| Credential Exposure | Credentials if unencrypted (use SLDAP) | No credentials transmitted over network |
| Encryption | Optional (requires TLS for SLDAP) | Built-in (symmetric key cryptography) |
| Standards | LDAPv3 (RFC 4511, 1997) | Kerberos v5 (RFC 4120) |
| History | Derived from X.500 DAP (1988); LDAPv3 finalized 1997 | MIT Project Athena; AD adoption in Windows 2000 |

### Practical Implications

**Industrial Application:** An enterprise enforces SLDAP (port 636 with a valid PKI certificate on all DCs) for all directory service queries, ensuring that HR system integrations and web application directory lookups do not expose user attribute data or authentication tokens in plaintext on the internal network.

**Technical Constraint:** If a user whose account is deleted from AD has encrypted files using EFS (Encrypting File System) — which ties encryption keys to the user's SID via Kerberos credentials — those files become permanently inaccessible after the account deletion. Administrators must ensure EFS-encrypted files are decrypted or ownership is transferred to a recovery agent before deprovisioning user accounts.

---

## Module 18: Windows Scripting — PowerShell vs. Python

### Executive Summary

PowerShell and Python represent two distinct automation paradigms available to Windows IT practitioners. PowerShell, being native to Windows and deeply integrated with the .NET framework and Active Directory, is the preferred tool for Windows system administration and server automation. Python offers broader cross-platform applicability, richer library ecosystems, and suitability for tasks ranging from web development to data science, making it a complementary rather than competing technology in the IT toolkit.

### Technical Specifications

**Terminology**

- **Cmdlet:** PowerShell's fundamental command unit; a .NET class following the verb-noun naming convention that operates on and returns .NET objects.
- **Module:** A package of cmdlets, functions, and scripts in PowerShell (`.psm1`); equivalent in conceptual role to a Python library (`.py` package).
- **Script Block:** An anonymous, parameterizable code block in PowerShell (enclosed in `{ }`); analogous to a lambda function in Python.
- **PSScriptAnalyzer:** A static analysis linting tool for PowerShell scripts that enforces stylistic conventions and identifies common anti-patterns; integrates with VS Code.
- **Least Privilege Principle (Scripting):** The security practice of running automation scripts with the minimum privilege level required for the task, reducing the scope of potential damage from script errors or exploitation.

**Operational Logic**

1. Identify the task scope: Windows-system-specific tasks favor PowerShell; cross-platform, web, or data tasks favor Python.
2. Write the script in a `.ps1` (PowerShell) or `.py` (Python) file; adhere to established style guides.
3. Test in a controlled, non-production environment before deployment.
4. Implement error handling (`try/catch` in PowerShell, `try/except` in Python) and logging.
5. Apply version control (e.g., Git) to track changes and enable rollback.
6. For production deployment, restrict execution scope with PowerShell execution policies or Python virtual environments.

**Standard Formulas / Syntax**

PowerShell — List directory contents:

```powershell
Get-ChildItem -Path C:\Documents
```

Python — Equivalent operation:

```python
import os
print(os.listdir('C:/Documents'))
```

PowerShell — HTTP GET request:

```powershell
Invoke-WebRequest -Uri "http://example.com"
```

Python — Equivalent operation:

```python
import requests
response = requests.get("http://example.com")
print(response.text)
```

PowerShell — Create directory:

```powershell
New-Item -Path 'C:\NewFolder' -ItemType Directory
```

Python — Equivalent operation:

```python
import os
os.mkdir('C:/NewFolder')
```

### Comparative Analysis

| Feature | PowerShell | Python |
|---|---|---|
| Origin | Microsoft (.NET Framework) | Independent (Guido van Rossum, 1991) |
| Primary Domain | Windows system administration | General-purpose: web, data science, AI, automation |
| Syntax Style | Verb-noun cmdlets | English-like, whitespace-sensitive |
| Object Model | .NET objects | Native Python objects (int, str, dict, etc.) |
| Cross-Platform | PowerShell Core (limited) | Native (Windows, Linux, macOS) |
| AD Integration | Native (`ActiveDirectory` module) | Requires third-party library (`python-ldap`, etc.) |
| Performance | Slightly slower (cmdlet overhead) | Generally faster for non-Windows tasks |
| Community | Strong Windows/IT community | Vast, global, multi-domain community |
| Script Extension | `.ps1` | `.py` |

### Practical Implications

**Industrial Application:** A DevOps team uses PowerShell to automate Windows Server provisioning (AD user creation, firewall rule deployment, IIS configuration) and Python to build the CI/CD pipeline logic, REST API tests, and data transformation scripts that feed into the provisioning workflow, leveraging each language's native strengths.

**Technical Constraint:** An error in a production automation script that processes hundreds or thousands of objects simultaneously propagates the mistake at scale before it is detected. A script that incorrectly formats a `SamAccountName` for one user would apply the same malformed value to every user in the CSV. Dry-run testing (`-WhatIf` parameter in PowerShell) and input validation logic must be implemented before any bulk operation script is executed against production systems.

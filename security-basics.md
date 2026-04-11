# Security Basics

## Table of Contents
1. [The Cybersecurity Landscape](#1-the-cybersecurity-landscape)
2. [Frameworks & Career Maps](#2-frameworks--career-maps)
3. [Devices & Technologies](#3-devices--technologies)
4. [Fundamental Security Concepts](#4-fundamental-security-concepts)
5. [Common Threats](#5-common-threats)

---

## 1. The Cybersecurity Landscape

Cybersecurity is young, vast, and largely unregulated compared to fields like medicine. No single person knows everything > the key is building a mental framework to organize incoming knowledge, not mastering it all at once.

**Key mindset:** Stay humble, stay curious. There will always be someone who knows more about a specific topic. That's an opportunity, not a threat.

---

## 2. Frameworks & Career Maps

### NICE Framework (CISA / NICCS)
The **National Initiative for Cybersecurity Education** framework is the industry-standard guidebook for cybersecurity roles.

| Level | Description |
|-------|-------------|
| 7 Categories | Broad work domains (Analyse, Collect & Operate, Investigate, Operate & Maintain, Oversee & Govern, Protect & Defend, Securely Provision) |
| 32 Specialty Areas | Sub-domains within each category |
| 52 Work Roles | Specific job roles |
| Tasks / Knowledge / Skills / Abilities | Granular competencies per role |

→ Explore: [niccs.cisa.gov/workforce-development/nice-framework](https://niccs.cisa.gov/workforce-development/nice-framework)

### Map of Cybersecurity Domains (Henry Jiang)
A community-enriched visual map of every major domain in the field > from SIEM and threat intel to governance, compliance, and application security. Good for identifying blind spots.

### CISA Career Profiles
CISA-funded structured career profiles built on the NICE Framework. Each profile includes degree requirements, median salary, job growth, soft skills, and common duties.

→ Explore: [cyber.org/career-exploration/cyber-career-profiles](https://cyber.org/career-exploration/cyber-career-profiles)

---

## 3. Devices & Technologies

### Core Network Devices

| Device | Role |
|--------|------|
| **Router** | Connects multiple networks, routes traffic between them |
| **Switch** | Connects devices within a LAN, forwards to correct destination |
| **Firewall** | Monitors/filters traffic, blocks unauthorized access |
| **Modem** | Converts digital ↔ analog signals; connects home network to ISP |
| **Hub** | Legacy device, replaced by switches |
| **NAS** | Centralized network storage and file sharing |
| **Server** | Provides services: web hosting, email, databases, file sharing |

### Key Security Technologies

| Technology | Purpose |
|------------|---------|
| **Load Balancer** | Distributes traffic across nodes; helps mitigate DDoS |
| **IDS / IPS** | Intrusion Detection (detect) vs. Intrusion Prevention (block) |
| **VPN** | Encrypted tunnel over internet; note: commercial VPN providers log your data — not truly anonymous |
| **Antivirus / Antimalware** | Detects, prevents, removes malicious software |
| **Encryption** | Converts data into unreadable form; protects confidentiality in transit/at rest |
| **PKI** | Framework for secure communication via digital certificates and key pairs |
| **MFA / 2FA** | Requires 2+ verification factors to authenticate |
| **Penetration Testing** | Simulated attacks to identify real vulnerabilities |
| **SIEM** | Aggregates and analyzes security events across the environment |
| **SSL / TLS** | Encrypts client-server communication over the internet |
| **Network Monitoring / Packet Analysis** | Detects anomalies and suspicious traffic patterns |
| **Cloud Security** | Policies and controls protecting cloud-based data and infrastructure |

---

## 4. Fundamental Security Concepts

### CIA Triad

The three pillars of data security. If any one fails, there is an exploitable vulnerability.

| Pillar | Definition | Example failure |
|--------|-----------|-----------------|
| **Confidentiality** | Data only accessible to authorized parties | Unencrypted file intercepted in transit |
| **Integrity** | Data has not been modified without authorization | Patient modifies their own medical record; hashes are used to verify integrity |
| **Availability** | Data is accessible when needed | Platform returns 404 — data exists but can't be reached |

> **Hashing** is used to verify integrity. It is one-way: `ABC → 956AGTF`, but you cannot derive `ABC` from `956AGTF`.

---

### Least Privilege

> Give every entity (user, process, application) **only the access required** to do its job — nothing more.

- Mirrors the military "need-to-know" principle: limits damage from leaks, insider threats, or compromise
- Applies at every level: user accounts, application memory, database access
- Example: a developer gets dummy data, not live client records
- At the OS level: each application is sandboxed to its allocated memory (violation → `Out of Bounds Exception`)

---

### AAA — Authentication, Authorization, Accounting

| Principle | What it does |
|-----------|-------------|
| **Authentication** | Verify *who* the user is (passwords, MFA) |
| **Authorization** | Verify *what* the user is allowed to do (roles, permissions) — ties directly to Least Privilege |
| **Accounting** | Track *everything* the user does (logs, SIEM) — enables forensic analysis after an incident |

---

### Defense in Depth

Layered security — no single control is sufficient. Think: castle moat → outer walls → inner keep → garrison.

**Core idea:** multiple overlapping layers so that if one fails, others remain.

Layers can include: physical security, firewalls, IDS/IPS, malware scanners, access controls, endpoint protection, network segmentation.

**Single vendor vs. multi-vendor:**
- Single vendor → easier to manage, but one blind spot affects everything
- Multi-vendor → better coverage, higher operational overhead
- No universal right answer — context dependent

**A2AD (military concept applied to cyber):**
- *Anti-Access* → prevent the attacker from entering (DMZ, perimeter firewall, MFA, air-gap)
- *Area Denial* → make movement inside the environment as hard as possible (micro-segmentation, EDR, Zero Trust)

**Titanic parallel:** The ship's hull was trusted absolutely — no adequate secondary defenses (lifeboats). In security: **one is none, two is one.**

---

### Assume Breach

The **mindset** that complements Defense in Depth's architecture.

> Accept that no system is fully immune. Plan not just to prevent, but to **detect, contain, and recover**.

- Shifts focus from prevention-only to a full detect/respond/recover posture
- Requires: continuous monitoring, incident response plans, recovery strategies, regular drills
- **DiD** = the castle's walls | **Assume Breach** = the garrison's tactics when the walls are breached

---

### Prevent vs. Detect

Two complementary security orientations — both are necessary:

| Orientation | Focus | Examples |
|-------------|-------|---------|
| **Prevention** | Stop threats from entering/executing | Firewalls, locked doors, MFA, AV |
| **Detection** | Identify threats that got through | SIEM, cameras, EDR, log monitoring |

**Real case:** The **RUAG hack** (2014–2016) — names of Swiss special forces operators leaked because RUAG lacked proper detection systems. Prevention alone was not enough.

A zero-day exploit bypasses all prevention — you *need* detection to know something happened, and *how*.

---

### Multifactor Authentication (MFA)

Requires 2+ independent authentication factors. Factors include:

| Method | Notes |
|--------|-------|
| **SMS Token** | 6-digit code to phone; common but vulnerable to SIM-swapping |
| **Email Token** | Approval via existing trusted device; used for new device logins |
| **Biometric** | Fingerprint, Face ID; hard to forge |
| **Retina / Iris Scanner** | High-security physical environments |
| **Security Questions** | Near-obsolete; answers easily found via OSINT and social engineering |

MFA directly implements Defense in Depth at the authentication layer.

---

### Usability vs. Security

Security that users work around provides **no security**.

> If a security measure is so cumbersome that users bypass it, the bypass becomes the vulnerability.

- Example: Bob buys an unauthorized USB hub because the company laptop doesn't have enough ports → potential malware delivery vector
- Security professionals must design controls that are effective *and* usable
- HTTPS is the ideal case: adds security without degrading user experience

---

## 5. Common Threats

> Almost all cyberattacks involve at least one of: **Passwords**, **Malware**, or **Mail**.

---

### 5.1 Password Attacks

Passwords are a fundamentally human-dependent control — and humans are the weakest link.

#### Hash Cracking Methods

| Attack | How it works | Effective against |
|--------|-------------|------------------|
| **Brute Force** | Try every possible combination (0000 → 9999...) | Short, simple passwords |
| **Dictionary** | Use known common passwords (e.g., `rockyou.txt`) | Common words, patterns |
| **Rule-Based** | Dictionary + mutation rules (leet speak, capitalization, appending numbers) | "Lazy human" password patterns |
| **Rainbow Table** | Pre-computed hash lookup table for fast cracking | Unsalted hashes |

> **Salt** defeats rainbow tables by making every hash unique — forces full recomputation.

#### Other Password Attacks

**Credential Stuffing**
- Take username/password from one breach and try it everywhere else
- Works because users reuse passwords across services
- *Mitigation:* unique passwords per service + password manager

**Password Spraying**
- Try one common password (e.g., `Password123`) across many accounts
- Avoids account lockouts from single-target brute forcing
- Exploits unchanged default/first-login passwords
- *Mitigation:* enforce password change on first login; block known default passwords

**Keyloggers**
- Record every keystroke to capture credentials in plaintext
- Can be hardware (plugged into keyboard port) or software (delivered via social engineering)
- *Mitigation:* physical security, inspect peripherals, never open email attachments from unknown sources

#### Password Defense Checklist
- Long, complex passwords with special characters and numbers (not single dictionary words)
- Unique password per service
- Use a password manager
- Enable MFA everywhere
- Check breach exposure: [haveibeenpwned.com](https://haveibeenpwned.com)
- Enforce strong password policy organization-wide

---

### 5.2 Malware

> **Two universal truths about malware:**
> 1. It must be delivered somehow
> 2. It can hide — but it must run

#### Malware Types

| Type | Description |
|------|-------------|
| **Virus** | Self-replicating; attaches to clean files |
| **Worm** | Self-replicating; spreads independently without host file |
| **Trojan** | Disguised as legitimate software; executes malicious payload on activation |
| **Ransomware** | Encrypts files; demands payment for decryption key |
| **Spyware** | Covertly exfiltrates data from victim's system |
| **Adware** | Displays unwanted ads; often bundled with free software |
| **Rootkit** | Gains admin-level control while hiding from detection |
| **Keylogger** | Records keystrokes to harvest credentials |
| **Botnet** | Network of compromised machines; used for DDoS and other attacks |
| **Miner** | Hijacks host resources to mine cryptocurrency |
| **Fileless Malware** | Runs entirely in memory/registry — no traditional file footprint |
| **Dropper** | Delivers and installs a payload without carrying harmful code itself |

#### Malware Lifecycle

```
Initial Compromise → Installation → Persistence → Avoid Detection
→ Execution → Propagation → C2 Communication → Action on Objectives → Exfiltration
```

Key techniques at each stage:
- **Persistence:** registry entries, scheduled tasks, modified system files
- **Evasion:** mimicking legitimate software, encrypting traffic, disabling AV
- **C2:** connects to attacker-controlled server for commands and data exfiltration
- **Polymorphism:** alters its own code signature to evade signature-based detection

#### Delivery Vectors

| Vector | Mechanism |
|--------|-----------|
| **Phishing Email** | Most common — malicious attachment or link |
| **Malicious Website** | Drive-by download via browser vulnerability |
| **Removable Media** | Infected USB; autorun or manual execution |
| **Network Propagation** | Worms spreading via vulnerabilities — no user interaction |
| **Supply Chain** | Bundled with legitimate software or updates from unverified sources |

---

### 5.3 Mail-Based Threats & Phishing

Email is a 1970s technology that cannot be replaced — backwards compatibility preserves its security weaknesses indefinitely. Corporate email schemas (`firstname.lastname@company.com`) make targeting trivial.

#### Phishing Variants

| Type | Description |
|------|-------------|
| **Spam** | Mass unsolicited email; targets volume, not precision (e.g., fake parcel fees) |
| **Phishing** | Generic deceptive emails designed to steal credentials or deliver malware |
| **Spear Phishing** | Targeted, researched attack on a specific individual or organization |
| **Whaling** | Spear phishing targeting executives for high-value fraud |
| **Vishing** | Voice phishing (phone calls) |
| **Smishing** | SMS phishing |
| **BEC (Business Email Compromise)** | Compromises legitimate accounts to authorize fraudulent transfers |

#### Technical Delivery Methods

| Method | How it works |
|--------|-------------|
| **Malicious Attachments** | Documents or executables that execute payload on open |
| **Embedded URLs** | Links to credential-harvesting or drive-by download pages |
| **Spoofing / Impersonation** | Forged sender address mimicking trusted contact |
| **Zero-Day Exploits** | Unpatched vulnerabilities exploited before a fix exists; can trigger during HTML email rendering |

#### Spear Phishing — Attack & Defense Framework

**Attacker approach (from course exercise):**
The most effective campaigns don't look like attacks. The highest-yield method is establishing genuine trust before executing the credential capture — framing the request as a normal collaboration action (e.g., SSO login to a shared workspace), not as a suspicious link.

**Defensive countermeasures:**
- Block "sign in with work account" flows to external/unvetted platforms
- All SSO-to-external-tool requests require IT approval
- Regular audit of connected third-party apps (revoke inactive/ended clients)
- Apply least privilege — does the PM really need permanent full DB access?
- MFA everywhere (hardware keys like YubiKey for high-privilege accounts)
- DNS-level filtering to block known malicious domains
- Security awareness training — especially during high-stress windows (product launches, audits) when social engineering is most effective
- Internal simulated phishing campaigns (with non-punitive, educational follow-up)

---

## Quick Reference — Core Principles

| Principle | One-liner |
|-----------|-----------|
| **CIA Triad** | Confidentiality · Integrity · Availability |
| **Least Privilege** | Only the access needed, nothing more |
| **AAA** | Authenticate → Authorize → Account for everything |
| **Defense in Depth** | Layers of overlapping controls; one is none |
| **Assume Breach** | Plan for compromise, not just prevention |
| **Prevent vs. Detect** | Prevention stops attacks; detection catches what gets through |
| **MFA** | Multiple independent factors; implements DiD at auth layer |
| **Usability vs. Security** | Security users route around is no security at all |

---

## Key References

- [NICE Framework](https://niccs.cisa.gov/workforce-development/nice-framework)
- [Map of Cybersecurity Domains — Henry Jiang](https://www.linkedin.com/in/henryjiang/)
- [CISA Career Profiles](https://cyber.org/career-exploration/cyber-career-profiles)
- [HaveIBeenPwned](https://haveibeenpwned.com)
- [OWASP — Credential Stuffing](https://owasp.org/www-community/attacks/Credential_stuffing)
- [OWASP — Password Spraying](https://owasp.org/www-community/attacks/Password_Spraying_Attack)
- [SANS — Active Cyber Defence Cycle](https://www.sans.org/blog/know-thyself-better-than-the-adversary-ics-asset-identification-and-tracking/)
- [LoginRadius — MFA Overview](https://www.loginradius.com/blog/identity/what-is-multi-factor-authentication/)

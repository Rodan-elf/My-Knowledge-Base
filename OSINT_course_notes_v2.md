# 3080 - Open Source Intelligence and Operational Security
## Comprehensive Course Notes and Extended Reference

> This document is based on course materials and extended with additional academic knowledge, frameworks, tools, and techniques relevant to the discipline.

---

## Table of Contents

1. [OSINT Foundations](#1-osint-foundations)
2. [The Intelligence Cycle](#2-the-intelligence-cycle)
3. [Intelligence Requirements](#3-intelligence-requirements)
4. [Analytical Frameworks](#4-analytical-frameworks)
5. [Preparing an OSINT Investigation](#5-preparing-an-osint-investigation)
6. [Evidence Types and Source Validation](#6-evidence-types-and-source-validation)
7. [Collection Management](#7-collection-management)
8. [Operational Security (OPSEC)](#8-operational-security-opsec)
9. [OSINT Collection Techniques](#9-osint-collection-techniques)
   - [Search Engines and Dorking](#search-engines-and-dorking)
   - [Social Media Intelligence (SOCMINT)](#social-media-intelligence-socmint)
   - [Image and Video Intelligence (IMINT/GEOINT)](#image-and-video-intelligence-imintgeoint)
   - [Infrastructure and Network Intelligence](#infrastructure-and-network-intelligence)
   - [People and Identity Search](#people-and-identity-search)
   - [Dark Web Intelligence](#dark-web-intelligence)
   - [Real-Time and Geographic Intelligence](#real-time-and-geographic-intelligence)
   - [Threat Actor and Malware Research](#threat-actor-and-malware-research)
   - [Data Breach and Leak Intelligence](#data-breach-and-leak-intelligence)
   - [Cryptocurrency Investigation](#cryptocurrency-investigation)
10. [Reporting and Dissemination](#10-reporting-and-dissemination)
11. [Learning Resources and Communities](#11-learning-resources-and-communities)
12. [Tools and Resources Index](#12-tools-and-resources-index)

---

## 1. OSINT Foundations

### Definition

Open Source Intelligence (OSINT) is the process of identifying, collecting, and analyzing publicly available information from open sources in order to answer specific intelligence requirements. The term "open source" refers to any non-classified, publicly accessible material.

Open sources include:

- Media: newspapers, television, radio
- Publications: government reports, scientific research, public records
- Internet: websites, social media, forums
- Commercial data: market reports, subscription databases
- Gray literature: unpublished works, technical reports, conference proceedings

### OSINT in Relation to Other Intelligence Disciplines

Understanding where OSINT fits in the broader intelligence taxonomy helps define its scope and limitations:

| Discipline | Abbreviation | Source |
|-----------|-------------|--------|
| Open Source Intelligence | OSINT | Publicly available information |
| Social Media Intelligence | SOCMINT | Social platforms specifically |
| Human Intelligence | HUMINT | Human sources and informants |
| Signals Intelligence | SIGINT | Intercepted communications and signals |
| Imagery Intelligence | IMINT | Photographs and satellite imagery |
| Geospatial Intelligence | GEOINT | Geographic and location data |
| Measurement and Signature Intelligence | MASINT | Technical sensor data |
| Cyber Threat Intelligence | CTI | Threat actor TTPs, IOCs, infrastructure |

SOCMINT and GEOINT are often treated as subsets of OSINT. CTI overlaps significantly, particularly in the adversary infrastructure research domain.

### Historical Context

OSINT has existed since at least the Second World War, when intelligence units analyzed enemy newspapers and radio broadcasts. The Foreign Research and Press Service at Chatham House was an early institutional example. Over time, the volume of publicly available digital information grew dramatically, and so did the importance of OSINT.

The Russo-Ukrainian War (2022–present) brought large-scale civilian OSINT to mainstream awareness through organizations such as Bellingcat, the OSINT community on Twitter/X, and dedicated Telegram channels tracking military movements in near-real time using commercial satellite imagery, geolocated photographs, and flight tracking data.

A core distinction this course emphasizes: most content labeled "OSINT" is collected data, not intelligence. The analytical step — which transforms data into actionable assessments — is frequently omitted.

### Domains of Application

- **Cyber Security:** Technical threat intelligence, adversary infrastructure mapping, IOC enrichment, threat actor profiling.
- **Investigative Journalism:** Bellingcat (MH17, Navalny poisoning), Citizen Lab (Pegasus spyware), OCCRP (financial crime investigations).
- **Criminal and Private Investigations:** Law enforcement tracking of criminal networks; victim protection services (Intel Techniques).
- **Corporate Intelligence:** Due diligence on business partners, supply chain risk, executive protection, competitive intelligence.
- **Military and Government:** Strategic and operational intelligence support.
- **Academic and NGO Research:** Human rights documentation, conflict monitoring (e.g., ACLED, Syrian Archive).

---

## 2. The Intelligence Cycle

The intelligence cycle is a five-phase framework from the US military manual JP 2-0. It applies universally across intelligence disciplines.

### Phase 1: Planning and Direction

Define intelligence requirements, identify stakeholders, set deadlines and output formats. Never collect without a clear requirement.

### Phase 2: Collection

Develop a collection plan based on requirements. Assign sources, tools, and collectors. Define collection management procedures for larger operations.

### Phase 3: Processing and Exploitation

Transform raw collected data into a usable format. Examples: normalizing breach data into a searchable database, geolocating photographs, extracting image EXIF data, transcribing audio.

### Phase 4: Analysis and Production

The most critical phase. Activities include:

- Identifying patterns, relationships, and anomalies
- Applying structured analytic techniques to avoid cognitive bias
- Verifying source credibility and cross-referencing findings
- Writing assessments with explicit confidence levels

### Phase 5: Dissemination and Integration

Deliver intelligence to stakeholders in a format matched to their needs and clearance level. Apply TLP markings. Solicit feedback to refine future collection.

### The Feedback Loop

The cycle is not linear — feedback from dissemination continuously refines requirements and collection plans. Effective intelligence teams treat the cycle as iterative, not sequential.

---

## 3. Intelligence Requirements

### Definition

An intelligence requirement (IR) is a formally defined knowledge gap. From JP 2-0: "A requirement for intelligence to fill a gap in the command's knowledge or understanding of the operational environment or threat forces."

### Priority Intelligence Requirements (PIRs)

PIRs are the highest-priority IRs, tied directly to a specific decision. Characteristics of a well-formed PIR:

- Addresses a single, specific question
- Is tied to a named decision that must be made
- Has a defined LTIOV (Last Time Information is of Value)
- Is approved by the stakeholder, not just the analyst

Poor PIR: "What are Russian threat actors doing?"  
Strong PIR: "Has Actor X scanned our external infrastructure in the last 14 days?"

### Requests for Information (RFIs)

RFIs are submitted by consumers (e.g., SOC analysts, leadership) to the intelligence team to fill specific gaps. They differ from PIRs in that they are ad hoc rather than standing requirements.

### Best Practices

- Write requirements collaboratively with the decision-maker.
- Singularity: one question per IR.
- Clarity: avoid vague or aspirational wording.
- Timeliness: all requirements should have a deadline.
- Periodically review and retire outdated requirements.

---

## 4. Analytical Frameworks

> Added section. These frameworks are not covered in course materials but are essential for professional-level OSINT analysis, particularly in a cyber context.

### Structured Analytic Techniques (SATs)

SATs are methods designed to reduce cognitive bias in intelligence analysis. Key techniques:

- **Analysis of Competing Hypotheses (ACH):** List all plausible hypotheses. For each piece of evidence, assess whether it is consistent, inconsistent, or not applicable to each hypothesis. Select the hypothesis with the least inconsistent evidence, not the most consistent. This is critical: analysts naturally seek confirmation, not refutation.
- **Key Assumptions Check:** Explicitly list the assumptions underlying an assessment and evaluate what would change if any of them were wrong.
- **Devil's Advocacy:** Assign an analyst to build the strongest possible case against the prevailing assessment.
- **Red Team Analysis:** Adopt the perspective of an adversary to identify weaknesses in your own analysis or security posture.
- **Indicator Development:** Define specific observable events that would confirm or refute a hypothesis before collection begins.

### The Diamond Model of Intrusion Analysis

The Diamond Model (Caltagirone, Pendergast, Betz, 2013) describes every intrusion event as a relationship between four core features:

```
       Adversary
      /          \
 Capability ---- Infrastructure
      \          /
         Victim
```

- **Adversary:** The threat actor.
- **Capability:** The tools, techniques, and malware used.
- **Infrastructure:** The systems used to deliver capability (IPs, domains, C2 servers).
- **Victim:** The targeted organization or individual.

Meta-features include timestamps, phase, result, direction, methodology, and resources. The model is particularly useful for pivoting: if you identify infrastructure, you can potentially identify other victims or capabilities linked to the same adversary.

### The Cyber Kill Chain (Lockheed Martin)

The Kill Chain describes the stages of a targeted intrusion:

1. Reconnaissance
2. Weaponization
3. Delivery
4. Exploitation
5. Installation
6. Command and Control (C2)
7. Actions on Objectives

OSINT is primarily useful at stages 1 (adversary reconnaissance against you; your reconnaissance against the adversary) and 6 (identifying C2 infrastructure).

### MITRE ATT&CK

ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) is a globally accessible knowledge base of adversary behavior based on real-world observations. It is organized by:

- **Tactics:** The adversary's goal (e.g., Initial Access, Lateral Movement, Exfiltration).
- **Techniques:** How the goal is achieved (e.g., Phishing, Pass-the-Hash).
- **Sub-techniques:** More specific implementations.
- **Procedures:** Specific implementations documented for named threat groups.

For OSINT practitioners, ATT&CK is useful for:
- Identifying which TTPs a known threat actor uses, to guide collection focus.
- Mapping observed indicators to a threat actor's documented behavior.
- Understanding which techniques are used in the Reconnaissance tactic (TA0043), which maps directly to OSINT.

ATT&CK Navigator is the interactive visualization tool used for mapping threat groups to techniques. It is available at https://mitre-attack.github.io/attack-navigator/

### F3EAD Cycle (Find, Fix, Finish, Exploit, Analyze, Disseminate)

Originally a military targeting cycle, F3EAD is used in CTI for structuring threat actor pursuit:

- **Find:** Identify the threat actor or infrastructure.
- **Fix:** Confirm attribution and persistence of the target.
- **Finish:** Take action (e.g., block, report, hand off to law enforcement).
- **Exploit:** Extract intelligence from the outcome.
- **Analyze:** Derive broader insights.
- **Disseminate:** Share with stakeholders.

### PEEL Framework (for reporting)

Point, Evidence, Explanation, Link. A structured writing model that ensures every analytical claim is supported by evidence and contextualized.

---

## 5. Preparing an OSINT Investigation

### Pre-Investigation Checklist

Before any collection begins:

1. Define intelligence requirements and get them approved by the stakeholder.
2. Establish legal and ethical boundaries for the specific investigation context.
3. Set up isolated investigation infrastructure (dedicated device or VM, clean persona, VPN).
4. Initialize note-taking tools (Hunchly case, Obsidian vault).
5. Define selectors (keywords, identifiers) to track.
6. Set a collection deadline.

### Note-Taking Workflow

Good note-taking serves five functions: organization, preservation, tracking progress, building connections, and supporting reporting.

**Recommended combination: Hunchly + Obsidian**

Steps:
1. Collect and auto-capture using Hunchly.
2. Annotate each capture with context and relevance immediately.
3. Organize in Obsidian: group by theme, maintain a chronological log, link related nodes.
4. Regularly review and back up.

**Obsidian** is a local, markdown-based knowledge management tool. Key plugins relevant to OSINT:
- **Graph view:** Visualize connections between notes.
- **Dataview:** Query notes like a database.
- **Templater:** Create standardized investigation templates.
- **Kanban:** Track investigation stages as a board.

Reference: https://obsidian.md (official docs), and the Medium article "Obsidian for Threat Intelligence."

**Hunchly** (https://www.hunch.ly) is a Chrome extension for automated web evidence capture. Key features:

- Full content capture: URL, timestamp, SHA-256 hash, page content
- Selectors: automatic keyword flagging across all captured pages
- Tags: category-based page organization (define before use)
- Notes: combined text annotations and screenshots; primary report-building mechanism
- EXIF extraction from captured images
- Drag-and-drop report builder (PDF and DOCX export)
- Chain of custody tracking for evidentiary purposes

**Maltego** (https://www.maltego.com) is a graphical link-analysis tool. It uses "transforms" to automatically pull related data from connected sources (Shodan, VirusTotal, HaveIBeenPwned, etc.) given a seed entity such as an email address, IP, or domain. It is industry-standard for visualizing complex entity relationships.

**SpiderFoot** (https://github.com/smicallef/spiderfoot) is an open-source OSINT automation tool. Given a seed (IP, domain, email, username), it automatically runs hundreds of modules against public sources and produces a visual relationship graph. Available as a self-hosted web application.

**Recon-ng** (https://github.com/lanmaster53/recon-ng) is a modular web reconnaissance framework written in Python. It uses a marketplace of modules for specific tasks (DNS, social media, breach lookup, etc.) and stores results in a local SQLite database. Similar to Metasploit in interface design.

**theHarvester** (https://github.com/laramies/theHarvester) is a command-line tool for gathering emails, subdomains, hosts, employee names, and open ports from public sources including Google, Bing, LinkedIn, Shodan, and others. Essential for passive reconnaissance on a target organization.

**Zotero** (https://www.zotero.org) is a reference management tool useful for organizing research papers, reports, and source citations in longer investigations.

---

## 6. Evidence Types and Source Validation

### Types of Evidence

- **Tangible Evidence:** Concrete, verifiable material (documents, official records, videos with verified provenance). Can be authenticated and secured. Susceptible to manipulation.
- **Authoritative/Bonafide Information:** Data from verified institutional sources (government publications, academic institutions, recognized industry bodies). High inherent credibility; still requires chain-of-custody protection.
- **Testimonial Evidence:** Statements by individuals based on personal experience or expertise. Valuable for unique perspective; requires authentication of the source and corroboration.
- **Circumstantial Evidence:** Indicators that suggest rather than prove. Useful for building context; must be triangulated against other evidence types.
- **Negative Evidence:** The absence of expected information. A source that goes silent may indicate censorship, compromise, or a change in operations. Requires careful contextual analysis.

### Admiralty / NATO Reliability and Validity Scale

Source reliability (A–F):

| Rating | Meaning |
|--------|---------|
| A | Completely reliable — no doubt about authenticity, history of accuracy |
| B | Usually reliable — minor doubts, majority of the time reliable |
| C | Fairly reliable — some doubt, reliable some of the time |
| D | Not usually reliable — significant doubt about authenticity and competence |
| E | Unreliable — great doubt, history of inaccuracy |
| F | Cannot be judged — insufficient information to assess |

Information validity (1–6):

| Rating | Meaning |
|--------|---------|
| 1 | Confirmed — corroborated by independent sources, logically consistent |
| 2 | Probably true — not confirmed but logical and consistent with other information |
| 3 | Possibly true — not confirmed, reasonably logical |
| 4 | Doubtfully true — not confirmed, not illogical, but not widely believed |
| 5 | Improbable — contradicted by other information |
| 6 | Cannot be judged — no basis for evaluation |

Usage: Combine a source rating and a content rating (e.g., "B2" = usually reliable source, probably true information).

### Confidence Levels

**FBI system:**
- High: solid, multi-source or single extremely reliable source with direct evidence.
- Medium: credible sources, less direct evidence or open to interpretation.
- Low: fragmented, untested, or unverified information.

**US NIC/ODNI system:**
- High, Moderate, Low — applied to finished intelligence assessments.

**Key principle:** Confidence levels communicate the quality of the underlying intelligence, not the severity of the threat. A low-confidence assessment of a catastrophic threat is not the same as a high-confidence assessment of a minor threat.

### Traffic Light Protocol (TLP)

| Label | Sharing Scope |
|-------|--------------|
| TLP:RED | Named recipients only; do not share beyond those present |
| TLP:AMBER | Recipient organization only; may share on need-to-know basis within org |
| TLP:AMBER+STRICT | Recipient only; no further distribution even within org |
| TLP:GREEN | Community-wide; partners and peers but not public |
| TLP:CLEAR | No restrictions; publicly distributable |

TLP:AMBER+STRICT was added in TLP version 2.0 (2022). Always use the latest TLP definitions from FIRST: https://www.first.org/tlp/

### Identifying Propaganda and Unreliable Sources

Reliable sources are transparent about ownership, authorship, and methodology. Warning indicators of low-quality or propagandistic sources:

- Anonymously authored with no editorial accountability
- Emotionally charged language and frequent use of superlatives
- One-sided framing; absence of counter-evidence or alternative views
- No citations or links to primary sources
- Frequent logical fallacies (ad hominem, appeal to authority, false dichotomy)
- Recently created domain with no publication history (check via web.archive.org)

Tools for source verification:
- **Who.is / WHOIS lookup:** Domain registration date and registrant.
- **web.archive.org (Wayback Machine):** Historical versions of a website.
- **AllSides / Ad Fontes Media:** Media bias ratings for news outlets.
- **NewsGuard:** Browser extension rating news site credibility.

### Cognitive Biases in Intelligence Analysis

Analysts must actively manage:

- **Confirmation bias:** Seeking evidence that supports existing beliefs.
- **Anchoring bias:** Over-weighting the first piece of information received.
- **Availability heuristic:** Overestimating the probability of events that are easy to recall.
- **Groupthink:** Suppressing dissenting views to maintain consensus.
- **Mirror imaging:** Assuming the adversary thinks and acts like you do.

The remedy is systematic use of SATs (see Section 4) and explicit documentation of assumptions.

---

## 7. Collection Management

### Core Process

1. Requirements identification and validation.
2. Collection planning: assets, methods, timeline.
3. Asset allocation: personnel, tools, platforms.
4. Team coordination and tasking.
5. Processing and exploitation of collected data.
6. Dissemination to stakeholders.
7. Feedback collection and plan revision.

### Collection Assets

A collection asset is any system, platform, or capability used to gather intelligence. Assets must be matched to requirements: not every tool is appropriate for every task. The principle of asset economy requires using the least invasive and most efficient asset for each requirement.

### Multidisciplinary Collection

No single source should be the sole basis for an assessment. Cross-validate across:
- OSINT sources (web, social media, public records)
- Internal telemetry (if in a corporate context)
- Threat intelligence feeds
- HUMINT (subject matter experts, vendor briefings)

### Collection Planning Templates

Effective collection plans document:

| Field | Content |
|-------|---------|
| IR reference | Unique IR identifier |
| Requirement text | The exact question to be answered |
| LTIOV | Deadline for the intelligence |
| Priority | High / Medium / Low |
| Collection method | Which tool, platform, or technique |
| Assigned analyst | Who is responsible |
| Status | Pending / In progress / Complete |
| Output | Where findings are documented |

---

## 8. Operational Security (OPSEC)

> Warning: This module is for educational purposes only. Real-world operational security against sophisticated adversaries requires significantly more than what is covered here.

### OPSEC Fundamentals

OPSEC is the process of protecting your own information and methods from adversarial detection. Before any collection:

- Who am I trying to conceal information from?
- What information am I protecting?
- How would an adversary access this information?
- What countermeasures prevent that access?

Core principle: if you do not know your threat, you do not know what to protect.

### Device and Environment Isolation

- Use dedicated hardware for intelligence operations, never connected to production or corporate networks.
- Boot from a live OS (Tails) or maintain a clean virtual machine per persona/operation.
- Full-disk encryption on all operational devices.
- Physically separate devices from personal hardware.

**Recommended isolated environments:**

- **Tails OS** (https://tails.boum.org): Amnesic live operating system that routes all traffic through Tor. Leaves no trace on the host machine. Recommended for highest-sensitivity operations.
- **Whonix** (https://www.whonix.org): Two-VM architecture (Gateway + Workstation) where all traffic is forced through Tor. Suitable for persistent investigative environments.
- **Kali Linux** (https://www.kali.org): Debian-based penetration testing distribution. Useful for technical OSINT due to pre-installed tooling.
- **VirtualBox / VMware** (https://portableapps.com/download): Standard virtualization for isolated workstation environments.
- **Tracelabs OSINT VM:** A purpose-built OSINT virtual machine provided by Tracelabs for their CTF competitions. Pre-loaded with common OSINT tools.

### Persona Creation

A persona is a consistent fictional identity used for passive collection on public platforms.

**DO NOT include in a persona:**
- Any element of your real identity
- Consistent login timestamps
- Images with unstripped EXIF data
- Native language special characters
- Real interests, hobbies, or professional background

**DO include in a persona:**
- Internally consistent backstory: claimed location, profession, interests
- Behavioral consistency: same posting cadence, writing style
- Geolocation-consistent details (local slang, references to local events)
- Deliberately introduced spelling/grammar errors consistent with the backstory

**OPSEC levels:**
- Persona 1 (low risk): same browser, same extensions, consistent VPN endpoint, consistent behavioral patterns.
- Persona 2 (high risk): separate browser, different extensions, different VPN country, separate VM or environment, distinct language patterns, separate accounts, separate avatars and handles.

**Persona generation tools:**

| Tool | URL | Purpose |
|------|-----|---------|
| This Person Does Not Exist | https://thispersondoesnotexist.com/ | AI-generated face images |
| Randus | https://randus.org/ | Random personality generator |
| Random Data Tools | https://randomdatatools.ru/ | Russian-language identity generator |
| Rangen Appearance | https://www.rangen.co.uk/chars/appgen.php | Character appearance |
| Rangen Quick Character | https://www.rangen.co.uk/chars/quickchargen.php | Quick character profile |
| Rangen Personality | https://www.rangen.co.uk/chars/pergen.php | Personality profile |
| Rangen Motive | https://www.rangen.co.uk/chars/motivegen.php | Character motivation |
| Random Character | https://random-character.com/ | Full character with backstory |
| Fake Name Generator | https://www.fakenamegenerator.com/ | Complete identity profile with address, DOB, etc. |

**Disposable communication:**
- Anonymous email: ProtonMail, Tutanota, Guerrilla Mail, Mailnull, EmailDeck
- Disposable SMS: receive-sms.com, sms-activate.org, SMS-Get, SMSReceiveFree

### Browser Configuration

**Recommended setup:**

- Firefox with Multi-Account Containers: isolates cookies, cache, and browsing history per container.
- Assign each container to a persona or operational context.
- Pair each container with a specific VPN endpoint.
- Use the same user agent consistently per container/persona.

**Privacy extensions (from course + additional):**

| Extension | Purpose |
|-----------|---------|
| uBlock Origin | Ad and tracker blocking |
| Privacy Badger (EFF) | Automatic tracker learning and blocking |
| HTTPS Everywhere | Force HTTPS on supported sites |
| WebRTC Control / Leak Shield | Prevent WebRTC IP leaks |
| Canvas Defender | Canvas fingerprint noise injection |
| User-Agent Switcher | Spoof browser identity |
| Location Guard / Vytal | Spoof geolocation and timezone |
| Firefox Multi-Account Containers | Session isolation per persona |

**WebRTC leak prevention:**
- Firefox: `about:config` → set `media.peerconnection.enabled` to `false`
- Chrome: use WebRTC Control extension
- Edge: `about:flags` → enable "Hide my local IP address over WebRTC connections"

**VPN considerations:**
- Mullvad VPN integrates natively with Firefox containers.
- For country-specific needs not covered by your VPN: ProtonVPN, IVPN, and Windscribe offer broad country coverage.
- Always verify VPN is working before operational browsing.

### Anonymity Verification Tools

Run before and after configuring privacy measures. Test without protection first (baseline), then with full protection active.

| Tool | URL | What It Checks |
|------|-----|---------------|
| Am I Unique | https://amiunique.org/fp | Browser fingerprint uniqueness |
| ProIPTest | http://proiptest.com/test/ | IP address, proxy headers, VPN detection |
| Proxy6 Privacy Check | https://proxy6.net/privacy | Anonymity and IP leak check |
| Cover Your Tracks (EFF) | https://coveryourtracks.eff.org | Fingerprinting and tracking test |
| BrowserLeaks | https://browserleaks.com | WebRTC, canvas, fonts, JS, CSS leaks |
| IPLeak | https://ipleak.net | DNS and IP leak test |
| DNS Leak Test | https://www.dnsleaktest.com | DNS provider verification |
| Whoer | https://whoer.net | Comprehensive anonymity score |

---

## 9. OSINT Collection Techniques

### Search Engines and Dorking

#### Google Dorking (Google Hacking)

Google advanced operators allow highly targeted searches. Key operators:

| Operator | Function | Example |
|----------|---------|---------|
| `site:` | Restrict to a domain | `site:gov.ch filetype:pdf` |
| `filetype:` | Search by file extension | `filetype:xlsx email` |
| `intitle:` | Search page title | `intitle:"index of"` |
| `inurl:` | Search URL string | `inurl:admin login` |
| `intext:` | Search page body text | `intext:"confidential" site:pastebin.com` |
| `cache:` | View cached version | `cache:example.com` |
| `link:` | Pages linking to a URL | (limited in modern Google) |
| `"exact phrase"` | Exact match | `"John Smith" "CIA"` |
| `-term` | Exclude term | `OSINT -tools` |
| `OR` | Boolean OR | `OSINT OR intelligence` |
| `*` | Wildcard | `"John * Smith"` |

**High-value dork combinations:**

```
# Find exposed login portals
intitle:"login" inurl:/admin site:example.com

# Find documents with classification markings
"SECRET//NOFORN" ext:pdf

# Find exposed configuration files
ext:env "DB_PASSWORD"

# Find exposed camera streams
intitle:"webcamXP 5" inurl:8080

# Find exposed Excel files with email addresses
filetype:xlsx intext:"@gmail.com" site:example.org

# FortiGate VPN portals
inurl:".php?id=" "You have an error in your SQL syntax"

# Find RDP files
"screen mode id:" ext:rdp
```

**The OSINT Framework** (https://osintframework.com): A community-maintained mind-map of OSINT tools organized by category (usernames, email, domain, IP, social networks, etc.). An essential reference for finding the right tool for any specific data type.

#### Yandex

Leading Russian search engine. Use the `lr` URL parameter to filter by geographic region. Yandex has its own dork operators similar to Google. Essential for Russian-language sources, Russian social media profiles, and content not indexed by Western engines. Yandex image search also performs more aggressive reverse image search than Google.

#### Other Search Engines

- **Bing:** Different index than Google; sometimes surfaces content Google does not. Use `ip:` operator to find sites on a specific IP.
- **Baidu:** For Chinese-language content.
- **Shodan** (https://shodan.io): Searches internet-connected devices rather than web pages. See Infrastructure section.
- **Censys** (https://search.censys.io): Certificate and device search.
- **FOFA** (https://fofa.info): Chinese-origin internet asset search engine. Strong for finding infrastructure in Asia-Pacific.
- **ZoomEye** (https://www.zoomeye.org): Another Chinese-origin device and service search engine.
- **Grep.app** (https://grep.app): Search across public GitHub repositories using regex.
- **PublicWWW** (https://publicwww.com): Search website source code for specific strings, technologies, and analytics IDs.

#### Paste Site Search

Paste sites are frequently used for data dumps, credential leaks, and covert communication:

- Pastebin: https://pastebin.com
- GitHub Gists: https://gist.github.com
- Hastebin, Ghostbin, Rentry.co
- Pastehunter (GitHub): Monitors paste sites for keywords in near-real time.

Google dork for paste sites: `site:pastebin.com "target@domain.com"`

---

### Social Media Intelligence (SOCMINT)

#### LinkedIn

LinkedIn is the richest source of professional intelligence. Key techniques from course materials plus additions:

**Search operators:**
```
site:linkedin.com "FIRSTNAME LASTNAME"
site:linkedin.com/in "COMPANYNAME" "Chief Information Security Officer"
ctitle:CISO ccompany:TARGET
interest:hacking school:ETH
ctitle:intelligence (threat OR cyber OR Hunt OR Detect)
```

Advanced search tool reference: http://recruitmentgeek.com/tools/linkedin/

**Additional techniques:**
- Use InSpy (https://github.com/leapsecurity/InSpy) for automated LinkedIn employee enumeration by company.
- Cross-reference LinkedIn profiles against GitHub, Twitter/X, and company directories to build complete profiles.

#### Facebook

Facebook directories (note: availability changes):
- https://www.facebook.com/directory/people
- https://www.facebook.com/directory/places
- https://www.facebook.com/directory/groups
- https://www.facebook.com/pages/category/work-position/
- https://www.facebook.com/directory/marketplace

**Additional techniques:**
- Search `site:facebook.com "NAME" "CITY"` to find profiles without a Facebook account.
- Lookup a Facebook profile ID by inspecting page source for `profile_id` or using the URL format `facebook.com/profile.php?id=XXXXXXX`.

#### Instagram

- **Osintgram** (https://github.com/Datalux/Osintgram): Command-line tool for extracting public Instagram data.
- **InstaLoader** (https://github.com/instaloader/instaloader): Download profiles, stories, metadata, and geotags.
- Search via Google: `site:instagram.com "USERNAME"`
- Examine geotags on posts and cross-reference coordinates.

#### Telegram

Google dork operators for Telegram:
```
site:telegra.ph russian_osint
site:t.me/joinchat/
site:t.me/addstickers/
inurl: hack site:telegram.me
site:telemetr.me OR site:tgstat.ru OR site:telegram.im
site:comments.bot OR site:c01.comments.bot
```

Tools:
- https://search.buzz.im/ — search messages in open Telegram chats
- https://lyzem.com/ — channel, group, bot, and message search
- https://telegramdb.org/ — searchable Telegram channel/group database
- https://github.com/ItIsMeCall911/Awesome-Telegram-OSINT — comprehensive resource list

#### Twitter / X

- **BirdHunt** (https://birdhunt.co): Search tweets by keyword and geolocation.
- **Social Bearing** (https://socialbearing.com): Twitter analytics and sentiment.
- **Twint** (https://github.com/twintproject/twint): Open-source Twitter scraping tool (note: API changes have affected functionality; verify current status).
- Advanced Twitter search: https://twitter.com/search-advanced — filter by date, location, language, account.
- **Kribrum.io** (https://kribrum.io): Russian-language social media monitoring.

#### Reddit

- **Pushshift** (note: availability has been disrupted by Reddit API changes): Historical Reddit data including deleted posts and comments.
- **Reddit Search** via Google: `site:reddit.com "username" OR "topic"`
- **Camas Reddit Search** (if available): Archive-based search for deleted content.
- **Unddit / Reveddit**: Retrieve deleted Reddit comments and posts by username or subreddit.

#### TikTok

- Search via Google: `site:tiktok.com "username"`
- **Exported data requests:** TikTok's privacy portal allows data export requests.
- Analyze hashtags and video metadata for geolocation and behavioral patterns.

#### Discord

- Directory-based server discovery using Google dorks with `site:discord.gg`
- **Disboard** (https://disboard.org): Public Discord server directory
- **DiscordHub** (https://discordhub.com): Another server listing
- **DISINT** (https://github.com/Dutchosintguy/DISINT): OSINT tool for Discord

#### Username Cross-Platform Tracking

| Tool | URL |
|------|-----|
| Namechk | https://namechk.com |
| WhatsMyName | https://whatsmyname.app |
| KnowEm | https://knowem.com |
| Sherlock (CLI) | https://github.com/sherlock-project/sherlock |
| Maigret (CLI) | https://github.com/soxoj/maigret |
| Holehe (CLI) | https://github.com/megadose/holehe |

**Sherlock** is a command-line Python tool that checks username availability across 300+ social networks simultaneously and produces a report with direct profile links.

**Maigret** is a more advanced fork of Sherlock with additional sites and the ability to collect profile information beyond just existence checks.

**Holehe** checks whether an email address is registered on a large number of websites without triggering password resets, by exploiting "forgot password" functionality.

---

### Image and Video Intelligence (IMINT/GEOINT)

> This is a significantly expanded section not covered in depth in the course materials.

#### Reverse Image Search

| Tool | URL | Strength |
|------|-----|---------|
| Google Images | https://images.google.com | Broad web index |
| Yandex Images | https://yandex.com/images | Superior facial recognition, Russian social media |
| TinEye | https://tineye.com | Chronological results; useful for finding original image |
| Bing Visual Search | https://www.bing.com/visualsearch | Microsoft-indexed content |
| Search4Faces | https://search4faces.com | VK, TikTok, Instagram, Clubhouse face search |
| PimEyes | https://pimeyes.com | Commercial face search engine (paid tiers) |

**Workflow recommendation:** Run images through Google, Yandex, and TinEye simultaneously. Yandex frequently finds results the others miss, especially for content originating from Russian-language platforms.

#### EXIF and Metadata Extraction

Images captured by smartphones and cameras contain EXIF metadata which can include GPS coordinates, device model, timestamp, and software version. This metadata is often stripped by social media platforms, but may survive in images shared via email, file hosting, or direct transfer.

| Tool | URL / Method |
|------|-------------|
| ExifTool | https://exiftool.org (CLI) |
| Jeffrey's Exif Viewer | http://exif.regex.info/exif.cgi |
| Jimpl | https://jimpl.com |
| PhotoOSINT | Browser extension (from course) |
| Hunchly | Automatically extracts EXIF from all captured images |

#### Geolocation from Images

Geolocating an image without embedded GPS metadata requires analysis of visual cues:

- **Architectural style and signage:** Language, script, building materials.
- **Vegetation:** Climate zone, seasonal indicators.
- **Infrastructure:** Road markings, power lines, vehicle types.
- **Sun position and shadow analysis:** Using SunCalc (https://suncalc.org) and known timestamp to establish photographer's latitude/approximate location.
- **Commercial satellite imagery cross-reference:** Google Maps, Google Earth Pro, Bing Maps Bird's Eye, Apple Maps.
- **Street-level verification:** Google Street View (https://www.google.com/streetview), Mapillary (https://www.mapillary.com), Yandex Panorama.

**Tools:**
- **SunCalc** (https://suncalc.org): Calculate sun position and shadow direction for a given time and location.
- **GeoSpy AI** (https://geospy.ai): AI-based geolocation from images (experimental accuracy).
- **PeakFinder** (https://www.peakfinder.org): Identify mountain silhouettes from photographs.
- **Google Earth Pro** (https://www.google.com/earth/about/versions/): Desktop application with historical satellite imagery.

#### Satellite Imagery

| Source | URL | Notes |
|--------|-----|-------|
| Google Earth / Maps | https://earth.google.com | Historical imagery; Street View |
| Sentinel Hub | https://www.sentinel-hub.com | ESA Copernicus satellite data; free tier |
| Planet Labs | https://www.planet.com | Commercial; high frequency revisit rate |
| NASA Worldview | https://worldview.earthdata.nasa.gov | Free; multi-band analysis |
| Maxar | https://www.maxar.com | Commercial high-resolution imagery |
| ESRI World Imagery | https://www.arcgis.com | ArcGIS satellite layer |
| Zoom.earth | https://zoom.earth | Near-real-time satellite and weather |

For conflict zone monitoring, Sentinel Hub combined with the EO Browser is a standard free tool for change detection over time.

#### Video Verification

Key techniques for verifying video content:
- Extract keyframes using ffmpeg for reverse image searching.
- Cross-reference landmarks visible in footage against satellite imagery.
- Analyze metadata with ExifTool if the file is unprocessed.
- Check for compression artifacts and inconsistencies that may indicate manipulation.
- **InVID / WeVerify** (https://weverify.eu/verification-plugin/): Browser plugin for video verification; checks metadata, runs reverse image search on keyframes, queries fact-checking databases.
- **Amnesty International YouTube DataViewer** (https://citizenevidence.amnestyusa.org): Extracts thumbnails and upload time from YouTube videos for reverse image search.

---

### Infrastructure and Network Intelligence

#### DNS Intelligence

DNS records reveal infrastructure relationships: A records link domains to IPs; MX records identify email providers; NS records identify registrars; TXT records may reveal SPF, DKIM, and DMARC configurations.

| Tool | URL | Purpose |
|------|-----|---------|
| DNSDumpster | https://dnsdumpster.com | DNS record enumeration and visualization |
| ViewDNS.info | https://viewdns.info | Comprehensive DNS and IP tools |
| MXToolbox | https://mxtoolbox.com | DNS, MX, blacklist, and email header analysis |
| SecurityTrails | https://securitytrails.com | Historical DNS and WHOIS data (free tier) |
| PassiveTotal / RiskIQ | https://community.riskiq.com | Passive DNS, WHOIS history, certificate data |
| Robtex | https://www.robtex.com | DNS lookup and reverse DNS |
| HackerTarget | https://hackertarget.com | DNS recon, reverse IP, and port scanning |
| DNSViz | https://dnsviz.net | Visual DNSSEC analysis |

#### WHOIS and Registration Data

WHOIS data reveals domain registrant information, registration dates, and registrars. Privacy services now mask most personal data, but historical WHOIS records (before GDPR) are often preserved in passive databases.

```bash
# CLI lookup
whois example.com

# With ARIN for IP ranges
whois -h whois.arin.net 1.2.3.4
```

| Tool | URL |
|------|-----|
| ICANN Lookup | https://lookup.icann.org |
| WhoisXML API | https://whois.whoisxmlapi.com |
| DomainTools | https://whois.domaintools.com (paid for history) |
| SecurityTrails | https://securitytrails.com |

#### Certificate Transparency (CT) Logs

Every TLS certificate issued must be logged in public CT logs. This creates a searchable record of all domains and subdomains that have ever had a certificate issued for them — an extremely powerful subdomain enumeration method.

| Tool | URL |
|------|-----|
| crt.sh | https://crt.sh |
| Censys Certificates | https://search.censys.io/certificates |
| Facebook CT Monitoring | https://developers.facebook.com/tools/ct/ |

Example query on crt.sh to find all subdomains: `%.example.com`

#### Internet-Connected Device Search (Shodan, Censys, FOFA)

**Shodan** (https://shodan.io) indexes banners returned by internet-facing services. It can find exposed cameras, industrial control systems, routers, databases, and any service with a detectable banner.

Key Shodan dorks:
```
# Find MongoDB instances with no authentication
product:"MongoDB" -authentication

# Find default Cisco credentials
"default password" cisco

# Find RDP services
port:3389 product:"Remote Desktop Protocol"

# Find Elasticsearch instances
product:"Elastic"

# Find specific organization's infrastructure
org:"TARGET COMPANY"

# Find ICS/SCADA
port:102 siemens

# Shodan browser extension
# Shows hosting info, open ports, and CVEs for any site you visit
```

**Censys** (https://search.censys.io): Similar to Shodan but with stronger certificate data integration. Excellent for mapping an organization's internet-facing infrastructure using certificate common names.

**FOFA** (https://fofa.info): Chinese-origin internet asset search. Strong coverage of Asia-Pacific infrastructure.

**ZoomEye** (https://www.zoomeye.org): Another Chinese-origin device search engine.

**GreyNoise** (https://www.greynoise.io): Identifies IPs that are mass-scanning the internet. Useful for filtering noise from threat intelligence feeds and identifying scanning campaigns.

**Onyphe** (https://www.onyphe.io): French cyber defense intelligence platform combining passive DNS, Shodan-style scanning, and threat intelligence.

#### BGP and ASN Research

Autonomous System Numbers (ASNs) identify blocks of IP addresses owned by an organization. Understanding ASN structure helps map an adversary's or target's complete IP footprint.

| Tool | URL |
|------|-----|
| BGP.he.net | https://bgp.he.net |
| ARIN / RIPE / APNIC | Regional Internet Registries |
| ASRank | https://asrank.caida.org |
| IPinfo ASN data | https://ipinfo.io |
| BGPView | https://bgpview.io |

#### Email Header Analysis

Email headers reveal routing information, originating IP addresses, and authentication results (SPF, DKIM, DMARC).

| Tool | URL |
|------|-----|
| MXToolbox Header Analyzer | https://mxtoolbox.com/EmailHeaders.aspx |
| Google Admin Toolbox | https://toolbox.googleapps.com/apps/messageheader/ |
| Mail Header Analyzer | https://mailheader.org |

#### Email Intelligence

| Tool | URL | Purpose |
|------|-----|---------|
| Hunter.io | https://hunter.io | Find email addresses for a domain; verify format |
| Phonebook.cz | https://phonebook.cz | Email, domain, and URL intelligence |
| Clearbit Connect | https://connect.clearbit.com | Email lookup via LinkedIn/company |
| Holehe | https://github.com/megadose/holehe | Check email registration across services |
| Kickbox | https://kickbox.com | Disposable email detection |
| EmailRep | https://emailrep.io | Email reputation and intelligence |
| Have I Been Pwned | https://haveibeenpwned.com | Breach notification for email addresses |

---

### People and Identity Search

#### Public Records and People Engines

| Tool | URL | Notes |
|------|-----|-------|
| WebMii | https://webmii.com | Aggregates social, web, and document presence |
| Pipl | https://pipl.com | Deep people search (paid professional tool) |
| Spokeo | https://spokeo.com | US-focused people search |
| Intelius | https://www.intelius.com | US people and background search |
| BeenVerified | https://www.beenverified.com | US public records aggregation |
| TruePeopleSearch | https://www.truepeoplesearch.com | Free US people search |
| Quant | https://quant.com | Less-filtered search engine |
| Clubhouse DB | http://clubhousedb.com | Clubhouse profile search |

#### Phone Number Intelligence

| Tool | URL |
|------|-----|
| Truecaller | https://www.truecaller.com |
| Sync.me | https://sync.me |
| NumLookup | https://www.numlookup.com |
| PhoneInfoga | https://github.com/sundowndev/phoneinfoga (CLI) |

**PhoneInfoga** is an open-source OSINT framework for phone numbers. It collects information from various sources including Numverify, Google, and TrueCaller.

---

### Dark Web Intelligence

#### The Tor Network

The Tor (The Onion Router) network routes traffic through a series of relays, providing anonymity for both users and hidden services (.onion addresses). Accessing .onion sites requires the Tor Browser (https://www.torproject.org) or a Tor-enabled environment.

Key considerations:
- Never access the dark web from a non-isolated environment.
- Use Tails OS or Whonix for operational dark web collection.
- Many .onion sites are offline or migrate frequently.

#### TOR Networking and Analysis Tools

| Tool | URL | Purpose |
|------|-----|---------|
| Tor Project | https://www.torproject.org | Official Tor browser and documentation |
| TOR Exit Nodes | https://check.torproject.org/torbulkexitlist | Full list of active exit nodes |
| ExoneraTor | https://metrics.torproject.org/exonerator.html | Check if an IP was a Tor relay at a given time |
| TorWHOIS | torwhois.com | Lookup .onion address information |
| Ahmia Link Graph | https://ahmia.fi | Onion domain zone mapping |
| D3 TOR Relay Node Map | https://torflow.uncharted.software | Global relay node visualization |

#### Dark Web Search Engines

| Tool | URL / Access |
|------|-------------|
| Ahmia | https://ahmia.fi (clearnet), also via Tor |
| OnionLand Search | (onion address, accessible via Tor) |
| Dargle | (onion) — dark web domain aggregation |
| Haystack | (I2P network) — hidden service discovery |
| DarkOwl | https://darkowl.com (commercial, paid) |

#### Open-Source Dark Web Tools (GitHub)

| Tool | Repository |
|------|-----------|
| OnionSearch | https://github.com/megadose/OnionSearch |
| Darkdump | https://github.com/josh0xA/darkdump |
| Ahmia search engine | https://github.com/ahmia/ahmia-site |
| DarkSearch | https://github.com/thehappydinoa/DarkSearch |
| Katana | https://github.com/adnane-X-tebbaa/Katana |
| Onioff (scanner) | https://github.com/k4m4/onioff |
| Onionscan | https://github.com/s-rah/onionscan |
| Onion-nmap | https://github.com/milesrichardson/docker-onion-nmap |
| TorBot | https://github.com/DedSecInside/TorBot |
| TorCrawl | https://github.com/MikeMeliz/TorCrawl.py |
| VigilantOnion | https://github.com/andreyglauzer/VigilantOnion |
| OnionIngestor | https://github.com/danieleperera/OnionIngestor |
| DeepDarkCTI | https://github.com/fastfire/deepdarkCTI |

#### Google Dork Onion Searches

Access onion content via Google by targeting known onion-to-clearweb gateways:
```
(site:onion.link | site:onion.cab | site:tor2web.org | site:onion.sh | site:tor2web.fi | site:onion.direct)
```

---

### Real-Time and Geographic Intelligence

#### Aviation Tracking

| Tool | URL | Notes |
|------|-----|-------|
| LiveATC | https://www.liveatc.net | Live ATC audio feeds worldwide |
| ADS-B Exchange | https://globe.adsbexchange.com | Unfiltered global aircraft tracking (does not honor military/government exclusion requests) |
| Flightradar24 | https://www.flightradar24.com | Commercial; filtered; real-time tracking |
| FlightAware | https://www.flightaware.com | US-strong; historical data |
| OpenSky Network | https://opensky-network.org | Research-grade ADS-B data; API available |
| globe.specschange.com | https://globe.specschange.com | From course materials |

Note: ADS-B Exchange is preferred for intelligence work because it does not filter out military or government aircraft that have requested exclusion from other services.

#### Maritime Tracking

| Tool | URL |
|------|-----|
| MarineTraffic | https://www.marinetraffic.com |
| VesselFinder | https://www.vesselfinder.com |
| Global Fishing Watch | https://globalfishingwatch.org |

#### Incident and Conflict Mapping

| Tool | URL | Purpose |
|------|-----|---------|
| Global Incident Map | https://www.globalincidentmap.com | Real-time worldwide incident categories |
| CFR Global Conflict Tracker | https://www.cfr.org/global-conflict-tracker | Ongoing conflicts with analysis |
| Live UA Map | https://liveuamap.com | Aggregated real-time event map |
| ACLED | https://acleddata.com | Armed Conflict Location and Event Data |
| Crisis Map (UNHCR/UNOCHA) | https://data2.unhcr.org/en/situations | Humanitarian situation maps |
| Bellingcat's Ukraine Map | https://ukraine.bellingcat.com | Verified Ukraine conflict events |

#### Wireless Network Intelligence

- **Wigle.net** (https://wigle.net): Global database of wireless access points with GPS coordinates. Useful for physical location confirmation and infrastructure mapping.

---

### Threat Actor and Malware Research

#### APT Tracking and Threat Group Databases

| Tool | URL |
|------|-----|
| APT Threat Tracking | https://apt.threattracking.com |
| APT Securelist (Kaspersky) | https://apt.securelist.com |
| MITRE ATT&CK Groups | https://attack.mitre.org/groups/ |
| ThaiCERT Threat Encyclopedia | https://www.thaicert.or.th/pages/threat-intel/ |
| Malpedia | https://malpedia.caad.fkie.fraunhofer.de |
| APTNotes | https://github.com/kbandla/APTnotes |

#### Threat Intelligence Platforms and Enrichment

| Tool | URL | Purpose |
|------|-----|---------|
| ThreatMiner | https://www.threatminer.org | Multi-source threat intelligence lookups |
| VirusTotal | https://www.virustotal.com/en/ | Multi-engine file, URL, hash, domain analysis |
| AlienVault OTX | https://otx.alienvault.com | Open threat exchange; community IOC sharing |
| MISP | https://www.misp-project.org | Open-source threat intelligence sharing platform (self-hosted) |
| IBM X-Force Exchange | https://exchange.xforce.ibmcloud.com | IBM threat intelligence portal |
| Pulsedive | https://pulsedive.com | IOC enrichment and threat intelligence |
| ThreatCrowd | https://www.threatcrowd.org | Domain, IP, email, and malware search |
| Cisco Talos | https://talosintelligence.com | Cisco threat intelligence and reputation |
| URLScan.io | https://urlscan.io | Analyze and sandbox URLs; screenshot and DOM capture |
| AbuseIPDB | https://www.abuseipdb.com | Community IP abuse reporting and lookup |
| Spamhaus | https://www.spamhaus.org | IP and domain reputation blocklists |

#### Sandboxes and Malware Analysis

| Tool | URL |
|------|-----|
| Any.run | https://any.run |
| Hybrid Analysis | https://www.hybrid-analysis.com |
| Cuckoo Sandbox | https://cuckoo.cert.ee |
| Joe Sandbox | https://www.joesandbox.com |
| Triage (Hatching) | https://tria.ge |
| Checkpoint ThreatPortal | https://threatpoint.checkpoint.com/ThreatPortal/emulation |
| CPCheckMe | http://www.cpcheckme.com/checkme |

#### Online Antivirus Scanners

| Tool | URL |
|------|-----|
| VirusTotal | https://www.virustotal.com/en/ |
| Dr.Web Online | https://online.drweb.com/ |
| Kaspersky OpenTIP | https://opentip.kaspersky.com/ |
| ESET Online Scanner | https://www.esetnod32.ru/home/products/online-scanner/ |
| MetaDefender | https://metadefender.opswat.com |

#### Ransomware Intelligence

| Tool | URL |
|------|-----|
| Ransomwatch | https://ransomwatch.telemetry.ltd |
| ID Ransomware | https://id-ransomware.malwarehunterteam.com |
| The No More Ransom Project | https://www.nomoreransom.org |
| Ransomlook | https://www.ransomlook.io |

---

### Data Breach and Leak Intelligence

| Tool | URL | Notes |
|------|-----|-------|
| Have I Been Pwned | https://haveibeenpwned.com | Standard breach notification |
| IntelX | https://intelx.io | Leaked data search: email, username, domain, phone |
| LeakCheck | https://leakcheck.io | 7B+ record breach database |
| Breach Directory | https://breachdirectory.org | Cross-breach search |
| DeHashed | https://dehashed.com | Comprehensive breach search (paid) |
| Snusbase | https://snusbase.com | Breach data search |
| Leak-Lookup | https://leak-lookup.com | Username, email, IP breach lookup |
| GhostProject | https://ghostproject.fr | Breach search focused on password pairs |

For bulk email validation and breach checking in corporate investigations, Have I Been Pwned's API is the industry standard. HIBP also maintains a Pwned Passwords list of over 800 million compromised password hashes, available for offline lookup.

---

### Cryptocurrency Investigation

#### Blockchain Explorers

| Tool | URL | Coverage |
|------|-----|---------|
| Blockchain.com | https://blockchain.com | BTC |
| Blockchair | https://blockchair.com | BTC, ETH, XRP, BCH, LTC, XLM, DASH, ZEC, XMR, TON |
| Etherscan | https://etherscan.io | ETH and ERC-20 tokens |
| BscScan | https://bscscan.com | Binance Smart Chain |
| Solscan | https://solscan.io | Solana |
| Mintscan | https://www.mintscan.io | Cosmos ecosystem |

#### Visualization and Analytics

| Tool | URL | Purpose |
|------|-----|---------|
| Breadcrumbs | https://www.breadcrumbs.app | Blockchain transaction visualization |
| Blockpath | https://blockpath.com | Bitcoin transaction path visualization |
| OXT | https://oxt.me | Bitcoin analytics and visualization |
| Graphsense | https://graphsense.info | Open-source cryptocurrency analytics |
| Ethtective | https://ethtective.com | Ethereum transaction visualization |
| Chainalysis Reactor | https://www.chainalysis.com | Commercial (law enforcement standard) |
| Elliptic | https://www.elliptic.co | Commercial blockchain analytics |

#### Abuse and Fraud Detection

| Tool | URL |
|------|-----|
| BitcoinAbuse | https://www.bitcoinabuse.com |
| Bitcoinwhoswho | https://bitcoinwhoswho.com |
| CheckBitcoinAddress | https://checkbitcoinaddress.com |
| Scamalert | https://scamalert.sg |
| Cryptscam | https://cryptscam.com |

#### Methodology for Crypto Investigation

1. Identify seed address from leaked data, ransom note, or blockchain reference.
2. Use a block explorer to trace transaction history.
3. Use a visualization tool (Breadcrumbs, OXT) to follow fund flows.
4. Apply clustering algorithms or commercial tools to group related addresses.
5. Cross-reference with exchange deposit addresses for potential de-anonymization.
6. Check abuse databases for reported fraud activity.
7. Identify cash-out patterns: exchange deposits, mixing services, chain-hopping.

Note on Monero (XMR): Monero uses ring signatures, stealth addresses, and RingCT, making transaction tracing significantly harder than Bitcoin. Tools like Graphsense have limited capability against XMR.

---

## 10. Reporting and Dissemination

> Added section not covered in course materials.

### Intelligence Report Structure

A standard intelligence report contains:

1. **Classification / TLP marking** — at top and bottom of every page.
2. **Executive Summary** — the bottom line up front (BLUF). One paragraph answering the core intelligence requirement.
3. **Key Judgments** — bulleted analytical conclusions with explicit confidence levels.
4. **Body** — supporting evidence, analysis, and methodology.
5. **Source Notes** — provenance and credibility rating for each source used.
6. **Appendices** — raw data, screenshots, IOC tables, timeline.

### Writing Style for Intelligence Products

- Lead with the conclusion, not the evidence. Decision-makers need the answer first.
- State confidence levels explicitly in the first paragraph ("With high confidence, we assess...").
- Use precise language. Avoid vague qualifiers without confidence context ("possibly", "may", "could").
- Use the PEEL structure for each analytical claim: Point, Evidence, Explanation, Link.
- Distinguish clearly between facts, assessments, and speculation.
- Avoid first-person language; write in third person or passive voice for formal products.

### Confidence Language Standards

Based on the ODNI/NIC standard:

| Phrase | Confidence Level | Probability Implication |
|--------|-----------------|------------------------|
| We assess with high confidence | High | Strong supporting evidence |
| We assess with moderate confidence | Moderate | Credible but not fully corroborated |
| We assess with low confidence | Low | Fragmented, limited, or questionable sourcing |
| We cannot assess | — | Insufficient information |

### Intelligence Sharing Platforms

| Platform | URL | Purpose |
|---------|-----|---------|
| MISP | https://www.misp-project.org | Open-source threat intel sharing (self-hosted) |
| OpenCTI | https://www.opencti.io | Open-source CTI platform with ATT&CK integration |
| AlienVault OTX | https://otx.alienvault.com | Community threat sharing |
| TAXII / STIX | https://oasis-open.github.io/cti-documentation/ | Structured threat intelligence data standards |

**STIX** (Structured Threat Information eXpression) and **TAXII** (Trusted Automated eXchange of Intelligence Information) are the dominant standards for machine-readable threat intelligence. Understanding them is increasingly expected in professional CTI roles.

---

## 11. Learning Resources and Communities

> Added section. These resources are not covered in course materials.

### Courses and Certifications

| Resource | URL | Notes |
|---------|-----|-------|
| SANS FOR578: Cyber Threat Intelligence | https://www.sans.org/cyber-security-courses/cyber-threat-intelligence/ | Industry-leading CTI course |
| SANS FOR589: Cybercrime Intelligence | https://www.sans.org/cyber-security-courses/cybercrime-intelligence/ | Dark web and criminal OSINT |
| Bellingcat Online Investigations Toolkit | https://docs.google.com/spreadsheets/d/18rtqh8EG2q1xBo2cLNyhIDuK9jrPGwYr9DI2UncoqJQ | Free community resource |
| IntelTechniques OSINT courses | https://inteltechniques.com/courses.html | Michael Bazzell's courses (respected practitioner) |
| TraceLabs OSINT CTF | https://www.tracelabs.org | Missing persons OSINT competitions |
| Maltego Academy | https://www.maltego.com/maltego-academy/ | Free Maltego training |
| OSINT Curious | https://osintcuriosa.com | Community blog and training |

### Reference Collections and Frameworks

| Resource | URL | Notes |
|---------|-----|-------|
| OSINT Framework | https://osintframework.com | Community mind-map of tools by category |
| Bellingcat's Online Investigation Toolkit | (Google Sheets — search "Bellingcat toolkit") | Curated tool list by type |
| IntelTechniques Search Tools | https://inteltechniques.com/tools/ | Michael Bazzell's curated search pages |
| Start.me OSINT Training | https://smart.myosint.training/ | 86,000+ curated source links |
| awesome-osint (GitHub) | https://github.com/jivoi/awesome-osint | Comprehensive GitHub OSINT resource list |

### Communities and Blogs

| Resource | URL | Type |
|---------|-----|------|
| Bellingcat | https://www.bellingcat.com | Investigations, guides, methodology |
| OSINT Curious | https://osintcuriosa.com | Blog and webcast series |
| IntelTechniques | https://inteltechniques.com | Michael Bazzell's blog and podcast |
| The Privacy, Security, & OSINT Show (podcast) | https://inteltechniques.com/podcast.html | Michael Bazzell podcast |
| Hatless1der Blog | https://hatless1der.com | OSINT blog and tool reviews |
| Sector035 OSINT Weekly | https://sector035.nl | Weekly OSINT tool and technique reviews |
| NixIntel | https://nixintel.info | OSINT and forensics blog |
| r/OSINT | https://www.reddit.com/r/OSINT/ | Reddit community |
| TraceLabs | https://www.tracelabs.org | Missing persons OSINT community and CTF |
| Wilder Security | https://www.wilderssecurity.com | Malware and security research forum |

### Practice Environments

| Platform | URL | Purpose |
|---------|-----|---------|
| TraceLabs CTF | https://www.tracelabs.org/initiatives/search-party | Compete finding real missing persons (real-world impact) |
| GeoGuessr | https://www.geoguessr.com | Geolocation training (image-based) |
| GeoGuessr OSINT edition | — | Multiple community maps focused on geolocation methodology |
| OSINT Dojo | https://www.osintdojo.com | OSINT challenges for beginners |
| Hacktoria | https://www.hacktoria.com | OSINT-focused CTF contracts |

---

## 12. Tools and Resources Index

### Note-Taking and Investigation Management

| Tool | URL | Purpose |
|------|-----|---------|
| Obsidian | https://obsidian.md | Local markdown knowledge management |
| Hunchly | https://www.hunch.ly | Automated web evidence capture (Chrome only) |
| Zotero | https://www.zotero.org | Reference and source management |
| Maltego | https://www.maltego.com | Graphical link analysis and entity pivoting |
| Kumu | https://kumu.io | Network and relationship mapping |
| SpiderFoot | https://github.com/smicallef/spiderfoot | Automated OSINT aggregation |
| Recon-ng | https://github.com/lanmaster53/recon-ng | Modular web reconnaissance framework |
| theHarvester | https://github.com/laramies/theHarvester | Email, subdomain, and employee enumeration |
| OpenCTI | https://www.opencti.io | Structured CTI platform with ATT&CK integration |
| MISP | https://www.misp-project.org | Threat intelligence sharing platform |

### OSINT Aggregators and Frameworks

| Tool | URL | Purpose |
|------|-----|---------|
| OSINT Framework | https://osintframework.com | Mind-map of tools by data type |
| Start.me | https://start.me | Customizable OSINT dashboard |
| OSINT Training Start.me | https://smart.myosint.training/ | 86,000+ curated source links |
| IntelTechniques Tools | https://inteltechniques.com/tools/ | Michael Bazzell's curated search pages |
| AlternativeTo | https://alternativeto.net | Find alternatives to any tool |
| Privacytools.io | https://www.privacytools.io | Privacy-focused tool recommendations |
| awesome-osint (GitHub) | https://github.com/jivoi/awesome-osint | Comprehensive OSINT resource list |

### Search Engines

| Tool | URL | Notes |
|------|-----|-------|
| Google | https://google.com | Primary; dorking via operators |
| Yandex | https://yandex.com | Russian sources; superior reverse image search |
| Bing | https://bing.com | Alternative index; `ip:` operator |
| Shodan | https://shodan.io | Internet-connected devices |
| Censys | https://search.censys.io | Certificates and internet infrastructure |
| FOFA | https://fofa.info | Asia-Pacific infrastructure |
| ZoomEye | https://www.zoomeye.org | Device and service search |
| GreyNoise | https://www.greynoise.io | Mass-scanning IP identification |
| Grep.app | https://grep.app | Search public GitHub repositories |
| PublicWWW | https://publicwww.com | Search website source code |
| DuckDuckGo | https://duckduckgo.com | Privacy-focused search |
| Startpage | https://startpage.com | Anonymous Google results |

### Username and Identity Search

| Tool | URL | Purpose |
|------|-----|---------|
| Namechk | https://namechk.com | Username availability |
| WhatsMyName | https://whatsmyname.app | Cross-platform username search |
| KnowEm | https://knowem.com | Username and brand on 500+ sites |
| Sherlock (CLI) | https://github.com/sherlock-project/sherlock | Command-line username search |
| Maigret (CLI) | https://github.com/soxoj/maigret | Advanced username OSINT |
| Holehe (CLI) | https://github.com/megadose/holehe | Email registration check via forgot-password |
| Pipl | https://pipl.com | Deep people search |
| Search4Faces | https://search4faces.com | Facial recognition across social platforms |

### Social Media and Community

| Tool | URL | Purpose |
|------|-----|---------|
| TelegramDB | https://telegramdb.org/ | Telegram channel/group database |
| Lyzem | https://lyzem.com/ | Telegram search engine |
| Search.buzz.im | https://search.buzz.im/ | Telegram open chat search |
| Awesome Telegram OSINT | https://github.com/ItIsMeCall911/Awesome-Telegram-OSINT | Telegram OSINT resources |
| BirdHunt | https://birdhunt.co | Twitter geolocation search |
| Social Bearing | https://socialbearing.com | Twitter analytics |
| Kribrum.io | https://kribrum.io | Russian social media monitoring |
| Clubhouse DB | http://clubhousedb.com | Clubhouse profile search |
| Disboard | https://disboard.org | Public Discord server directory |
| InSpy (CLI) | https://github.com/leapsecurity/InSpy | LinkedIn employee enumeration |
| LinkedIn operators ref | http://recruitmentgeek.com/tools/linkedin/ | LinkedIn search reference |
| Osintgram (CLI) | https://github.com/Datalux/Osintgram | Instagram OSINT |
| InstaLoader (CLI) | https://github.com/instaloader/instaloader | Instagram data download |

### Image and Video Verification

| Tool | URL | Purpose |
|------|-----|---------|
| Google Reverse Image | https://images.google.com | Reverse image search |
| Yandex Images | https://yandex.com/images | Best for faces and Russian sources |
| TinEye | https://tineye.com | Chronological reverse image |
| PimEyes | https://pimeyes.com | Commercial face search |
| ExifTool | https://exiftool.org | EXIF metadata extraction (CLI) |
| Jeffrey's Exif Viewer | http://exif.regex.info/exif.cgi | Web-based EXIF viewer |
| Jimpl | https://jimpl.com | Online EXIF viewer |
| InVID / WeVerify | https://weverify.eu/verification-plugin/ | Video verification browser plugin |
| SunCalc | https://suncalc.org | Sun position and shadow analysis |
| GeoSpy AI | https://geospy.ai | AI geolocation from images |
| PeakFinder | https://www.peakfinder.org | Mountain silhouette identification |
| Google Earth Pro | https://earth.google.com | Historical satellite and Street View |
| Sentinel Hub | https://www.sentinel-hub.com | ESA Copernicus satellite data |
| Mapillary | https://www.mapillary.com | Crowdsourced street-level imagery |

### Infrastructure and Network

| Tool | URL | Purpose |
|------|-----|---------|
| Shodan | https://shodan.io | Internet device search |
| Censys | https://search.censys.io | Certificate and device search |
| FOFA | https://fofa.info | Asia-Pacific device search |
| ZoomEye | https://www.zoomeye.org | Device and service search |
| GreyNoise | https://www.greynoise.io | Mass-scanning IP identification |
| DNSDumpster | https://dnsdumpster.com | DNS record enumeration |
| ViewDNS.info | https://viewdns.info | DNS and IP tools |
| MXToolbox | https://mxtoolbox.com | DNS, MX, blacklist analysis |
| SecurityTrails | https://securitytrails.com | Historical DNS and WHOIS |
| Robtex | https://www.robtex.com | DNS and reverse DNS |
| crt.sh | https://crt.sh | Certificate transparency log search |
| BGP.he.net | https://bgp.he.net | ASN and BGP routing data |
| BGPView | https://bgpview.io | IP and ASN intelligence |
| IPinfo | https://ipinfo.io | IP geolocation and ASN |
| Hunter.io | https://hunter.io | Email discovery for domains |
| Phonebook.cz | https://phonebook.cz | Email, domain, URL intelligence |
| Holehe | https://github.com/megadose/holehe | Email registration check |
| EmailRep | https://emailrep.io | Email reputation |
| URLScan.io | https://urlscan.io | URL sandbox and screenshot |
| AbuseIPDB | https://www.abuseipdb.com | IP abuse reports |
| Spamhaus | https://www.spamhaus.org | IP and domain reputation |
| Wigle.net | https://wigle.net | Wireless network mapping |
| PeeringDB | https://peeringdb.com | Network interconnection data |
| Onyphe | https://www.onyphe.io | Passive DNS and threat intelligence |

### Threat Intelligence

| Tool | URL | Purpose |
|------|-----|---------|
| MITRE ATT&CK | https://attack.mitre.org | TTP database and threat groups |
| ATT&CK Navigator | https://mitre-attack.github.io/attack-navigator/ | ATT&CK visualization |
| ThreatMiner | https://www.threatminer.org | Multi-source threat intelligence |
| AlienVault OTX | https://otx.alienvault.com | Community IOC sharing |
| IBM X-Force Exchange | https://exchange.xforce.ibmcloud.com | Threat intelligence portal |
| Cisco Talos | https://talosintelligence.com | Threat intel and reputation |
| Pulsedive | https://pulsedive.com | IOC enrichment |
| APT Threat Tracking | https://apt.threattracking.com | APT group tracking |
| APT Securelist | https://apt.securelist.com | Kaspersky APT database |
| Malpedia | https://malpedia.caad.fkie.fraunhofer.de | Malware family database |
| APTNotes (GitHub) | https://github.com/kbandla/APTnotes | APT report archive |

### Sandboxes and Malware Analysis

| Tool | URL |
|------|-----|
| Any.run | https://any.run |
| Hybrid Analysis | https://www.hybrid-analysis.com |
| Cuckoo Sandbox | https://cuckoo.cert.ee |
| Joe Sandbox | https://www.joesandbox.com |
| Triage (Hatching) | https://tria.ge |
| VirusTotal | https://www.virustotal.com/en/ |
| Kaspersky OpenTIP | https://opentip.kaspersky.com/ |
| Dr.Web Online | https://online.drweb.com/ |
| ESET Online Scanner | https://www.esetnod32.ru/home/products/online-scanner/ |
| MetaDefender | https://metadefender.opswat.com |

### Data Breach and Leak Intelligence

| Tool | URL |
|------|-----|
| Have I Been Pwned | https://haveibeenpwned.com |
| IntelX | https://intelx.io |
| LeakCheck | https://leakcheck.io |
| Breach Directory | https://breachdirectory.org |
| DeHashed | https://dehashed.com |
| GhostProject | https://ghostproject.fr |
| Snusbase | https://snusbase.com |

### People and Real-World Search

| Tool | URL | Purpose |
|------|-----|---------|
| WebMii | https://webmii.com | Aggregated people search |
| Pipl | https://pipl.com | Professional deep people search |
| TruePeopleSearch | https://www.truepeoplesearch.com | Free US people search |
| PhoneInfoga | https://github.com/sundowndev/phoneinfoga | Phone number OSINT (CLI) |
| Truecaller | https://www.truecaller.com | Phone number lookup |
| LiveATC | https://www.liveatc.net | Live ATC audio |
| ADS-B Exchange | https://globe.adsbexchange.com | Unfiltered aircraft tracking |
| Flightradar24 | https://www.flightradar24.com | Commercial aircraft tracking |
| MarineTraffic | https://www.marinetraffic.com | Vessel tracking |
| ACLED | https://acleddata.com | Armed conflict event data |

### Cryptocurrency

| Tool | URL | Category |
|------|-----|---------|
| Blockchain.com | https://blockchain.com | BTC Explorer |
| Blockchair | https://blockchair.com | Multi-currency explorer |
| Etherscan | https://etherscan.io | ETH explorer |
| Breadcrumbs | https://www.breadcrumbs.app | Visualization |
| OXT | https://oxt.me | BTC analytics |
| Graphsense | https://graphsense.info | Open-source analytics |
| Bitcoinabuse | https://www.bitcoinabuse.com | Abuse detection |
| Scamalert | https://scamalert.sg | Fraud flagging |

### Anonymity and OPSEC

| Tool | URL | Purpose |
|------|-----|---------|
| Tails OS | https://tails.boum.org | Amnesic live OS via Tor |
| Whonix | https://www.whonix.org | Two-VM Tor-routing OS |
| Tor Browser | https://www.torproject.org | Tor-based browser |
| Am I Unique | https://amiunique.org/fp | Browser fingerprint test |
| Cover Your Tracks | https://coveryourtracks.eff.org | EFF fingerprint test |
| BrowserLeaks | https://browserleaks.com | Comprehensive leak tests |
| IPLeak | https://ipleak.net | DNS and IP leak test |
| DNS Leak Test | https://www.dnsleaktest.com | DNS provider verification |
| Fake Name Generator | https://www.fakenamegenerator.com/ | Complete identity profile |
| Portableapps | https://portableapps.com/download | Portable app suite |

### Browser Extensions (OSINT/OPSEC)

| Extension | Purpose |
|-----------|---------|
| uBlock Origin | Ad and tracker blocker |
| uBlock Origin Extra | Companion extension |
| Privacy Badger | Automatic tracker learning |
| DuckDuckGo Privacy Essentials | Tracker blocking and private search |
| Ghostery | Ad blocker and tracker stopper |
| HTTPS Everywhere | Force HTTPS |
| WebRTC Control | WebRTC IP leak prevention |
| WebRTC Leak Shield | Disable WebRTC |
| Canvas Defender | Canvas fingerprint noise |
| Location Guard / Vytal | Geolocation and timezone spoofing |
| User-Agent Switcher | Spoof browser identity |
| Firefox Multi-Account Containers | Session isolation per persona |
| Shodan | Hosting info and open ports for current site |
| Mitaka | Context-menu IOC search (IP, domain, hash, CVE) |
| ThreatPinch Lookup | Hover-based threat intel tooltips |
| Threat Analytics Search | IOC context-menu search |
| Vulners Web Scanner | Passive vulnerability scanning |
| PhotoOSINT | EXIF metadata scanner for page images |
| Reverse Image Search | Right-click reverse image |
| InVID / WeVerify | Video verification |
| Data Scraper | HTML to Excel data extraction |
| Password Checkup | Breach exposure alert |
| Malwarebytes Browser Guard | Malware and phishing protection |
| Zotero Connector | Save references to Zotero |
| Windscribe | Free proxy and ad blocker |
| NewsGuard | News site credibility ratings |
| KProxy Extension | Anonymous proxy |
| Censor Tracker | Censorship circumvention |
| Grammarly | Writing assistance |
| Google Translate | Inline translation |
| DALL-E 2 Google Extension | AI image results in Google Images |
| Map Switcher | Switch between map providers |
| W3bin | Identify website hosting |
| Unstoppable Extension | Access blockchain domains |

---

*Course: 3080 - Open Source Intelligence and Operational Security*  
*Base notes from course materials, extended with additional frameworks, techniques, and tools.*  
*For educational use. All tools should be used in accordance with applicable law and ethical guidelines.*

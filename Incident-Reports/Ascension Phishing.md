# Phishing Incident Triage – Ascension Health Ransomware Recovery (2024)

## Overview
During the 2024 Ascension Health ransomware recovery period, I served as a first-responder for potential endpoint compromises and phishing reports across a multi-state healthcare environment spanning New York to Texas. This writeup documents the triage methodology I followed during that period.

> **Note:** All patient data, proprietary system details, and identifying information have been omitted. This documents methodology only.

---

## Background
Ascension Health experienced a significant ransomware incident in 2024 that disrupted systems across multiple states. During the recovery period, standard administrative functions (password resets, MFA changes) were suspended, making endpoint triage and phishing response a critical frontline responsibility for the support team.

---

## Triage Workflow

### Step 1 — Initial User Report
When a user reported suspicious activity, a potential phishing email, or scareware behavior, I would:
- Log the incident in ServiceNow with full user and device details
- Remotely access the affected endpoint via **Bomgar**
- Assess the situation before taking any action

### Step 2 — Scareware vs. Genuine Compromise
For reported scareware or suspicious popups:
- Investigated browser settings to determine if popups were being allowed from specific domains
- If browser-based and containable — documented the source domain and resolved
- If behavior could not be attributed to browser settings — immediately advised the user to **power off the device and disconnect the ethernet cable**, then escalated to the physical security (FS) team for forensic handling

### Step 3 — Phishing Email Analysis
For reported phishing emails:
- Remotely accessed the user's machine via **Bomgar**
- Opened the suspicious email in **Gmail**
- Exported the raw email headers and source via Gmail's "Show Original" feature
- Transferred the data securely to my **VDI** for analysis, keeping potentially malicious content off the endpoint

### Step 4 — Header & Domain Analysis
On my VDI:
- Reviewed email headers for spoofed sender addresses, mismatched reply-to fields, and suspicious routing
- Extracted domains and IP addresses from headers and email body
- Submitted domains to **VirusTotal** for reputation analysis
- Submitted IPs to **AbuseIPDB** for abuse confidence scoring and historical report review

### Step 5 — IOC Documentation
- **Defanged** all malicious domains and IPs in documentation (e.g., `malicious[.]com`, `192[.]168[.]1[.]1`) to prevent accidental clicks
- Documented full findings including sender analysis, domain/IP verdicts, and timeline
- Pasted raw email source into the ServiceNow ticket
- Escalated to the security team with a complete triage summary

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Bomgar | Secure remote access to affected endpoints |
| Gmail "Show Original" | Raw email header extraction |
| VirusTotal | Domain and file reputation analysis |
| AbuseIPDB | IP abuse history and confidence scoring |
| ServiceNow | Incident documentation and escalation |

---

## Key Takeaways
- Analyzed potentially malicious content on an isolated VDI rather than the affected endpoint — limiting exposure
- Defanging IOCs in documentation is a standard practice that prevents accidental navigation to malicious infrastructure
- Clear isolation procedures (power off, disconnect ethernet) are critical during active incidents when normal remediation tools are unavailable
- Structured documentation enables faster escalation and more effective response by downstream security teams

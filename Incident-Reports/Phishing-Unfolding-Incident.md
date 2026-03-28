# Phishing Campaign Investigation with Malware Delivery and Post-Exploitation Activity

## Scenario Overview

A series of alerts were triggered indicating suspicious email activity, followed by potential execution and system-level behavior. The investigation was conducted to determine whether the activity represented a phishing attempt, malware delivery, and possible post-exploitation actions.

---

## Timeline of Events

* **17:15** – Suspicious phishing email received from external domain
* **17:18** – System process activity observed (baseline OS behavior)
* **17:20** – Additional system processes triggered (validated as benign)
* **17:26** – Email containing suspicious ZIP attachment delivered
* **17:49** – PowerShell spawned `net.exe` to map a network drive
* **17:50+** – Multiple high-severity alerts indicating suspicious process activity

---

## Initial Access – Phishing Activity

A phishing email was identified with the following characteristics:

* Sender: `eileen@trendymillineryco.me`
* Recipient: `support@tryhackme.com`
* Subject: Inheritance-themed financial lure
* Indicators:

  * Unusual domain (`.me` TLD)
  * Social engineering language requesting sensitive information
  * Urgency and financial incentive

### Key Finding

Pivoting on the sender domain revealed multiple emails from the same source, indicating a broader phishing campaign. Only one email triggered detection, suggesting incomplete rule coverage.

---

## Malware Delivery – Suspicious Attachment

A second email introduced a ZIP attachment:

* File: `ImportantInvoice-Febrary.zip`
* Sender: `john@hatmakereurope.xyz`

### Indicators:

* Suspicious domain (`.xyz` TLD)
* Urgency and legal threats in message content
* Misspelled file name (“Febrary”)
* Compressed archive commonly used to evade detection

### Assessment

The attachment was treated as a potential malware delivery mechanism. The file was not executed during analysis and was escalated for sandbox detonation.

---

## Execution and Post-Exploitation Activity

### Suspicious Process Behavior

A notable event was observed:

* `powershell.exe` → `net.exe`
* Command:
  net use Z: \FILESRV-01\SSF-FinancialRecords
* Execution directory:
  `C:\Users\michael.ascot\downloads\`

### Assessment

This behavior is not typical for standard user activity and may indicate:

* Scripted execution following user interaction
* Attempted access to internal network resources
* Potential lateral movement or data staging

---

## False Positive Validation

Several alerts involving system processes were investigated and classified as benign:

### Example:

* `services.exe` → `TrustedInstaller.exe`
* `svchost.exe` → `taskhostw.exe`

### Justification:

* Known Windows processes
* Execution from trusted system directories
* Expected parent-child relationships

---

## User Interaction Verification

A search was conducted to determine whether the recipient responded to the phishing email.

### Result:

No outbound communication was identified.

### Impact:

* No confirmed user engagement
* Reduced likelihood of credential compromise

---

## Indicators of Compromise (IOCs)

* Domains:

  * `trendymillineryco.me`
  * `hatmakereurope.xyz`

* Email Addresses:

  * `eileen@trendymillineryco.me`
  * `john@hatmakereurope.xyz`

* File:

  * `ImportantInvoice-Febrary.zip`

---

## Detection Gaps Identified

* Detection rules failed to identify all emails from the malicious domain
* Benign system activity generated unnecessary alerts
* Opportunities exist to improve rule tuning for both accuracy and noise reduction

---

## Final Assessment

This activity represents a **phishing campaign with attempted malware delivery**, followed by **suspicious system behavior potentially indicative of post-exploitation activity**.

While no confirmed compromise occurred, the sequence of events suggests a high-risk scenario requiring escalation and monitoring.

---

## Recommended Remediation Actions

* Block malicious domains:

  * `trendymillineryco.me`
  * `hatmakereurope.xyz`

* Quarantine affected emails

* Submit attachment for sandbox analysis

* Monitor endpoint activity for execution or persistence

* Improve detection rules for domain-based phishing

* Tune alerts to reduce false positives from legitimate system processes

---

## Skills Demonstrated

* SIEM investigation and log analysis
* Phishing detection and analysis
* Malware delivery identification
* Process behavior analysis (parent-child relationships)
* False positive validation
* Incident correlation and timeline construction
* Detection rule evaluation and tuning awareness

---

## Performance Summary

* True Positive Identification Rate: 94%
* False Positive Identification Rate: 93%
* Alerts Handled: 29
* Mean Time to Resolve: 3 minutes

---

## Key Takeaways

* Phishing campaigns often involve multiple stages, including delivery, execution, and follow-on activity
* Contextual analysis is critical when evaluating process behavior
* Detection systems require continuous tuning to balance accuracy and noise
* Correlating multiple alerts into a single incident is essential for effective SOC operations

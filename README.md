# SOC Analyst Portfolio

## About Me

Aspiring SOC Analyst with hands-on experience in security investigations, SIEM analysis, and incident response. Currently developing real-world cybersecurity skills through practical labs and documented case studies using tools like Splunk.

---

## Key Highlight

Investigated a multi-stage phishing incident involving malware delivery and post-exploitation activity, achieving:
- 94% true positive identification rate
- 93% false positive accuracy
- 29 alerts triaged in a simulated SOC environment
---

## Skills & Tools

* SIEM: Splunk
* Threat Detection & Analysis
* Incident Response
* Log Analysis
* MITRE ATT&CK Framework
* Phishing Investigation

---

## Portfolio Projects

### Phishing Incident Investigation

* Investigated a phishing attack involving user interaction with a malicious link
* Analyzed logs and identified indicators of compromise
* Mapped activity to MITRE ATT&CK techniques
* Recommended remediation actions

### Phishing Campaign Investigation (Multi-Stage Incident)
-> [View Full Investigation](./Incident-Reports/Phishing-Unfolding-Incident.md)

### Brute Force Incident Investigation
* Reviewed Authentication Logs
  * The authentication records showed a burst of failed login attempts targeting a single user account, followed by a successful login from the same IP address.
* Identified Attack Pattern
  * The sequence of repeated failures followed by success strongly suggested password guessing or brute force activity rather than normal user error.
* Evaluated Timing
    * The login activity occurred at approximately 02:14 AM, which is outside standard working hours for most corporate users and increases suspicion.
* Assessed Source IP Context
    * The source IP was treated as suspicious because it was external, repeated rapidly across authentication attempts, and was tied directly to the successful login event.
* Compared Against Normal User Behaviour
    * A legitimate user may occasionally mistype a password once or twice, but eight failed attempts followed by a success from the same IP in under a minute is not typical behavior.

### Brute Force Investigation
 -> [View Full Investigation](./Incident-Reports/Brute-Force-Investigation.md)

---

## Current Focus

* Completing TryHackMe SOC Level 1 Path
* Strengthening Splunk query skills
* Building real-world incident investigation portfolio

---

## Connect With Me

* LinkedIn: https://www.linkedin.com/in/joshua-sell-dallas
* GitHub: https://github.com/nuwuser

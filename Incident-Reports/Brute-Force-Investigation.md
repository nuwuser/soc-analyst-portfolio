
#Brute Force Attack Investigation
#Overview

---

This project documents a simulated Security Operations Center (SOC) investigation involving repeated failed VPN login attempts followed by a successful authentication from the same source IP address. The objective was to determine whether the activity was benign or indicative of an account compromise.

This case study demonstrates core SOC analyst skills including alert triage, log analysis, investigative reasoning, and incident response recommendations.

#Scenario

At approximately 02:14 AM, multiple failed login attempts were detected against a corporate VPN account. Shortly afterward, a successful login was recorded from the same external IP address.

The activity was flagged as suspicious due to the volume of failed attempts, the timing of the login, and the successful authentication after repeated failures.

## Simulated Alert
Alert Name: Possible Brute Force Attack Against VPN Account
Severity: Medium-High
Detection Logic: Multiple failed login attempts followed by a successful login from the same IP within a short time window
Affected User: j.smith
Source IP: 185.243.115.84
Log Data
Timestamp        Username     Source_IP       Action
----------------------------------------------------------
02:14:03         j.smith      185.243.115.84  Failed Login
02:14:07         j.smith      185.243.115.84  Failed Login
02:14:10         j.smith      185.243.115.84  Failed Login
02:14:15         j.smith      185.243.115.84  Failed Login
02:14:18         j.smith      185.243.115.84  Failed Login
02:14:22         j.smith      185.243.115.84  Failed Login
02:14:27         j.smith      185.243.115.84  Failed Login
02:14:31         j.smith      185.243.115.84  Failed Login
02:14:36         j.smith      185.243.115.84  Successful Login
Initial Triage

During triage, several indicators suggested potentially malicious activity:

Multiple failed login attempts occurred in rapid succession
All attempts originated from the same external IP address
A successful login followed immediately after the failures
The activity occurred outside normal business hours
The pattern was inconsistent with typical user behavior

These factors justified further investigation.

Investigation Process
1. Reviewed Authentication Logs

Authentication logs revealed a burst of failed login attempts targeting a single account, followed by a successful login from the same IP address.

2. Identified Attack Pattern

The sequence of repeated failures followed by success is consistent with brute force or password guessing activity.

3. Evaluated Timing

The activity occurred at approximately 02:14 AM, outside standard working hours, increasing the likelihood of malicious intent.

4. Assessed Source IP

The source IP was external and repeatedly attempted authentication in a short timeframe, which is not typical for legitimate user activity.

5. Compared Against Normal Behavior

While occasional login failures are normal, repeated rapid failures followed by a success strongly indicate automated or persistent login attempts.

Key Findings
8 failed login attempts occurred within ~33 seconds
A successful login immediately followed the failures
All activity originated from 185.243.115.84
The login occurred during unusual hours
The pattern aligns with brute force attack behavior
Analyst Assessment

This activity is consistent with a brute force attack that likely resulted in a successful account compromise.

The defining factor is the progression from repeated failed authentication attempts to a successful login from the same source IP within a short time window.

Verdict: True Positive

Recommended Response Actions

If this were a production environment, the following actions would be recommended:

Temporarily disable the affected account
Force a password reset
Invalidate all active sessions
Block or monitor the source IP address
Investigate potential lateral movement
Review additional authentication attempts from the same IP
Enforce or verify multi-factor authentication (MFA)
If This Were a Real SOC Environment

Further investigation would include:

SIEM Analysis
Identify additional activity tied to the source IP or user
VPN Logs
Review session details and accessed resources
Endpoint Detection and Response (EDR)
Check for suspicious processes or endpoint compromise
Firewall / Proxy Logs
Identify unusual outbound connections
Identity Provider Logs
Confirm MFA behavior and authentication anomalies
Detection Opportunities

This scenario highlights several useful detection strategies:

Multiple failed login attempts from a single IP
Successful login following repeated failures
Login activity outside expected hours
Geographic anomalies in authentication
Example Detection Logic
Alert on 5+ failed logins within a short timeframe
Escalate if followed by a successful login from the same IP
Increase severity for off-hours authentication events
Lessons Learned
Repeated failed logins should always be investigated
Context (timing, frequency, and source) is critical in determining risk
A simple login alert can indicate a full account compromise
Effective SOC analysis includes both detection and response planning
Skills Demonstrated
Alert triage
Log analysis
Incident investigation
Pattern recognition
True positive determination
Incident response planning
SOC documentation
Project Purpose

This project was created as part of a SOC analyst portfolio to demonstrate practical, investigation-focused cybersecurity skills using a realistic brute force attack scenario.

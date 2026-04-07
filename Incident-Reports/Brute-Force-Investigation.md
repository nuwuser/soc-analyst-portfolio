

---

# Brute Force Attack Investigation

---

## Overview

This project documents a simulated Security Operations Center (SOC) investigation involving repeated failed VPN login attempts followed by a successful authentication from the same source IP address.

The objective was to determine whether the activity was benign or indicative of an account compromise.

This case study demonstrates:

* Alert triage
* Log analysis
* Investigative reasoning
* Incident response recommendations

---

## Scenario

At approximately **02:14 AM**, multiple failed login attempts were detected against a corporate VPN account.

Shortly afterward, a successful login was recorded from the same external IP address.

The activity was flagged as suspicious due to:

* High volume of failed attempts
* Off-hours login timing
* Successful authentication after repeated failures

---

## Simulated Alert

* **Alert Name:** Possible Brute Force Attack Against VPN Account
* **Severity:** Medium-High
* **Detection Logic:** Multiple failed logins followed by a success from the same IP
* **Affected User:** `j.smith`
* **Source IP:** `185.243.115.84`

---

## Log Data

```
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
```

---

## Initial Triage

During triage, several indicators suggested malicious activity:

* Multiple failed login attempts in rapid succession
* All attempts originated from the same external IP
* A successful login immediately followed failures
* Activity occurred outside normal business hours
* Behavior was inconsistent with normal user activity

---

## Investigation Process

### 1. Reviewed Authentication Logs

Authentication logs showed a burst of failed login attempts targeting a single account, followed by a successful login from the same IP.

---

### 2. Identified Attack Pattern

The sequence of repeated failures followed by success is consistent with:

* Brute force attacks
* Password guessing attempts

---

### 3. Evaluated Timing

The activity occurred at **02:14 AM**, which is outside typical working hours and increases suspicion.

---

### 4. Assessed Source IP

The source IP:

* Was external
* Repeatedly attempted authentication
* Was directly tied to the successful login

---

### 5. Compared Against Normal Behavior

A legitimate user may mistype a password once or twice.

However:

* 8 rapid failures
* Followed by a success

> Strong indicator of automated or persistent attack behavior

---

## Key Findings

* **8 failed login attempts** within ~33 seconds
* **1 successful login** immediately after
* All activity originated from `185.243.115.84`
* Login occurred during unusual hours
* Pattern matches brute force attack behavior

---

## Analyst Assessment

This activity is **consistent with a brute force attack resulting in account compromise**.

The defining factor:

* Repeated failed logins
* Followed by a successful authentication from the same IP

### Verdict

* **True Positive**

---

## Recommended Response Actions

If this were a production environment:

* Disable the affected account
* Force a password reset
* Invalidate all active sessions
* Block or monitor the source IP
* Investigate for lateral movement
* Review additional login attempts
* Enforce or verify MFA

---

## If This Were a Real SOC Environment

Further investigation would include:

### SIEM

* Search for additional activity from the same IP
* Correlate with other alerts

### VPN Logs

* Review session duration
* Identify accessed resources

### EDR

* Check for suspicious processes
* Look for endpoint compromise

### Firewall / Proxy Logs

* Identify unusual outbound connections

### Identity Logs

* Verify MFA usage
* Check for authentication anomalies

---

## Detection Opportunities

This scenario highlights useful detection strategies:

* Multiple failed logins from one IP
* Successful login after failures
* Off-hours login activity
* Geographic anomalies

### Example Detection Logic

* Alert on **5+ failed logins within short timeframe**
* Escalate if followed by **successful login**
* Increase severity for **off-hours activity**

---

## Lessons Learned

* Repeated failed logins should never be ignored
* Context (timing, frequency, source) is critical
* Simple alerts can indicate full compromise
* SOC analysis requires both detection and response planning

---

## Skills Demonstrated

* Alert triage
* Log analysis
* Incident investigation
* Pattern recognition
* True positive identification
* Incident response planning
* Professional SOC documentation

---

## Project Purpose

This project was created as part of a SOC analyst portfolio to demonstrate practical, investigation-focused cybersecurity skills using a realistic brute force attack scenario.

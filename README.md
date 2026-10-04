# SSH Log Analysis & Brute-Force Detection using Splunk

## Project Overview

This project demonstrates a SOC Level 1 investigation of SSH authentication logs using Splunk Enterprise.

The goal was to analyze SSH login activity, identify repeated failed authentication attempts, investigate targeted usernames and source IPs, and detect activity consistent with potential SSH brute-force behavior.

## Objectives

- Analyze SSH authentication logs
- Identify failed SSH login attempts
- Identify successful SSH logins
- Find targeted usernames
- Identify suspicious source IP addresses
- Correlate failed and successful authentication attempts
- Detect potential SSH brute-force activity
- Create a Splunk security monitoring dashboard

## Tools Used

- Splunk Enterprise
- Linux SSH authentication logs
- SPL (Search Processing Language)
- Windows laptop

## Log Configuration

- **Log file:** `auth.log`
- **Index:** `main`
- **Source type:** `linux_secure`

## Investigation Results

| Investigation | Result |
|---|---|
| Failed SSH logins | 300 |
| Successful SSH logins | 2,001 |
| Top targeted username | `root` |
| Failed attempts against root | 300 |
| Top failed-login source IP | `203.0.113.50` |
| Failed attempts from source | 300 |
| Successful authentication from source | 1 |

## Key Finding

Splunk analysis identified repeated failed SSH authentication attempts from `203.0.113.50` targeting the `root` account.

A successful authentication was subsequently observed from the same source.

This pattern is consistent with **potential SSH brute-force activity** and should be investigated further.

> Note: `203.0.113.50` is a documentation/example IP address present in the sample dataset. It should not be treated as a real attacker IP.

## Investigation Process

### 1. Failed SSH Login Analysis

The SSH logs were searched for failed password authentication events.

### 2. Username Analysis

The username was extracted from failed authentication events to determine which accounts were being targeted.

The `root` account was the most targeted username.

### 3. Source IP Analysis

Source IP addresses were extracted from the SSH events to identify the systems generating failed login attempts.

### 4. Successful Login Analysis

Successful SSH authentication events were identified using accepted authentication events.

### 5. Correlation

Failed and successful authentication events were correlated by source IP.

This identified a source with a large number of failures followed by a successful authentication.

### 6. Brute-Force Detection

A threshold-based search was used to identify source IPs with a high number of failed SSH authentication attempts.

## Splunk Dashboard

The dashboard contains:

- Total Failed SSH Logins
- Total Successful SSH Logins
- Top Failed Login Source IPs
- Top Targeted Usernames
- Potential SSH Brute-Force Sources
- SSH Login Activity Timeline

## SOC Analyst Skills Demonstrated

- Log analysis
- SSH authentication investigation
- SPL queries
- Field extraction using `rex`
- Event counting and aggregation
- Source IP analysis
- Authentication correlation
- Brute-force detection
- Security dashboard creation
- Basic SOC investigation and reporting

## Recommended SOC Response

If this were a real security event, the SOC analyst should:

1. Validate whether the successful login was authorized.
2. Review the affected account.
3. Investigate activity after the successful authentication.
4. Check for suspicious commands or processes.
5. Review additional activity from the source IP.
6. Escalate the incident if unauthorized activity is confirmed.

## Project Files

```text
SSH-Splunk-SOC-Project/
│
├── README.md
├── SPL-Queries.txt
├── Investigation-Report.pdf
├── Dashboard-Evidence.pdf
└── Screenshots/
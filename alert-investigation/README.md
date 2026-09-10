# 🔎 SOC Alert Investigation Lab

Hands-on SOC investigation focused on analyzing a suspected SSH brute-force attack and potential account compromise.

## Objective

The objective of this lab is to practice a basic SOC investigation workflow, including:

* Analyzing authentication logs
* Correlating security events
* Identifying suspicious activity
* Investigating Indicators of Compromise (IOCs)
* Establishing an incident timeline
* Assessing severity and confidence
* Documenting findings
* Recommending containment and response actions
* Escalating a potential security incident

## Scenario

A security monitoring alert was generated after multiple failed SSH authentication attempts were detected against the `admin` account on `web-server01`.

The authentication attempts originated from the same external IP address. Shortly after the failed attempts, a successful login was recorded from the same IP and account.

Additional activity was then observed during the authenticated session, including system reconnaissance, privilege enumeration, and connections to other internal hosts.

The activity was investigated as a potential account compromise.

## 🔍 Investigation Process

The investigation followed these steps:

1. Review authentication logs.
2. Identify repeated failed authentication attempts.
3. Correlate the successful authentication with the same source IP and account.
4. Review post-authentication activity.
5. Identify suspicious commands and network connections.
6. Extract relevant indicators.
7. Build an incident timeline.
8. Assess severity and confidence.
9. Recommend containment and further investigation.
10. Document the final disposition and escalation.

## Evidence

### Authentication Logs

`logs/auth.log`

Contains the simulated SSH authentication events, including failed and successful login attempts.

### Session Evidence

`evidence/session.log`

Contains activity observed after the successful authentication, including:

* Process execution
* User identification
* Account enumeration
* Privilege enumeration
* Internal network connections
* Command history review

### Alert Investigation

`alerts/alert-001.md`

Contains the complete investigation, including:

* Alert information
* Incident summary
* Indicators of Compromise
* Timeline
* Investigation findings
* Recommended actions
* Incident classification
* Final conclusion

##  Key Findings

The investigation identified:

* Five consecutive failed SSH authentication attempts.
* A successful authentication from the same external IP address.
* Post-authentication reconnaissance activity.
* Enumeration of local accounts and available privileges.
* Connections to additional internal hosts using SMB and SSH.
* A pattern consistent with possible unauthorized access.

##  Final Assessment

| Field         | Result                       |
| ------------- | ---------------------------- |
| Incident Type | Potential Account Compromise |
| Severity      | High                         |
| Confidence    | Medium                       |
| Disposition   | Escalated                    |
| Status        | Closed - Escalated           |

The available evidence is consistent with a potential compromise of the `admin` account.

Because the evidence is simulated, the investigation does not establish definitive compromise or attribution. The case was therefore classified as a potential security incident and escalated for further investigation.

##  Skills Practiced

**SOC Operations:** Alert Triage · Event Correlation · Incident Investigation · Incident Classification

**Security Analysis:** Authentication Analysis · IOC Identification · Timeline Analysis · Evidence Review

**Networking:** SSH · SMB · TCP/IP · Internal Network Connections

**Incident Response:** Containment · Evidence Preservation · Escalation · Incident Documentation

---

> This laboratory uses simulated security events for educational purposes and documents a practical SOC investigation workflow.

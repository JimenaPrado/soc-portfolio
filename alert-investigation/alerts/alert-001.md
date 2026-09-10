# SOC-001 — Possible Brute Force and Account Compromise

## Alert Information

| Field | Value |
|---|---|
| Alert ID | SOC-001 |
| Severity | High |
| Status | Open |
| Category | Credential Access |
| Affected Host | web-server01 |
| Affected User | admin |
| Source IP | 185.220.101.45 |
| Detection Time | 2026-09-09 08:41:12 |

## Incident Summary

Multiple failed SSH authentication attempts were detected against the `admin` account from the same external IP address, `185.220.101.45`.

Five consecutive authentication failures were followed by a successful login from the same IP and account. After authentication, the session executed commands related to system and privilege enumeration and established network connections to other internal hosts.

The activity is consistent with a possible brute-force attack followed by potential account compromise and requires further investigation.


## Indicators of Compromise (IOCs)

| Type | Indicator | Description |
|---|---|---|
| IP Address | `185.220.101.45` | Source IP associated with repeated failed logins and successful authentication |
| User Account | `admin` | Account targeted during the authentication attempts |
| Host | `web-server01` | Host where the suspicious session was established |
| Destination IP | `10.10.20.25:445` | Internal connection using SMB |
| Destination IP | `10.10.20.30:22` | Internal connection using SSH |


## Timeline of Events

| Time | Event | Analysis |
|---|---|---|
| 08:41:12 | Failed SSH authentication | First failed authentication attempt against the `admin` account |
| 08:41:18 | Failed SSH authentication | Repeated authentication attempt from the same source IP |
| 08:41:24 | Failed SSH authentication | Third consecutive failed attempt |
| 08:41:31 | Failed SSH authentication | Fourth consecutive failed attempt |
| 08:41:38 | Failed SSH authentication | Fifth consecutive failed attempt |
| 08:42:05 | Successful SSH authentication | Successful login to `web-server01` using the `admin` account from the same source IP |
| 08:42:11 | Bash session started | Interactive shell established after successful authentication |
| 08:42:19 | `whoami` executed | Possible verification of the current account |
| 08:42:27 | `/etc/passwd` accessed | Possible enumeration of local system accounts |
| 08:42:41 | `sudo -l` executed | Possible enumeration of available administrative privileges |
| 08:42:56 | Network connection to `10.10.20.25:445` | Connection to an internal host using SMB |
| 08:43:04 | Network connection to `10.10.20.30:22` | Connection to an internal host using SSH |
| 08:43:11 | `history` executed | Review of previously executed shell commands |


## Analysis & Investigation

The investigation identified a sequence of events consistent with a possible brute-force attack followed by unauthorized access to the `admin` account.

Five consecutive failed SSH authentication attempts were observed from `185.220.101.45` within approximately 26 seconds. A successful authentication for the same `admin` account occurred shortly afterward from the same source IP.

Following the successful authentication, the session executed several commands that may indicate system reconnaissance:

- `whoami` — identifies the current user.
- `cat /etc/passwd` — retrieves information about local system accounts.
- `sudo -l` — checks the user's available administrative privileges.
- `history` — displays previously executed shell commands.

The session also established connections to two internal hosts:

- `10.10.20.25:445` — SMB connection.
- `10.10.20.30:22` — SSH connection.

The combination of repeated authentication failures, successful authentication from the same source, system and privilege enumeration, and subsequent internal network connections increases the likelihood of unauthorized activity.

Based on the available evidence, the activity should be treated as a potential account compromise and escalated for further investigation.



## Recommended Actions

### 1. Containment

- Temporarily restrict or block the source IP `185.220.101.45`, following the organization's incident response procedures.
- Review the `admin` account and consider temporarily disabling or resetting its credentials.
- Restrict unnecessary access from `web-server01` to the internal hosts involved in the investigation.

### 2. Evidence Preservation

- Preserve the authentication and session logs associated with the incident.
- Collect relevant system, authentication, and network logs for further analysis.
- Record the timestamps, source IP, affected account, affected host, and observed commands.

### 3. Further Investigation

- Determine whether the `admin` account was legitimately used during the identified period.
- Investigate activity originating from `185.220.101.45` across other monitored systems.
- Review connections to `10.10.20.25` and `10.10.20.30` for related suspicious activity.
- Search for additional authentication attempts involving the same source IP or account.
- Review whether any configuration, account, or privilege changes occurred after the successful authentication.

### 4. Escalation

The alert should be escalated to the appropriate incident response or security team because the available evidence indicates a potential compromise of the `admin` account and possible activity involving additional internal hosts.

### 5. Ticket Follow-up

Create a security incident ticket containing:

- Alert ID: `SOC-001`
- Severity: `High`
- Source IP: `185.220.101.45`
- Affected account: `admin`
- Affected host: `web-server01`
- Summary of findings
- Evidence collected
- Actions performed
- Escalation status
- Investigation owner
- Current status


## Incident Classification

| Field | Value |
|---|---|
| Classification | Potential Account Compromise |
| Severity | High |
| Confidence | Medium |
| Disposition | Escalated |
| Status | Closed - Escalated |

### Conclusion

The investigation identified multiple failed SSH authentication attempts against the `admin` account, followed by a successful authentication from the same external IP address.

Post-authentication activity included system and privilege enumeration and network connections to additional internal hosts. This behavior is suspicious and is consistent with a potential account compromise.

Due to the available evidence and the potential impact of unauthorized access to a privileged account, the alert was classified as **High severity** and **escalated for further investigation**.

No definitive attribution or confirmation of compromise can be established from the simulated evidence alone.
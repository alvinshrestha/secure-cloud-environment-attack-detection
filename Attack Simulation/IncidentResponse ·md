# Incident Response — SSH Brute Force Detection

## Overview

This document outlines the incident response process for the SSH brute force attack detected on April 28, 2026 against `vm-security-lab`. It follows a structured incident response framework covering detection, analysis, containment, eradication, recovery, and lessons learned.

---

## Incident Summary

| Field | Detail |
|---|---|
| Incident Type | SSH Brute Force Attack |
| Detection Method | Azure Monitor Log Alert |
| Affected Resource | vm-security-lab |
| Attacker IP | 203.164.222.82 |
| Attack Tool | Hydra v9.5 |
| Total Attempts | 72 credential attempts |
| Successful Logins | 0 |
| Detection Time | April 28, 2026 — 11:30 UTC |
| Response Time | Immediate (simulated environment) |
| Severity | Sev2 |

---

## Incident Response Framework

This response follows the **NIST SP 800-61** Incident Response lifecycle:

```
1. Preparation
2. Detection & Analysis
3. Containment
4. Eradication
5. Recovery
6. Post-Incident Activity
```

---

## Phase 1 — Preparation

Controls already in place before the incident:

| Control | Status |
|---|---|
| SSH password authentication disabled | ✅ Active |
| NSG restricting SSH to known IPs only | ✅ Active |
| Linux Syslog collection via DCR | ✅ Active |
| KQL detection rule in Azure Monitor | ✅ Active |
| Email alerting via Action Group | ✅ Active |

---

## Phase 2 — Detection & Analysis

### Initial Detection

Alert `alert-suspicious-ssh-activity` fired at 11:30 UTC via Azure Monitor. Email notification received via `ag-security-lab` Action Group.

### Investigation Query

The following KQL query was used to investigate the scope of the attack:

```kql
Syslog
| where Facility == "auth" or Facility == "authpriv"
| where SyslogMessage contains "Invalid user"
    or SyslogMessage contains "Failed password"
| project TimeGenerated, Facility, SyslogMessage
| order by TimeGenerated desc
| take 20
```

### Findings

- **Attack source:** Single IP — `203.164.222.82`
- **Usernames attempted:** admin, root, test, ubuntu, user, guest, alvin, mecca, sysadmin
- **Pattern:** Rapid sequential attempts — characteristic of automated brute force tooling
- **Result:** All attempts rejected — no successful authentication

### Severity Assessment

| Factor | Assessment |
|---|---|
| Successful login? | No |
| Data exfiltration? | No |
| Lateral movement? | No |
| Impact to availability? | None |
| Overall severity | Low (in this case) — high volume but no compromise |

---

## Phase 3 — Containment

### Immediate Actions

In a real incident, the following containment steps would be taken:

**1. Block the attacker IP at NSG level:**
```
Azure Portal → vm-security-lab-nsg → Inbound rules → Add rule:
Priority: 100
Source: 203.164.222.82/32
Port: 22
Action: Deny
```

**2. Isolate the VM if compromise is suspected:**
```
Azure Portal → vm-security-lab → Networking → 
Remove all inbound rules temporarily
```

**3. Preserve evidence:**
```kql
Syslog
| where Facility == "auth" or Facility == "authpriv"
| where SyslogMessage contains "Invalid user"
    or SyslogMessage contains "Failed password"
| where TimeGenerated between (
    datetime(2026-04-28T11:00:00Z) .. datetime(2026-04-28T12:00:00Z))
| project TimeGenerated, Facility, SyslogMessage
| order by TimeGenerated asc
```
Export results for forensic record.

---

## Phase 4 — Eradication

### Actions in This Simulation

Since no compromise occurred, eradication steps were minimal:

- Password authentication re-disabled on SSH daemon
- Verified via Hydra re-test — attack surface confirmed closed
- NSG rules reviewed and confirmed correct

### In a Real Incident, Additionally:

- Audit all user accounts for unauthorised additions
- Review `/var/log/auth.log` for any successful logins
- Check for new SSH keys added to `~/.ssh/authorized_keys`
- Review running processes for suspicious activity
- Rotate SSH keys if any possibility of compromise

---

## Phase 5 — Recovery

### Actions Taken

| Action | Status |
|---|---|
| Password authentication disabled | ✅ Done |
| SSH hardening verified | ✅ Confirmed via Hydra re-test |
| Monitoring confirmed active | ✅ Alerts still configured |
| VM returned to normal operation | ✅ Done |

### Verification Query Post-Recovery

```kql
Syslog
| where Facility == "auth" or Facility == "authpriv"
| where SyslogMessage contains "Accepted"
| project TimeGenerated, SyslogMessage
| order by TimeGenerated desc
| take 10
```

No unauthorised accepted logins found.

---

## Phase 6 — Post-Incident Activity

### What Worked Well

| Item | Detail |
|---|---|
| Detection speed | Alert fired within minutes of attack start |
| Log fidelity | All 72 attempts captured accurately in Syslog |
| Hardening effectiveness | 0 successful logins despite sustained attack |
| Notification | Email received promptly via Action Group |

### What Could Be Improved

| Improvement | Detail |
|---|---|
| Automatic IP blocking | Could use Azure Logic App to auto-block attacker IP on alert |
| Alert threshold tuning | Set higher threshold (e.g., 10+ attempts) to reduce noise from single failed logins |
| Geo-blocking | Block SSH from countries outside Australia entirely via NSG |
| Microsoft Sentinel | Upgrade to Sentinel for automated SOAR response playbooks |

---

## Recommended Security Improvements

Based on this incident, the following improvements are recommended for a production environment:

**1. Implement Azure Sentinel SOAR Playbook**
Automate containment — when brute force is detected, automatically add a Deny rule to the NSG for the source IP.

**2. Enable Microsoft Defender for Cloud**
Provides built-in brute force detection, JIT (Just-in-Time) VM access, and security recommendations.

**3. Just-in-Time VM Access**
Only open SSH port when explicitly requested, for a limited time window, from a specific IP. Eliminates persistent SSH exposure entirely.

**4. Rate Limiting via fail2ban**
Install `fail2ban` on the Linux VM to automatically block IPs after a configurable number of failed attempts at the OS level.

```bash
sudo apt install fail2ban -y
```

**5. Move to Certificate-Based Authentication Only**
Already implemented — but document and enforce via Azure Policy.

---

## Incident Timeline

| Time (UTC) | Event |
|---|---|
| 11:19 | Hydra brute force attack commenced |
| 11:30 | First auth failure logs appear in Log Analytics |
| 11:30 | Azure Monitor alert fires (14 events detected) |
| 11:30 | Email notification received |
| 11:33 | Hydra completes — 0 successful logins |
| 11:35 | Password authentication re-disabled on VM |
| 11:36 | Hardening verified via Hydra re-test |
| 11:40 | Incident closed — no compromise confirmed |

---

## Conclusion

This incident response exercise demonstrated that the security monitoring pipeline built across Weeks 5 and 6 is effective at detecting, alerting, and enabling rapid response to SSH brute force attacks. The existing hardening controls (disabled password authentication, NSG restrictions) prevented any successful compromise, while the monitoring layer provided full visibility into the attack as it occurred.

> The combination of preventive controls (hardening) and detective controls (monitoring + alerting) is the foundation of a defence-in-depth security posture.

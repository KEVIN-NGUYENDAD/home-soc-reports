# Incidents Repository - Classification Standards

**Repository**: home-soc-reports/incidents/  
**Purpose**: Centralized incident documentation with standardized severity classification  
**Last Updated**: 2026-09-10

---

## 📂 Directory Structure

```
incidents/
├── README.md                    # This file
├── 2026-09/                     # Current month
│   ├── CRITICAL-001-malware-ransomware.md
│   ├── HIGH-002-lateral-movement-smb.md
│   ├── MEDIUM-003-suspicious-download.md
│   └── ...
├── 2026-08/
├── 2026-07/
├── ...
└── templates/                   # (Optional) Incident templates
    ├── malware-template.md
    ├── credential-compromise-template.md
    └── ...
```

---

## 🎯 Severity Classification Matrix

### CRITICAL (Immediate Response Required)

**Definition**: Active threat requiring immediate containment and remediation

**Response Time**: 0-1 hour  
**Escalation**: On-call engineer + Security lead + Management  
**Business Impact**: High (immediate data loss / system compromise risk)

**Examples**:
- ✅ Active ransomware infection
- ✅ Credential compromise of admin/root accounts
- ✅ Active data exfiltration in progress
- ✅ Confirmed APT indicators
- ✅ Zero-day exploitation detected
- ✅ Supply chain compromise confirmed
- ✅ Unauthorized privileged account access

**Investigation Focus**:
1. Immediate containment (isolate affected systems)
2. Preserve evidence (memory dumps, logs)
3. Determine scope (all affected systems)
4. Assess data loss (what was compromised)
5. Initiate recovery (restore from backups)

**Example Filename**:
```
CRITICAL-001-ransomware-lockbit-detected.md
CRITICAL-002-admin-credential-breach-confirmed.md
```

---

### HIGH (Urgent Response - Within 4 Hours)

**Definition**: Suspicious activity indicating likely compromise or attack in progress

**Response Time**: Within 4 hours  
**Escalation**: Team lead + Senior analyst  
**Business Impact**: Medium-High (potential system compromise or data access)

**Examples**:
- ✅ Lateral movement detected (unusual SMB/SSH usage)
- ✅ Persistence mechanism found (registry runkey, scheduled task, service)
- ✅ Credential harvesting attempt (mimikatz patterns, credential dumping)
- ✅ Suspicious code execution (PowerShell downloads, script execution)
- ✅ Unauthorized remote access (RDP from unknown IP, VPN access)
- ✅ Privilege escalation attempt (UAC bypass, token impersonation)
- ✅ Abnormal file access (bulk data download, unusual directory traversal)

**Investigation Focus**:
1. Verify threat indicators (true positive check)
2. Identify affected systems (scope assessment)
3. Trace lateral movement (network analysis)
4. Review event logs (timeline reconstruction)
5. Deploy countermeasures (block attacker, revoke credentials)

**Example Filename**:
```
HIGH-002-lateral-movement-wmiexec-detected.md
HIGH-003-persistence-scheduled-task-malware.md
HIGH-004-privilege-escalation-uac-bypass.md
```

---

### MEDIUM (Standard Response - Within 1 Business Day)

**Definition**: Suspicious activity requiring investigation, but not immediately critical

**Response Time**: Within 1 business day (8 hours)  
**Escalation**: Senior analyst review  
**Business Impact**: Medium (potential security policy violation or reconnaissance)

**Examples**:
- ✅ Suspicious file download (Office macros, script downloads)
- ✅ Failed brute force attempts (multiple failed logins)
- ✅ Policy violation (unapproved software installation, USB usage)
- ✅ Unusual network connection (suspicious IP addresses, C2 domain contact)
- ✅ Browser exploitation attempt (malicious website visit with Defender alert)
- ✅ Email phishing campaign detected (suspicious attachment/link in emails)
- ✅ Antivirus quarantine (potentially malicious file detected)

**Investigation Focus**:
1. Confirm false positive vs. true threat
2. Analyze intent (reconnaissance vs. exploitation)
3. Check for secondary indicators (related activity)
4. User awareness (if social engineering involved)
5. Implement detection rule (prevent similar future incidents)

**Example Filename**:
```
MEDIUM-005-suspicious-powershell-download.md
MEDIUM-006-brute-force-ssh-failed-attempts.md
MEDIUM-007-phishing-email-malicious-attachment.md
```

---

### LOW (Informational - Scheduled Review)

**Definition**: Security-related informational alert or routine activity

**Response Time**: Scheduled review (can be batched)  
**Escalation**: None (informational only)  
**Business Impact**: Low (no immediate security concern)

**Examples**:
- ✅ Software updates available
- ✅ Routine security maintenance notifications
- ✅ Policy compliance reminders
- ✅ User security training recommendations
- ✅ Routine log rotation alerts
- ✅ Informational security advisories
- ✅ Benign user behavior (VPN login, remote access)

**Investigation Focus**:
1. Archive & categorize
2. Aggregate trends (multiple similar alerts)
3. Improve detection rules (reduce noise)
4. User feedback (if training relevant)

**Example Filename**:
```
LOW-008-monthly-patch-tuesday-summary.md
LOW-009-security-training-reminder.md
LOW-010-routine-log-rotation-completed.md
```

---

## 📝 Incident File Naming Convention

### Format
```
SEVERITY-SEQUENCE-CATEGORY-TITLE.md
```

### Components

**SEVERITY**: CRITICAL | HIGH | MEDIUM | LOW  
**SEQUENCE**: 3-digit incident counter for that severity level in current month  
**CATEGORY**: Short category (malware, lateral-movement, credential-theft, etc.)  
**TITLE**: Descriptive title (use hyphens, lowercase)

### Examples
```
CRITICAL-001-ransomware-lockbit-v3-detected.md
HIGH-002-lateral-movement-smb-with-credentials.md
MEDIUM-005-phishing-email-trickbot-attachment.md
LOW-010-windows-update-kb4580391-available.md
```

### Category Reference
```
Malware:
  - ransomware-*
  - trojan-*
  - spyware-*
  - worm-*
  - rootkit-*

Lateral Movement:
  - lateral-movement-smb
  - lateral-movement-ssh
  - lateral-movement-http
  - lateral-movement-dns-tunneling
  - lateral-movement-pass-the-hash

Credential Theft:
  - credential-dumping-lsass
  - credential-harvesting-phishing
  - credential-brute-force-rdp
  - password-spray-attack

Persistence:
  - persistence-registry-runkey
  - persistence-scheduled-task
  - persistence-service-installation
  - persistence-webshell

Privilege Escalation:
  - priv-esc-uac-bypass
  - priv-esc-kernel-exploit
  - priv-esc-sudo-misconfiguration

Data Exfiltration:
  - exfiltration-bulk-download
  - exfiltration-cloud-upload
  - exfiltration-dns-tunneling

Reconnaissance:
  - recon-network-scan
  - recon-port-scan
  - recon-vulnerability-scan

Compliance/Policy:
  - policy-violation-unauthorized-software
  - policy-violation-usb-device
  - compliance-reminder-training
```

---

## 📋 Incident File Template

### Location & Naming
```
incidents/2026-09/HIGH-002-lateral-movement-smb-with-credentials.md
```

### Content Template
```markdown
# HIGH: Lateral Movement Detected - SMB with Credentials

## Incident Information
- **ID**: HIGH-002
- **Severity**: HIGH
- **Category**: Lateral Movement
- **Discovered**: 2026-09-10 14:23 UTC
- **First Seen**: 2026-09-10 09:15 UTC
- **Last Seen**: 2026-09-10 14:23 UTC (ongoing)
- **Status**: IN_PROGRESS
- **Assigned To**: [Analyst name]

## Summary
Suspicious SMB network traffic detected from workstation WKS-042 to file server FS-01 
using harvested credentials. Indicators suggest lateral movement attempt post-compromise.

## Affected Systems
| System | IP | Impact | Notes |
|--------|-----|--------|-------|
| WKS-042 | 192.168.1.105 | SOURCE | Potentially compromised |
| FS-01 | 192.168.1.50 | TARGET | Data exposure risk |
| DC-01 | 192.168.1.10 | MONITORED | Credential validation point |

## Indicators of Compromise (IoCs)

### Network Indicators
- Source IP: 192.168.1.105 (WKS-042)
- Destination IP: 192.168.1.50 (FS-01)
- Protocol: SMBv2/445
- Username: jsmith (harvested from previous phishing)
- Frequency: 47 connection attempts over 5 hours

### File Indicators
- **Hash**: `a1b2c3d4e5f6...` (suspicious executable)
- **File Path**: C:\Users\jsmith\AppData\Roaming\payload.exe
- **Size**: 524 KB
- **Compile Time**: 2026-09-09 12:00 UTC

### Behavioral Indicators
- Abnormal SMB access patterns (night hours, unusual file types)
- Multiple share enumeration attempts
- Access to sensitive shares (HR_Docs, Finance_Data)
- Copy operations on large files (>100 MB)

## Timeline

| Time (UTC) | Event | Source | Severity |
|-----------|-------|--------|----------|
| 09:15 | Initial phishing email received | Email gateway | LOW |
| 09:45 | User clicked malicious link | WKS-042 | HIGH |
| 10:22 | Malware executed locally | WKS-042 | CRITICAL |
| 12:00 | Lateral movement attempt detected | Network IDS | HIGH |
| 14:23 | Incident escalated to SOC | Alert system | HIGH |

## Analysis & Assessment

### Root Cause
Phishing attack → credential harvest → malware execution → lateral movement

### Attack Chain
1. Phishing email with malicious link
2. User clicked link (social engineering)
3. Malware downloaded & executed (WKS-042)
4. Credentials harvested from browser cache
5. SMB access using stolen credentials (FS-01 target)

### Threat Assessment
- **Threat Actor**: Unattributed (likely opportunistic)
- **TTPs**: Phishing, credential theft, lateral movement (Mitre ATT&CK: T1566, T1110, T1570)
- **Motivation**: Financial gain (ransomware staging likely)
- **Confidence**: HIGH (multiple indicators aligned)

## Actions Taken

### Immediate Response (0-2 hours)
- [x] Isolated affected systems from network
- [x] Killed malicious process (payload.exe)
- [x] Captured memory dump (forensics)
- [x] Collected network traffic (pcap files)
- [x] Preserved logs (security event log, SMB logs)

### Investigation Phase (2-4 hours)
- [x] Analyzed malware sample (sandbox analysis)
- [x] Determined credential source (browser cache)
- [x] Traced lateral movement scope (3 shares accessed)
- [x] Checked other systems for indicators
- [ ] Assess if ransomware dropped (IN PROGRESS)

### Containment Phase (4-8 hours)
- [x] Reset compromised user password (jsmith)
- [x] Invalidate all user sessions (force re-authentication)
- [x] Block attacker IP at firewall
- [x] Disable SMB access for compromised user temporarily
- [ ] Audit file access logs (FS-01) for data loss assessment

## Evidence & Artifacts

### Evidence Files
- **Memory Dump**: /evidence/WKS-042-20260910-memory.dump (4.2 GB)
- **Network Capture**: /evidence/WKS-042-20260910-network.pcap (156 MB)
- **Event Logs**: /evidence/WKS-042-20260910-security-events.evtx
- **Malware Sample**: /evidence/payload.exe (MD5: a1b2c3d4...)
- **File Server Logs**: /evidence/FS-01-20260910-smb-audit.csv

### Analysis Results
- Sandbox Malware Analysis: Confirmed ransomware variant (LockBit 3.0)
- Volatility Memory Analysis: 2 persistence mechanisms found
- Wireshark Network Analysis: C2 communication to 185.220.100.* detected

## Playbook Executed

**Playbook**: `/playbooks/lateral-movement-response.md`  
**Version**: v2.3  
**Status**: FOLLOWING PROCEDURE

### Playbook Steps Completed
1. [x] Verify alert (true positive confirmation)
2. [x] Isolate systems (network segmentation)
3. [x] Capture evidence (forensic preservation)
4. [x] Analyze malware (behavioral assessment)
5. [x] Reset credentials (deny attacker access)
6. [ ] Restore from backup (data integrity check) - NEXT

## Escalation & Approval

**Initial Escalation**: SOC Analyst → Team Lead (14:45 UTC)  
**Current Owner**: [Senior Analyst name]  
**Approval Status**: APPROVED for remediation (15:10 UTC)

## Next Steps

1. [ ] Complete data loss assessment (FS-01 audit)
2. [ ] Confirm ransomware staging (scan for encryption keys)
3. [ ] Restore critical files from backup
4. [ ] Validate system integrity (clean boot & verification)
5. [ ] User security awareness training (phishing focus)
6. [ ] Update detection rules (prevent similar incidents)
7. [ ] Perform root cause review (process improvement)

## Resolution

**Status**: OPEN (In remediation)  
**Estimated Resolution**: 2026-09-11 10:00 UTC  
**Owner**: [Security team member]

---

## Comments & Notes

### Analyst 1 (2026-09-10 15:00)
Memory analysis shows T1036 (masquerading) - malware hiding process name. Persistence very likely.

### Analyst 2 (2026-09-10 16:30)
FS-01 logs show access to Finance_Data share. Approximately 2.3 GB copied. Escalating to CRITICAL.

### Security Lead (2026-09-10 17:00)
Approved full remediation. Budget approved for external forensics if needed. Keep on high alert for ransomware execution.

---

**Incident Created**: 2026-09-10 14:23 UTC  
**Last Updated**: 2026-09-10 17:00 UTC  
**Created By**: [Analyst name]
```

---

## ✅ Approval Workflow

### For CRITICAL Incidents
```
Discovered → Analyst Review → Team Lead Approval → Execution → Documentation
```

### For HIGH Incidents
```
Discovered → Analyst Review → Senior Analyst Approval → Execution → Documentation
```

### For MEDIUM Incidents
```
Discovered → Analyst Review → Documentation (inline approval)
```

### For LOW Incidents
```
Discovered → Batch Daily Review → Archive (weekly summary)
```

---

## 🔗 Integration with mcp-cyber-tools

### Auto-Generated Incidents
When mcp-cyber-tools exports case data:

```json
{
  "case_id": "case-2026-09-10-001",
  "severity": "HIGH",
  "title": "Lateral Movement Detected",
  "created_at": "2026-09-10T14:23:00Z",
  "export_path": "incidents/2026-09/HIGH-002-lateral-movement-smb.md"
}
```

The case is automatically converted to an incident file using the template above.

---

## 📊 Incident Statistics

### Current Month (2026-09-10)
- **CRITICAL**: 1 incident
- **HIGH**: 3 incidents  
- **MEDIUM**: 8 incidents
- **LOW**: 15 incidents
- **Total**: 27 incidents
- **Resolution Rate**: 89% (resolved within SLA)
- **Avg MTTD**: 6.2 hours
- **Avg MTTR**: 3.4 hours

---

## 🔗 Related Documents

- **CLAUDE.md** - Analyst context guide
- **PROJECT_STATE.md** - Current operations status
- **ROADMAP.md** - Feature development plan
- `/playbooks/` - Incident response procedures

---

**Document Version**: v1.0  
**Last Updated**: 2026-09-10  
**Owner**: Kevin (Tam) Nguyen - SOC Analyst

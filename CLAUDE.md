# CLAUDE.md - home-soc-reports Context Guide

## 🔍 Vai trò và Phạm vi

**Project**: Home SOC Operations & Incident Management  
**Vai trò**: SOC Analyst / DFIR Specialist  
**Mục tiêu**: Tập trung hóa quản lý sự cố, phân tích log an ninh, tạo báo cáo hàng ngày cho Home Security Operations Center.

---

## 🏗️ Cấu trúc Dự Án

```
home-soc-reports/
├── README.md                    # Project overview
├── CLAUDE.md                    # This file - context guide
├── PROJECT_STATE.md             # Current status & metrics
├── ROADMAP.md                   # Feature roadmap
│
├── incidents/                   # Centralized incident repository
│   ├── README.md               # Severity & classification standards
│   ├── 2026-09/                # Monthly folders
│   │   ├── incident-001-malware.md
│   │   ├── incident-002-suspicious-login.md
│   │   └── incident-003-network-scan.md
│   ├── 2026-08/
│   └── ...
│
├── daily-reports/              # Daily security briefings
│   ├── 2026-09-10.md
│   ├── 2026-09-09.md
│   └── ...
│
├── playbooks/                  # Incident response procedures
│   ├── malware-response.md
│   ├── credential-compromise.md
│   └── ...
│
├── alert-rules/                # Alert configuration & tuning
│   ├── critical-alerts.yaml
│   ├── false-positive-filters.yaml
│   └── ...
│
├── statistics/                 # KPI tracking & metrics
│   ├── monthly-summary-2026-09.md
│   ├── trends.csv
│   └── ...
│
└── archive/                    # Resolved cases (older than 6 months)
    └── 2026-Q1-Q2/
```

---

## 📋 Quy ước Phân Loại Sự Cố (Severity Standards)

### Severity Levels
```yaml
CRITICAL:
  Response Time: Immediate (0-1 hour)
  Escalation: On-call + Team lead
  Examples: 
    - Active malware infection
    - Credential compromise (admin accounts)
    - Active data exfiltration
    - Ransomware detected
  
HIGH:
  Response Time: Within 4 hours
  Escalation: Team lead
  Examples:
    - Suspicious lateral movement
    - Unauthorized access (user accounts)
    - Persistence mechanisms detected
    - Abnormal data access patterns

MEDIUM:
  Response Time: Within 1 business day
  Escalation: Senior analyst review
  Examples:
    - Suspicious downloads
    - Failed brute force attempts
    - Policy violations
    - Suspicious network connections

LOW:
  Response Time: Scheduled review
  Escalation: Information only
  Examples:
    - Software updates
    - User training recommendations
    - Routine maintenance alerts
    - Informational security notices
```

### Incident File Naming
```
SEVERITY-SEQUENCE-CATEGORY-TITLE.md

Examples:
- CRITICAL-001-malware-ransomware-detected.md
- HIGH-002-lateral-movement-suspicious-smb.md
- MEDIUM-003-suspicious-download-office-macro.md
- LOW-004-policy-violation-unapproved-software.md
```

---

## 📝 Daily Report Format

### Location
`daily-reports/YYYY-MM-DD.md`

### Template
```markdown
# Daily Security Report - YYYY-MM-DD

## 📊 Summary
- Total Alerts: N
- Critical: N | High: N | Medium: N | Low: N
- Incidents Resolved: N
- New Incidents: N

## 🚨 Critical/High Incidents

### Incident: [ID] [Title]
- **Severity**: CRITICAL/HIGH
- **Status**: Open/In-Progress/Resolved
- **First Seen**: YYYY-MM-DD HH:MM
- **Last Seen**: YYYY-MM-DD HH:MM
- **Description**: [Brief summary]
- **Action Taken**: [Steps taken]
- **Next Steps**: [Follow-up items]

## ✅ Resolved Today
- [incident-001]
- [incident-002]

## 📈 Metrics
- Mean Time to Detect (MTTD): X hours
- Mean Time to Respond (MTTR): X hours
- False Positive Rate: X%

## 📞 Escalations
None / [List as needed]

## 🔔 Alerts to Watch
- [Upcoming system maintenance]
- [Expected activity]

---
*Generated: 2026-09-10 09:00 UTC*
```

---

## 🛠️ Lệnh Làm Việc Hằng Ngày (Common Tasks)

### Tạo báo cáo hàng ngày
```bash
# 1. Create today's report from template
cp templates/daily-report-template.md daily-reports/$(date +%Y-%m-%d).md

# 2. Add incident summaries
# - Review last 24 hours of alerts
# - Document critical/high severity
# - Resolve if applicable

# 3. Commit changes
git add daily-reports/
git commit -m "[REPORT] Daily security report $(date +%Y-%m-%d)"
git push origin develop
```

### Ghi nhận sự cố mới
```bash
# 1. Create incident file
SEVERITY="CRITICAL"
SEQUENCE="001"
TITLE="malware-detected"
touch "incidents/2026-09/${SEVERITY}-${SEQUENCE}-${TITLE}.md"

# 2. Fill incident template
# - Title, severity, discovery date
# - Indicators of compromise (IoCs)
# - Systems affected
# - Initial assessment
# - Response actions

# 3. Commit & notify team
git add incidents/
git commit -m "[INCIDENT] $SEVERITY: $TITLE"
git push origin develop
# Send Slack notification to #security-team
```

### Phân tích log & sự cố
```bash
# 1. Collect evidence from mcp-cyber-tools
python -m sentinelops.cli investigate --case-id <CASE_ID> --export-to incidents/

# 2. Generate analysis report
# - Timeline of events
# - Affected systems
# - Threat actor indicators
# - Recommendations

# 3. Link to playbook & execute
# Reference: incidents/README.md for playbook links
```

---

## 🔐 Security Policies

### Data Handling
- All incident data must be classified (PUBLIC, INTERNAL, CONFIDENTIAL)
- Sensitive data (IP addresses, hashes) allowed, but passwords/tokens prohibited
- All PDFs/attachments must be scanned before adding
- GDPR compliance: PII handling requires special notation

### Incident Retention
- **Active Incidents**: Kept in `incidents/YYYY-MM/`
- **Resolved**: Move to `archive/` after 6 months
- **Confidential**: Encrypt sensitive cases
- **Purge Schedule**: 12 months for INTERNAL data, 7 years for CRITICAL

### Access Control
- Pull requests required for all changes
- Review by at least one senior analyst
- No direct commits to `main` or `develop`

---

## 🔗 Integration with mcp-cyber-tools

### Workflow
```
1. Alert triggered (mcp-cyber-tools)
   ↓
2. Investigation automated (MCP engine)
   ↓
3. Case exported → incidents/
   ↓
4. Analyst reviews & approves (home-soc-reports)
   ↓
5. Playbook executed (mcp-cyber-tools)
   ↓
6. Resolution logged → archive/
```

### Data Format
- Export format: JSON (structured evidence) + Markdown (human-readable)
- Timestamp: ISO 8601 (UTC)
- Evidence links: Relative paths within incidents/

---

## 📞 Escalation & Support

**New Security Alert?**  
→ Create issue in home-soc-reports with `[ALERT]` tag

**Need DFIR Analysis?**  
→ Submit case to mcp-cyber-tools with evidence files

**Playbook Missing?**  
→ PR to `playbooks/` with test results

**Question on Severity?**  
→ See `incidents/README.md` severity matrix

---

## 🔗 Related Resources

- Architecture: Integrated with mcp-cyber-tools engine
- Playbooks: `/playbooks/` directory (procedures for each incident type)
- Metrics: `/statistics/` for KPI tracking
- Archive: `/archive/` for historical reference

---

**Last Updated**: 2026-09-10  
**Maintainer**: Kevin (Tam) Nguyen - SOC Analyst

# Home SOC Operations & Incident Management

**Project**: Centralized incident documentation, daily security operations, and automated playbooks  
**Status**: 🟢 ACTIVE (v1.0) | **Owner**: Kevin (Tam) Nguyen  
**Integration**: Powered by [mcp-cyber-tools](https://github.com/KEVIN-NGUYENDAD/mcp-cyber-tools)

---

## 🎯 Purpose

This repository is the **operational hub for Home Security Operations Center (SOC)**. It serves as:
- 📋 **Incident Registry**: Centralized documentation of all security incidents with standardized classification
- 📊 **Daily Operations**: Automated security briefings and status reports
- 📚 **Playbook Library**: Reusable incident response procedures
- 🔍 **Investigation Records**: Forensic evidence and timeline documentation

---

## 📂 Repository Structure

```
home-soc-reports/
├── README.md                    # This file
├── CLAUDE.md                    # Context guide for analysts
├── PROJECT_STATE.md             # Current status & metrics
├── ROADMAP.md                   # Feature development plan
│
├── incidents/                   # CENTRALIZED INCIDENT REPOSITORY
│   ├── README.md               # Severity classification standards
│   ├── 2026-09/                # Monthly folders
│   │   ├── CRITICAL-001-*.md
│   │   ├── HIGH-002-*.md
│   │   ├── MEDIUM-005-*.md
│   │   └── LOW-010-*.md
│   ├── 2026-08/
│   └── ...
│
├── daily-reports/              # Daily security briefings (auto-generated)
│   ├── 2026-09-10.md
│   ├── 2026-09-09.md
│   └── ...
│
├── playbooks/                  # Incident response procedures (40+ templates)
│   ├── malware-response.md
│   ├── credential-compromise.md
│   ├── lateral-movement-response.md
│   └── ...
│
├── alert-rules/                # Alert tuning & configuration
│   ├── critical-alerts.yaml
│   └── false-positive-filters.yaml
│
├── statistics/                 # KPI tracking & metrics
│   ├── monthly-summary-2026-09.md
│   ├── trends.csv
│   └── ...
│
└── archive/                    # Resolved cases (>6 months old)
    └── 2026-Q1-Q2/
```

---

## 🚀 Quick Start

### For Analysts
1. **New Security Alert?** → Create issue in `incidents/` with severity tag
2. **Investigate Incident?** → Review playbook in `playbooks/` matching incident type
3. **Document Finding?** → Add entry to `incidents/YYYY-MM/` using severity standards
4. **Track Progress?** → Update daily report in `daily-reports/`

### For DevOps/Automation
1. **Daily Report Generation** → `daily-reports/` (automated, 07:00 UTC daily)
2. **Incident Export** → JSON from mcp-cyber-tools → `incidents/` (auto-import)
3. **Playbook Sync** → Update from centralized library

---

## 🎯 Integration with mcp-cyber-tools

**Workflow**:
```
mcp-cyber-tools (Investigation)     home-soc-reports (Operations)
  Case Engine ──JSON export────→   Incident File
                                   Analyst Review
  Playbook ←──────Approval─────── Decision & Action
  Execution                       Documentation
```

---

## 📊 Incident Classification

Incidents are classified by **SEVERITY**:

| Severity | Response Time | Examples |
|----------|---------------|----------|
| **CRITICAL** | 0-1 hour | Ransomware, admin account breach, active data exfiltration |
| **HIGH** | Within 4 hours | Lateral movement, persistence detected, privilege escalation |
| **MEDIUM** | Within 1 day | Suspicious download, brute force attempts, policy violations |
| **LOW** | Scheduled | Software updates, training reminders, routine alerts |

→ **Full standards**: See `incidents/README.md`

---

## 📋 Files Overview

### Context & Documentation
- **CLAUDE.md** - Analyst context guide, daily procedures
- **PROJECT_STATE.md** - Current KPI metrics, known issues, next steps
- **ROADMAP.md** - v1.0 (current), v1.1 (automation), v2.0 (dashboard), v2.1+ (AI)

### Incident Management
- **incidents/README.md** - Severity matrix, naming conventions, templates
- **incidents/YYYY-MM/** - Organized by month, files named `SEVERITY-SEQ-CATEGORY-TITLE.md`

### Operations & Reporting
- **daily-reports/** - Automated daily security briefings
- **playbooks/** - 40+ incident response procedures
- **statistics/** - KPI tracking (MTTD, MTTR, false positive rate)

### Archive
- **archive/** - Resolved incidents >6 months old (for historical reference)

---

## 🔐 Security & Data Handling

### Sensitivity Classification
- **PUBLIC**: General summaries (shareable)
- **INTERNAL**: Team-only documentation
- **CONFIDENTIAL**: Sensitive incidents (encrypted)

### Data Retention Policy
- **Active**: Incidents in `incidents/YYYY-MM/` for 6 months
- **Archive**: Move to `archive/` after 6 months
- **Purge**: Delete INTERNAL after 12 months, CRITICAL after 7 years

### No Secrets Policy
❌ **Never store**: Passwords, API keys, tokens, credit cards, PII  
✅ **Always safe**: Hashes, IP addresses (internal/external), incident categories

---

## 📈 Key Metrics (v1.0)

| Metric | Current | Target |
|--------|---------|--------|
| Avg MTTD (Mean Time to Detect) | 6-12 hrs | <2 hrs |
| Avg MTTR (Mean Time to Respond) | 2-8 hrs | <1 hr |
| False Positive Rate | 25-30% | <10% |
| Playbook Coverage | 40% | 90% |

→ **Full metrics**: See `PROJECT_STATE.md`

---

## 🔄 Workflow Examples

### Creating a New Incident
```bash
# 1. Discover alert
# 2. Create incident file
touch incidents/2026-09/HIGH-002-lateral-movement-smb.md

# 3. Fill template (see incidents/README.md for details)
# 4. Commit & push
git add incidents/2026-09/
git commit -m "[INCIDENT] HIGH: Lateral movement detected - SMB activity"
git push origin develop
```

### Generating Daily Report
```bash
# Automated: Daily at 07:00 UTC
# Manual: 
bash scripts/generate-daily-report.sh
```

### Executing Playbook
```bash
# 1. Review incident
# 2. Match to playbook (e.g., playbooks/lateral-movement-response.md)
# 3. Follow steps & document in incident file
# 4. Mark resolved when complete
```

---

## 🔗 Related Resources

- **[mcp-cyber-tools](https://github.com/KEVIN-NGUYENDAD/mcp-cyber-tools)** - Core investigation engine
- **[MASTER_REPOSITORY_INDEX.md](https://github.com/KEVIN-NGUYENDAD/mcp-cyber-tools/blob/develop/MASTER_REPOSITORY_INDEX.md)** - Ecosystem overview
- **[SentinelOps Homepage](https://github.com/KEVIN-NGUYENDAD/sentinelops-homepage)** - Project portfolio

---

## 📞 Support & Escalation

**Issue with an incident?**  
→ Open GitHub Issue with `[INCIDENT]` tag + attach evidence

**Need playbook updated?**  
→ Submit PR to `playbooks/` with test results

**Performance problem?**  
→ Contact: Kevin (Tam) Nguyen (Security Architect)

---

**Status**: 🟢 ACTIVE (v1.0)  
**Last Updated**: 2026-09-10  
**Next Review**: 2026-10-10

---

## How it works

Every file in this repo is written by `export-home-soc-reports.js`, which lives in the
private repo. Nothing here is edited by hand.

```
PRIVATE  mcp-cyber-tools
┌──────────────────────────────────────────────┐
│  network-scan-data/network-scan-*.json       │  device inventory, open ports
│  laptop-collection-data/*.json               │  DNS, WiFi, host state
│  baseline/BASELINE-*.json                    │  approved baseline
│  state.json + baseline.json  (optional)      │  security-watch control states
└──────────────────────────────────────────────┘
                     │  newest of each type
                     ▼
        export-home-soc-reports.js
                     │
                     ├── classify   addresses → link type
                     │              MAC       → device id  (gateway-01, camera-01)
                     │              vendor    → discarded
                     │              model/fw  → discarded
                     │              port      → service class (web-ui, video-stream…)
                     │              resolvers → provider class (isp_default…)
                     │
                     ├── derive     alerts from control changes + LAN remote-access
                     │              risk level GREEN / YELLOW / RED
                     │              data_age_hours + stale flag
                     │
                     └── LEAK GUARD  regex sweep over the exact output bytes
                                     MAC · IPv4 · IPv6 · credential keywords ·
                                     private-key blocks · vendor names · SSID
                                     any hit → abort, write nothing, push nothing
                     │
                     ▼
PUBLIC  home-soc-reports
┌──────────────────────────────────────────────┐
│  ROUTER-SECURITY-AUDIT-LATEST.md             │
│  BASELINE-LATEST.json                        │
│  DEVICE-SUMMARY.json                         │
└──────────────────────────────────────────────┘
                     │  git add -f · commit · push origin main
                     ▼
        Claude Scheduled Task — daily 20:10
        fetches the three raw.githubusercontent.com URLs
                     │
                     ▼
            🏠 Home Security Bulletin  →  Email
```

**Two properties worth knowing:**

*Unknown is reported as unknown.* A control with no collector output is published as
`state: "unknown"` and shown as `NO DATA` in the audit, never as a pass. The bulletin
therefore cannot mistake a coverage gap for a clean result.

*The leak guard is a gate, not a filter.* It does not scrub — it aborts. If any output
byte still matches an identifier pattern, the export stops before writing and before
pushing. A partial or half-sanitized publish is not reachable.

The private repo keeps the full, unsanitized data and all tooling. Only the projection
lands here.

---

## Raw URLs used by the scheduled task

```
https://raw.githubusercontent.com/KEVIN-NGUYENDAD/home-soc-reports/main/ROUTER-SECURITY-AUDIT-LATEST.md
https://raw.githubusercontent.com/KEVIN-NGUYENDAD/home-soc-reports/main/BASELINE-LATEST.json
https://raw.githubusercontent.com/KEVIN-NGUYENDAD/home-soc-reports/main/DEVICE-SUMMARY.json
```

---

## Freshness contract

Every file carries a timestamp (`generated_at` / `approved_at` / audit date).
If the newest timestamp is more than **48 hours** old, the bulletin must report
`Dữ liệu cũ — collector có thể đã dừng` rather than presenting stale state as current.

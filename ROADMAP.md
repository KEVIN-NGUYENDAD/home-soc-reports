# ROADMAP.md - home-soc-reports Feature Roadmap

**Project**: Home SOC Operations & Incident Management  
**Planning Horizon**: 2026-2027  
**Last Updated**: 2026-09-10

---

## 📅 Release Timeline

```
2026-Q3 (CURRENT)        2026-Q4           2027-Q1+
├─ v1.0 STABLE          ├─ v1.1 ADVANCED  └─ v2.0+ INTEGRATION
│  (Core foundation)    │  (Automation)       (Dashboard + AI)
└─ Incident repo        └─ ML automation
```

---

## 🎯 Version Roadmap

### ✅ v1.0 - STABLE Foundation (2026-08 to 2026-09) **CURRENT**

**Focus**: Centralized incident repository, daily reports, playbook library

**Features Delivered**:
- [x] Incident repository with YYYY-MM/ structure
- [x] Severity classification (CRITICAL, HIGH, MEDIUM, LOW)
- [x] Daily automated security reports
- [x] Playbook library (40+ procedures)
- [x] Alert routing & triage framework
- [x] Evidence aggregation & linking
- [x] Timeline tracking (first seen, last seen, resolved)
- [x] Archive system (6-month auto-archival)

**Test Coverage**: 80%+ documentation validation  
**Docs**: README.md, CLAUDE.md, PROJECT_STATE.md (new)

**Known Gaps**:
- Manual false positive filtering
- No alert automation
- Limited trend analysis

---

### 🔄 v1.1 - ADVANCED Automation (2026-10 to 2026-11) **PLANNED**

**Focus**: Integration with mcp-cyber-tools, automate common workflows

**Planned Features**:
- [ ] Automated case export → incident import (JSON pipeline)
- [ ] Alert de-duplication & correlation
- [ ] False positive filtering (ML-based or rule-based)
- [ ] Playbook auto-suggestion based on incident type
- [ ] Batch incident analysis (process 20+ incidents/day)
- [ ] KPI dashboard (MTTD, MTTR, FP rate trending)
- [ ] Slack integration (daily digest, incident notifications)
- [ ] Automated playbook execution trigger
- [ ] Historical trend analysis & anomaly detection

**Integration Requirements**:
- ✅ mcp-cyber-tools v1.2 accuracy gate ≥90%
- ✅ Event-sourced case output in JSON format
- ✅ Approval workflow integration

**Success Criteria**:
```
✓ Incident processing time: <30 min (vs. 2 hours manual)
✓ Alert automation coverage: ≥60% of incident types
✓ False positive reduction: 30% → <10%
✓ Daily reports: <5 min generation (vs. 30 min)
✓ Playbook execution rate: ≥80% of recommendations
```

**Release Date**: Early December 2026 (depends on v1.2 gate)

---

### 🚀 v2.0 - INTEGRATION Dashboard (2027-01+) **BLOCKED UNTIL v1.1**

**Prerequisites**: 
- ✅ v1.1 automation complete
- ✅ mcp-cyber-tools v1.2 accuracy gate ≥90%
- ✅ 3 months operational stability

**Focus**: Visual dashboards, team collaboration, advanced analytics

**Planned Features**:
- [ ] React dashboard (real-time incident visualization)
- [ ] KPI trending graphs (MTTD, MTTR, severity distribution)
- [ ] Incident timeline visualization (interactive)
- [ ] Team collaboration (comments, assignments, tags)
- [ ] Advanced search & filtering
- [ ] Custom alert rule builder (UI)
- [ ] SIEM integration (Splunk, ELK connectors)
- [ ] Threat intelligence enrichment (automatic)
- [ ] Playbook builder (visual workflow)
- [ ] Mobile app (incident view on-the-go)

**Estimated Dev Time**: 12-16 weeks (if all dependencies met)

---

### 🌐 v2.1+ - AI-DRIVEN Analytics (2027-Q2+) **CONTINGENT**

**Prerequisites**: ✓ v2.0 production + 6+ months stability

**Planned Features**:
- [ ] ML-based incident classification (auto-tagging)
- [ ] Threat actor attribution (pattern matching)
- [ ] Predictive incident forecasting
- [ ] Automated playbook generation (from attack patterns)
- [ ] Anomaly detection (behavioral baseline)
- [ ] Supply chain risk assessment
- [ ] Industry-specific compliance tracking (PCI, HIPAA, etc.)

---

## 📊 Feature Priority Matrix

| Feature | v1.0 | v1.1 | v2.0 | v2.1+ | Priority |
|---------|------|------|------|-------|----------|
| Incident Repository | ✅ | ✅ | ✅ | ✅ | CRITICAL |
| Daily Reports | ✅ | 🔄 | 🔄 | ✅ | CRITICAL |
| Playbook Library | ✅ | 🔄 | 🔄 | ✅ | HIGH |
| Alert Automation | ❌ | 🔄 | ✅ | ✅ | HIGH |
| KPI Dashboard | ❌ | 🔄 | ✅ | ✅ | HIGH |
| Team Collaboration | ❌ | ❌ | 🔄 | ✅ | MEDIUM |
| AI Classification | ❌ | ❌ | ❌ | 🔄 | MEDIUM |
| SIEM Integration | ❌ | ❌ | 🔄 | ✅ | MEDIUM |
| Mobile App | ❌ | ❌ | 🔄 | ✅ | LOW |

**Legend**: ✅ Done | 🔄 In Progress | ❌ Backlog

---

## 🎲 Backlog (Prioritized)

### P0 - BLOCKING (v1.1 release)
```
[ ] Consolidate sentinelops-security-incidents → incidents/
[ ] Create incidents/README.md with standards
[ ] Test JSON export from mcp-cyber-tools
[ ] Validate alert de-duplication logic
```

### P1 - HIGH (v1.1 target)
```
[ ] Implement ML-based false positive filter
[ ] Automate playbook suggestion
[ ] KPI calculation engine
[ ] Slack integration (notifications)
[ ] Expand playbook library (60+ procedures)
```

### P2 - MEDIUM (v2.0 candidate)
```
[ ] React dashboard components
[ ] SIEM connectors
[ ] Advanced search UI
[ ] Team collaboration features
[ ] Threat intelligence enrichment
```

### P3 - LOW (v2.1+ or backlog)
```
[ ] Mobile app development
[ ] Supply chain risk module
[ ] Automated playbook generation
[ ] Predictive forecasting
```

---

## 🚦 Gate Criteria & Milestones

### GATE 1: v1.1 Automation Readiness (PENDING - 2026-10)
**Status**: 🟡 PLANNED (awaiting mcp-cyber-tools v1.2)

**Requirements**:
```
✓ mcp-cyber-tools v1.2 accuracy ≥90% (from mcp-cyber-tools)
✓ Case export JSON schema validated
✓ Alert automation covers ≥60% of incidents
✓ False positive filter accuracy ≥90%
✓ Daily report generation <5 minutes
✓ Playbook suggestions tested with 50+ cases
✓ Zero data loss in case import/export
```

**Timeline**: 2026-10 to 2026-11 (depends on mcp-cyber-tools)  
**Owner**: Kevin (Tam) Nguyen + SOC team

---

### GATE 2: v2.0 Dashboard Readiness (AFTER GATE 1)
**Status**: 🔴 BLOCKED (depends on v1.1)

**Requirements**:
```
✓ v1.1 automation gate passed
✓ Dashboard UI fully tested
✓ SIEM integrations validated
✓ Team feedback incorporated
✓ Performance benchmarks met (<2s page load)
✓ Mobile responsiveness verified
```

**Estimated Date**: Early 2027 (if all dependencies met)

---

## 📈 Success Metrics by Release

### v1.0 Baseline
- Incident documentation: 150+ cases
- Playbook coverage: 40+ procedures
- Daily reports: 30+ generated
- Team efficiency: +15% (anecdotal)

### v1.1 Target
- Processing time: 2 hours → <30 min (-75%)
- Alert automation: 0% → ≥60% coverage
- False positive rate: 25-30% → <10% (-70%)
- Report generation: 30 min → <5 min (-83%)
- Playbook execution: Manual → 80% automated

### v2.0 Target
- Dashboard adoption: 100% team usage
- KPI trend visibility: +40% decision speed
- Team collaboration: Comments on 70%+ incidents
- Advanced analytics: Predictive alerts working

### v2.1+ Target
- ML classification accuracy: >95%
- Automated playbook generation: 30% coverage
- Threat actor attribution: 60% accuracy
- Compliance tracking: 4+ frameworks

---

## 📝 Known Constraints

### ⛓️ Hard Constraints
- **NO AI-driven features** until v1.2 accuracy gate passed (90%+)
- **NO autonomous response** without human approval
- **NO sensitive data exposure** (GDPR compliance required)
- **NO breaking changes** after v1.0 public release

### ⚠️ Risk Areas
- **Data consistency** across mcp-cyber-tools export/import
- **Performance at scale** (1000+ daily incidents)
- **Alert de-duplication** false negatives
- **Playbook execution** error handling

---

## 🔗 Dependencies

### External
- ✅ **mcp-cyber-tools** v1.1.1 (current) → v1.2 (pending)
- ⏳ **GitHub API** (for automation)
- ⏳ **Slack API** (for notifications, v1.1)
- ⏳ **SIEM platforms** (Splunk, ELK, v2.0)

### Internal
- ✅ sentinelops-security-incidents (to consolidate)
- ✅ Existing playbook library (40+ procedures)
- ✅ Daily report templates

---

## 🔗 Related Documents

- **PROJECT_STATE.md** - Current status details
- **CLAUDE.md** - Context guide
- **MASTER_REPOSITORY_INDEX.md** - Ecosystem overview
- **/incidents/README.md** - Severity standards (to create)

---

**Next Review Date**: 2026-10-10  
**Owner**: Kevin (Tam) Nguyen - SOC Analyst  
**Last Modified**: 2026-09-10

---
title: Team Health Report
type: report
version: 1.0
created: 2025-12-12
tags: [report, team, health, culture, performance]
---

# Team Health Report

**Team**: {{TEAM_NAME}}
**Reporting Period**: {{START_DATE}} to {{END_DATE}}
**Prepared by**: {{AUTHOR}}
**Date**: {{DATE}}

## Executive Summary

### Team Overview

| Metric | Current | Target | Status |
|--------|---------|--------|--------|
| **SRE Maturity Level** | Level _____ | Level _____ | 🟢/🟡/🔴 |
| **Services Owned** | _____ | - | - |
| **Incident Load** | _____ /month | <5 | 🟢/🟡/🔴 |
| **On-Call Load** | _____ pages/week | <10 | 🟢/🟡/🔴 |
| **Toil Ratio** | ____% | <30% | 🟢/🟡/🔴 |

### Health Score

**Overall Team Health**: _____/100 (🟢 Healthy / 🟡 At Risk / 🔴 Needs Attention)

**Key Strengths**:
1. _____
2. _____
3. _____

**Areas for Improvement**:
1. _____
2. _____
3. _____

---

## 1. Service Portfolio Health

### 1.1 Services Owned

**Query**:
```
search_datadog_services(query="team:{{TEAM_NAME}}")
```

| Service | Tier | Status | Incidents | Error Rate | SLO |
|---------|------|--------|-----------|------------|-----|
| | T_____ | 🟢/🟡/🔴 | _____ | ____% | ____%  |
| | T_____ | 🟢/🟡/🔴 | _____ | ____% | ____% |
| | T_____ | 🟢/🟡/🔴 | _____ | ____% | ____% |

**Total Services**: _____
- Tier 0 (Critical): _____
- Tier 1 (Core): _____
- Tier 2 (Supporting): _____
- Tier 3 (Non-critical): _____

### 1.2 Service Maturity

**Monitoring Coverage**:
```
search_datadog_monitors(query="team:{{TEAM_NAME}}")
```

| Service | Monitors | Coverage | Alert Quality |
|---------|----------|----------|---------------|
| | _____ | ____% | _____/10 |
| | _____ | ____% | _____/10 |

**Overall Monitoring Score**: _____/10

**Gaps**:
- Services without monitors: _____
- Services without dashboards: _____
- Services without runbooks: _____

### 1.3 Technical Debt

| Service | Debt Type | Severity | Impact | Plan |
|---------|----------|----------|--------|------|
| | [Architecture/Code/Infrastructure] | H/M/L | _____ | _____ |
| | [Architecture/Code/Infrastructure] | H/M/L | _____ | _____ |

**Total Debt Items**: _____
- High severity: _____
- Medium severity: _____
- Low severity: _____

---

## 2. Team Performance

### 2.1 Incident Response

**Query team incidents**:
```
search_datadog_incidents(
  query="team:{{TEAM_NAME}}",
  from="now-30d"
)
```

| Metric | This Period | Last Period | Change | Target |
|--------|------------|-------------|--------|--------|
| Total Incidents | _____ | _____ | +/- _____ | <5 |
| SEV-1 Incidents | _____ | _____ | +/- _____ | 0 |
| MTTD | _____ min | _____ min | +/- _____ | <5min |
| MTTR | _____ min | _____ min | +/- _____ | <30min |

**Incident Trend**: ↑ Increasing / → Stable / ↓ Decreasing

**Top 3 Incident Causes**:
1. _____ (_____ incidents)
2. _____ (_____ incidents)
3. _____ (_____ incidents)

### 2.2 On-Call Metrics

**Data Source**: PagerDuty/On-call platform

| Metric | This Period | Last Period | Change |
|--------|------------|-------------|--------|
| Total Pages | _____ | _____ | +/- _____ |
| Pages/Week | _____ | _____ | +/- _____ |
| After-Hours Pages | _____ | _____ | +/- _____ |
| False Positives | ____% | ____% | +/- ____% |
| Avg Response Time | _____ min | _____ min | +/- _____ |

**On-Call Health**: 🟢 Healthy / 🟡 Moderate / 🔴 Overloaded

**Concerns**:
- [ ] Too many pages (>10/week)
- [ ] Too many after-hours pages (>5/week)
- [ ] High false positive rate (>20%)
- [ ] Slow response times (>5 min)

### 2.3 Toil Analysis

**Time Allocation**:
| Activity | Hours/Week | % of Time | Target | Status |
|----------|-----------|-----------|--------|--------|
| Incident Response | _____ | ____% | <20% | 🟢/🟡/🔴 |
| On-Call | _____ | ____% | <10% | 🟢/🟡/🔴 |
| Manual Operations | _____ | ____% | <20% | 🟢/🟡/🔴 |
| **Total Toil** | **_____** | **____%** | **<30%** | **🟢/🟡/🔴** |
| Project Work | _____ | ____% | >50% | 🟢/🟡/🔴 |

**Toil Trend**: ↑ Increasing / → Stable / ↓ Decreasing

**Top Toil Activities**:
1. _____ (_____ hrs/week)
2. _____ (_____ hrs/week)
3. _____ (_____ hrs/week)

**Automation Opportunities**:
- [ ] _____ (Potential savings: _____ hrs/week)
- [ ] _____ (Potential savings: _____ hrs/week)

---

## 3. Team Capacity

### 3.1 Team Composition

| Role | Count | Headcount Plan | Status |
|------|-------|---------------|--------|
| SRE Lead | _____ | _____ | 🟢/🟡/🔴 |
| Senior SRE | _____ | _____ | 🟢/🟡/🔴 |
| SRE | _____ | _____ | 🟢/🟡/🔴 |
| Junior SRE | _____ | _____ | 🟢/🟡/🔴 |
| **Total** | **_____** | **_____** | **🟢/🟡/🔴** |

**Open Roles**: _____

**Recent Changes**:
- New hires: _____
- Departures: _____
- Transfers: _____

### 3.2 Capacity Allocation

**This Period** (_____ total hours):
| Category | Hours | % | Trend |
|----------|-------|---|-------|
| Incident Response | _____ | ____% | ↑/↓/→ |
| On-Call | _____ | ____% | ↑/↓/→ |
| Operational Work | _____ | ____% | ↑/↓/→ |
| Project Work | _____ | ____% | ↑/↓/→ |
| Meetings | _____ | ____% | ↑/↓/→ |
| Training/Learning | _____ | ____% | ↑/↓/→ |

**Project Work Ratio**: ____% (Target: >50%)

### 3.3 Workload Balance

**Load Distribution**:
| Engineer | On-Call Rotations | Incidents | Pages | Project Hours |
|----------|------------------|-----------|-------|--------------|
| | _____ | _____ | _____ | _____ |
| | _____ | _____ | _____ | _____ |
| | _____ | _____ | _____ | _____ |

**Balance Status**: 🟢 Balanced / 🟡 Uneven / 🔴 Severely Unbalanced

---

## 4. Knowledge and Skills

### 4.1 Service Ownership

**Knowledge Coverage**:
| Service | Primary Expert | Backup | Documentation | Bus Factor |
|---------|---------------|--------|---------------|------------|
| | _____ | _____ | 🟢/🟡/🔴 | _____ |
| | _____ | _____ | 🟢/🟡/🔴 | _____ |

**Risk Assessment**:
- Single points of failure: _____
- Services with bus factor = 1: _____
- Undocumented services: _____

### 4.2 Training and Development

**This Period**:
| Activity | Participants | Hours | Status |
|----------|-------------|-------|--------|
| Training sessions | _____ | _____ | ✅ |
| Certifications earned | _____ | - | ✅ |
| Knowledge sharing | _____ | _____ | ✅ |
| Conference attendance | _____ | - | ✅ |

**Skill Gaps**:
1. _____ (_____ team members need training)
2. _____ (_____ team members need training)

**Training Plan**:
- [ ] _____ (Timeline: _____, Budget: $_____)
- [ ] _____ (Timeline: _____, Budget: $_____)

### 4.3 Documentation

**Documentation Health**:
| Type | Count | Quality | Last Updated |
|------|-------|---------|-------------|
| Runbooks | _____ | _____/10 | _____ |
| Architecture Docs | _____ | _____/10 | _____ |
| Postmortems | _____ | _____/10 | _____ |
| Onboarding Guides | _____ | _____/10 | _____ |

**Documentation Gaps**:
- [ ] Missing runbooks: _____
- [ ] Outdated docs (>6 months): _____
- [ ] Incomplete postmortems: _____

---

## 5. Team Morale and Well-being

### 5.1 Burnout Indicators

**Risk Factors**:
| Indicator | Current | Threshold | Status |
|-----------|---------|-----------|--------|
| On-Call Frequency | _____ shifts/month | <4 | 🟢/🟡/🔴 |
| After-Hours Pages | _____ /week | <5 | 🟢/🟡/🔴 |
| Weekend Incidents | _____ /month | <2 | 🟢/🟡/🔴 |
| Vacation Days Taken | _____ /year avg | >15 | 🟢/🟡/🔴 |
| Overtime Hours | _____ /week avg | <5 | 🟢/🟡/🔴 |

**Burnout Risk**: 🟢 Low / 🟡 Moderate / 🔴 High

**Concerns**:
- [ ] Team member at high risk: _____
- [ ] Excessive on-call load
- [ ] Chronic overwork
- [ ] Vacation deficit

### 5.2 Team Sentiment

**Recent Feedback** (from retros, 1:1s, surveys):

**Positive Themes**:
1. _____
2. _____
3. _____

**Concerns**:
1. _____
2. _____
3. _____

**Action Items from Feedback**:
- [ ] _____ (Owner: _____, Due: _____)
- [ ] _____ (Owner: _____, Due: _____)

### 5.3 Work-Life Balance

| Metric | Status | Notes |
|--------|--------|-------|
| Team working reasonable hours | 🟢/🟡/🔴 | |
| On-call rotation sustainable | 🟢/🟡/🔴 | |
| Flexible work arrangements | 🟢/🟡/🔴 | |
| Mental health resources | 🟢/🟡/🔴 | |

---

## 6. Team Culture

### 6.1 Collaboration

**Cross-Team Collaboration**:
| Team | Interactions | Projects | Relationship |
|------|-------------|----------|--------------|
| | _____ /month | _____ | 🟢/🟡/🔴 |
| | _____ /month | _____ | 🟢/🟡/🔴 |

**Knowledge Sharing**:
- Tech talks given: _____
- Postmortems shared: _____
- Documentation contributions: _____

### 6.2 Blameless Culture

**Postmortem Quality**:
- Postmortems completed on time: _____%
- Action items completion rate: _____%
- Blameless approach maintained: 🟢 Yes / 🔴 No

**Culture Indicators**:
- [ ] Engineers comfortable acknowledging mistakes
- [ ] Focus on system improvements, not individual blame
- [ ] Psychological safety in incident response
- [ ] Open discussion of failures

### 6.3 Continuous Improvement

**Improvement Initiatives**:
| Initiative | Status | Impact | Owner |
|-----------|--------|--------|-------|
| | 🟢/🟡/⚪ | _____ | _____ |
| | 🟢/🟡/⚪ | _____ | _____ |

**Experimentation**:
- New tools tried: _____
- New processes adopted: _____
- Innovation time allocated: _____%

---

## 7. Growth and Career Development

### 7.1 Career Progression

**This Period**:
- Promotions: _____
- Level progressions: _____
- Role changes: _____

**Career Development Plans**:
| Engineer | Current Level | Target Level | Timeline | Status |
|----------|--------------|--------------|----------|--------|
| | L_____ | L_____ | Q_____ | 🟢/🟡/🔴 |
| | L_____ | L_____ | Q_____ | 🟢/🟡/🔴 |

### 7.2 Growth Opportunities

**Completed This Period**:
- [ ] Led incident response: _____ engineers
- [ ] Mentored junior engineer: _____ engineers
- [ ] Led project: _____ engineers
- [ ] Presented at conference: _____ engineers
- [ ] Contributed to open source: _____ engineers

**Upcoming Opportunities**:
- [ ] _____ (Engineer: _____, Timeline: _____)
- [ ] _____ (Engineer: _____, Timeline: _____)

---

## 8. Strategic Initiatives

### 8.1 Current Quarter Goals

1. **Goal**: _____
   - **Owner**: _____
   - **Progress**: ____%
   - **Status**: 🟢 On Track / 🟡 At Risk / 🔴 Blocked
   - **Blockers**: _____

2. **Goal**: _____
   - **Owner**: _____
   - **Progress**: ____%
   - **Status**: 🟢 On Track / 🟡 At Risk / 🔴 Blocked
   - **Blockers**: _____

3. **Goal**: _____
   - **Owner**: _____
   - **Progress**: ____%
   - **Status**: 🟢 On Track / 🟡 At Risk / 🔴 Blocked
   - **Blockers**: _____

### 8.2 SRE Maturity Roadmap

**Current Level**: _____
**Target Level**: _____ (by _____/_____)

**Gap Closure Plan**:
| Gap | Initiative | Effort | Timeline | Owner |
|-----|-----------|--------|----------|-------|
| | | _____ weeks | Q_____ | _____ |
| | | _____ weeks | Q_____ | _____ |

---

## 9. Recommendations

### 9.1 Immediate Actions (This Month)

1. **Action**: _____
   - **Rationale**: _____
   - **Owner**: _____
   - **Priority**: P_____

2. **Action**: _____
   - **Rationale**: _____
   - **Owner**: _____
   - **Priority**: P_____

### 9.2 Strategic Changes (Next Quarter)

1. **Change**: _____
   - **Expected Impact**: _____
   - **Investment Needed**: $_____

2. **Change**: _____
   - **Expected Impact**: _____
   - **Investment Needed**: $_____

### 9.3 Resource Needs

**Hiring**:
- [ ] _____ (Role, Urgency: H/M/L)
- [ ] _____ (Role, Urgency: H/M/L)

**Tools/Infrastructure**:
- [ ] _____ (Cost: $_____, ROI: _____)
- [ ] _____ (Cost: $_____, ROI: _____)

**Training/Development**:
- [ ] _____ (Cost: $_____, Participants: _____)

---

## 10. Summary and Next Steps

### Key Takeaways

**Strengths**:
1. _____
2. _____
3. _____

**Opportunities**:
1. _____
2. _____

**Risks**:
1. _____
2. _____

### Action Plan

**Next 30 Days**:
- [ ] _____ (Owner: _____, Due: _____)
- [ ] _____ (Owner: _____, Due: _____)
- [ ] _____ (Owner: _____, Due: _____)

**Next 90 Days**:
- [ ] _____ (Owner: _____, Due: _____)
- [ ] _____ (Owner: _____, Due: _____)

---

## References

- **Team Dashboard**: [Link]
- **Service Catalog**: [Link]
- **Incident Log**: [Link]
- **On-Call Schedule**: [Link]
- **Previous Report**: [Link]

---

**Report Status**: 🔴 Draft / 🟡 Under Review / 🟢 Published

**Next Report Date**: _____

**Review Meeting**: _____ (Date, Time)

---

**Template Usage**:
1. Generate this report monthly or quarterly
2. Review with team lead and management
3. Use for team retrospectives and planning
4. Track trends over time
5. Share with team for transparency
6. Archive in Datadog Notebook: `/save-to-notebook`

---
title: Monthly SRE Metrics Report
type: report
version: 1.0
created: 2025-12-12
tags: [report, metrics, monthly, kpi]
---

# Monthly SRE Metrics Report

**Month**: {{MONTH}} {{YEAR}}
**Prepared by**: {{AUTHOR}}
**Date**: {{DATE}}
**Distribution**: Engineering Team, Management

## Summary Dashboard

| Category | This Month | Last Month | Change | Target | Status |
|----------|-----------|------------|--------|--------|--------|
| **Availability** | ____% | ____% | +/- ____% | 99.9% | 🟢/🟡/🔴 |
| **Incidents** | _____ | _____ | +/- _____ | <5 | 🟢/🟡/🔴 |
| **MTTR** | _____ min | _____ min | +/- _____ | <30min | 🟢/🟡/🔴 |
| **Cost** | $_____  | $_____ | +/- $_____ | <$_____ | 🟢/🟡/🔴 |
| **Monitoring** | ____% | ____% | +/- ____% | 95% | 🟢/🟡/🔴 |

---

## 1. Infrastructure Metrics

### 1.1 Host Count and Coverage

**Query**:
```
search_datadog_hosts(query="*")
```

| Metric | This Month | Last Month | Change |
|--------|-----------|------------|--------|
| Total Hosts | _____ | _____ | +/- _____ |
| Monitored Hosts | _____ | _____ | +/- _____ |
| Coverage | ____% | ____% | +/- ____% |
| New Hosts | _____ | _____ | - |
| Decommissioned | _____ | _____ | - |

**Breakdown by Environment**:
```
search_datadog_hosts(query="*", include_all_tags=true)
# Group by env tag
```

| Environment | Hosts | % of Total |
|------------|-------|------------|
| Production | _____ | ____% |
| Staging | _____ | ____% |
| Development | _____ | ____% |

### 1.2 Service Count

**Query**:
```
search_datadog_services(query="*")
```

| Metric | This Month | Last Month | Change |
|--------|-----------|------------|--------|
| Total Services | _____ | _____ | +/- _____ |
| Active Services | _____ | _____ | +/- _____ |
| APM Instrumented | _____ | _____ | +/- _____ |
| Instrumentation Rate | ____% | ____% | +/- ____% |

### 1.3 Resource Utilization

**Query**:
```
get_datadog_metric(
  queries=[
    "avg:system.cpu.user{*}",
    "avg:system.mem.used{*}"
  ],
  from="now-30d"
)
```

| Resource | Avg | Peak | P95 | Trend |
|----------|-----|------|-----|-------|
| CPU | ____% | ____% | ____% | ↑/↓/→ |
| Memory | ____% | ____% | ____% | ↑/↓/→ |
| Disk | ____% | ____% | ____% | ↑/↓/→ |
| Network | _____ MB/s | _____ MB/s | _____ MB/s | ↑/↓/→ |

---

## 2. Application Performance

### 2.1 Request Volume

**Query**:
```
get_datadog_metric(
  queries=["sum:trace.*.request.hits{*}.as_rate()"],
  from="now-30d"
)
```

| Metric | This Month | Last Month | Change |
|--------|-----------|------------|--------|
| Total Requests | _____ M | _____ M | +/- ____% |
| Avg Requests/Day | _____ K | _____ K | +/- ____% |
| Peak Requests/Sec | _____ | _____ | +/- _____ |

**Top Services by Request Volume**:
| Service | Requests | % of Total | Change |
|---------|----------|------------|--------|
| | _____ M | ____% | +/- ____% |
| | _____ M | ____% | +/- ____% |
| | _____ M | ____% | +/- ____% |

### 2.2 Latency Metrics

**Query**:
```
get_datadog_metric(
  queries=[
    "p50:trace.*.request.duration{*}",
    "p95:trace.*.request.duration{*}",
    "p99:trace.*.request.duration{*}"
  ],
  from="now-30d"
)
```

| Percentile | This Month | Last Month | Change | Target |
|-----------|-----------|------------|--------|--------|
| p50 | _____ ms | _____ ms | +/- _____ | <100ms |
| p95 | _____ ms | _____ ms | +/- _____ | <500ms |
| p99 | _____ ms | _____ ms | +/- _____ | <1000ms |

**Slowest Services**:
| Service | p95 Latency | Change | Status |
|---------|------------|--------|--------|
| | _____ ms | +/- ____% | 🟢/🟡/🔴 |
| | _____ ms | +/- ____% | 🟢/🟡/🔴 |

### 2.3 Error Rates

**Query**:
```
get_datadog_metric(
  queries=["sum:trace.*.request.errors{*}.as_rate() / sum:trace.*.request.hits{*}.as_rate()"],
  from="now-30d"
)
```

| Metric | This Month | Last Month | Change | Target |
|--------|-----------|------------|--------|--------|
| Overall Error Rate | ____% | ____% | +/- ____% | <1% |
| 4xx Errors | _____ K | _____ K | +/- ____% | - |
| 5xx Errors | _____ K | _____ K | +/- ____% | <0.1% |

**Services with Highest Error Rates**:
| Service | Error Rate | Error Count | Status |
|---------|-----------|-------------|--------|
| | ____% | _____ | 🟢/🟡/🔴 |
| | ____% | _____ | 🟢/🟡/🔴 |

---

## 3. Incident Metrics

### 3.1 Incident Count and Severity

**Query**:
```
search_datadog_incidents(
  query="*",
  from="now-30d"
)
```

| Severity | Count | MTTR | Customer Impact |
|----------|-------|------|----------------|
| SEV-0 | _____ | _____ min | _____ users |
| SEV-1 | _____ | _____ min | _____ users |
| SEV-2 | _____ | _____ min | _____ users |
| SEV-3 | _____ | _____ min | _____ users |
| **Total** | **_____** | **_____ min** | **_____ users** |

**Trend**: _____ incidents → _____ incidents (____% change)

### 3.2 MTTD and MTTR

| Metric | This Month | Last Month | Change | Target |
|--------|-----------|------------|--------|--------|
| MTTD (Detection) | _____ min | _____ min | +/- _____ | <5min |
| MTTR (Recovery) | _____ min | _____ min | +/- _____ | <30min |
| MTTA (Acknowledge) | _____ min | _____ min | +/- _____ | <2min |

### 3.3 Incident Root Causes

| Root Cause | Count | % of Total |
|-----------|-------|------------|
| Code deployment | _____ | ____% |
| Infrastructure | _____ | ____% |
| External dependency | _____ | ____% |
| Configuration | _____ | ____% |
| Capacity | _____ | ____% |
| Other | _____ | ____% |

**Top 3 Incidents This Month**:
1. **[SEV-_____]** {{INCIDENT_1}} - _____
2. **[SEV-_____]** {{INCIDENT_2}} - _____
3. **[SEV-_____]** {{INCIDENT_3}} - _____

---

## 4. Cost Metrics

### 4.1 Total Cost

**Query**:
```
get_datadog_metric(
  queries=["sum:all.cost{*}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-30d"
)
```

| Metric | This Month | Last Month | Change |
|--------|-----------|------------|--------|
| Total Cost | $_____ | $_____ | +/- $_____ |
| Daily Average | $_____ | $_____ | +/- $_____ |
| Cost per Service | $_____ | $_____ | +/- $_____ |
| Cost per Request | $_____  | $_____ | +/- $_____ |

### 4.2 Cost by Service

**Query**:
```
get_datadog_metric(
  queries=["sum:all.cost{*} by {service}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-30d"
)
```

| Service | Cost | % of Total | Change |
|---------|------|------------|--------|
| | $_____ | ____% | +/- $_____ |
| | $_____ | ____% | +/- $_____ |
| | $_____ | ____% | +/- $_____ |

### 4.3 Cost Optimization

| Initiative | Savings | Status |
|-----------|---------|--------|
| | $_____ | ✅/🟡/⚪ |
| | $_____ | ✅/🟡/⚪ |
| **Total Savings** | **$_____** | |

---

## 5. Tagging Compliance

### 5.1 UST Compliance

**Query**:
```
search_datadog_hosts(query="*", include_all_tags=true)
analyze_datadog_logs(
  filter="*",
  sql_query="SELECT count(*) FROM logs WHERE env IS NOT NULL AND service IS NOT NULL AND version IS NOT NULL",
  from="now-7d"
)
```

| Tag | Coverage | Target | Status |
|-----|----------|--------|--------|
| env | ____% | 95% | 🟢/🟡/🔴 |
| service | ____% | 95% | 🟢/🟡/🔴 |
| version | ____% | 95% | 🟢/🟡/🔴 |
| team | ____% | 90% | 🟢/🟡/🔴 |
| **Overall UST** | **____%** | **95%** | **🟢/🟡/🔴** |

### 5.2 Non-Compliant Resources

| Resource Type | Count | Top Offenders |
|--------------|-------|---------------|
| Hosts | _____ | _____ |
| Services | _____ | _____ |
| Logs | ____% | _____ |

---

## 6. Monitoring Quality

### 6.1 Monitor Health

**Query**:
```
search_datadog_monitors(query="*")
search_datadog_monitors(query="status:'No Data' OR status:Alert")
```

| Metric | This Month | Last Month | Change | Target |
|--------|-----------|------------|--------|--------|
| Total Monitors | _____ | _____ | +/- _____ | - |
| Healthy Monitors | ____% | ____% | +/- ____% | >90% |
| Alert State | _____ | _____ | +/- _____ | <5% |
| No Data State | _____ | _____ | +/- _____ | <5% |

### 6.2 Alert Volume

| Metric | This Month | Last Month | Change | Target |
|--------|-----------|------------|--------|--------|
| Total Alerts | _____ | _____ | +/- _____ | <150 |
| Alerts/Day | _____ | _____ | +/- _____ | <5 |
| False Positives | ____% | ____% | +/- ____% | <10% |
| Actionable Alerts | ____% | ____% | +/- ____% | >90% |

### 6.3 Coverage by Service Tier

| Tier | Services | Monitored | Coverage |
|------|----------|-----------|----------|
| Tier 0 (Critical) | _____ | _____ | ____% |
| Tier 1 (Core) | _____ | _____ | ____% |
| Tier 2 (Supporting) | _____ | _____ | ____% |
| Tier 3 (Non-critical) | _____ | _____ | ____% |

---

## 7. Log Management

### 7.1 Log Volume

**Query**:
```
analyze_datadog_logs(
  filter="*",
  sql_query="SELECT count(*) FROM logs",
  from="now-30d"
)
```

| Metric | This Month | Last Month | Change |
|--------|-----------|------------|--------|
| Total Logs | _____ M | _____ M | +/- ____% |
| Logs/Day | _____ M | _____ M | +/- ____% |
| Data Volume | _____ GB | _____ GB | +/- ____% |
| Cost | $_____ | $_____ | +/- $_____ |

### 7.2 Log Breakdown by Status

**Query**:
```
analyze_datadog_logs(
  filter="*",
  sql_query="SELECT status, count(*) as logs FROM logs GROUP BY status",
  from="now-30d"
)
```

| Status | Count | % of Total | Change |
|--------|-------|------------|--------|
| INFO | _____ M | ____% | +/- ____% |
| WARN | _____ M | ____% | +/- ____% |
| ERROR | _____ M | ____% | +/- ____% |
| DEBUG | _____ M | ____% | +/- ____% |

### 7.3 Top Log Sources

| Source | Volume/Day | Cost/Month | Optimization |
|--------|-----------|------------|--------------|
| | _____ M | $_____ | _____ |
| | _____ M | $_____ | _____ |
| | _____ M | $_____ | _____ |

---

## 8. Month-over-Month Comparison

### 8.1 Key Metrics Trend (Last 3 Months)

| Metric | Month-3 | Month-2 | Month-1 | Current | Trend |
|--------|---------|---------|---------|---------|-------|
| Availability | ____% | ____% | ____% | ____% | ↑/↓/→ |
| Incident Count | _____ | _____ | _____ | _____ | ↑/↓/→ |
| MTTR | _____ min | _____ min | _____ min | _____ min | ↑/↓/→ |
| Cost | $_____ | $_____ | $_____ | $_____ | ↑/↓/→ |
| Error Rate | ____% | ____% | ____% | ____% | ↑/↓/→ |

**Overall Trend**: 🟢 Improving / 🟡 Stable / 🔴 Declining

---

## 9. Achievements This Month

### 9.1 Reliability Improvements

1. **Achievement**: _____
   - **Impact**: _____
   - **Metric improvement**: _____

2. **Achievement**: _____
   - **Impact**: _____
   - **Metric improvement**: _____

### 9.2 Cost Optimizations

1. **Optimization**: _____
   - **Savings**: $_____
   - **Status**: ✅ Complete

2. **Optimization**: _____
   - **Savings**: $_____
   - **Status**: 🟡 In Progress

### 9.3 Process Improvements

1. **Improvement**: _____
   - **Benefit**: _____
   - **Adoption**: ____%

---

## 10. Issues and Concerns

### 10.1 Current Issues

1. **Issue**: _____
   - **Impact**: [High / Medium / Low]
   - **Status**: _____
   - **Owner**: _____
   - **ETA**: _____

2. **Issue**: _____
   - **Impact**: [High / Medium / Low]
   - **Status**: _____
   - **Owner**: _____
   - **ETA**: _____

### 10.2 Risks for Next Month

1. **Risk**: _____
   - **Probability**: [High / Medium / Low]
   - **Mitigation**: _____

2. **Risk**: _____
   - **Probability**: [High / Medium / Low]
   - **Mitigation**: _____

---

## 11. Action Items for Next Month

### 11.1 High Priority

- [ ] **P1** _____ (Owner: _____, Due: _____)
- [ ] **P1** _____ (Owner: _____, Due: _____)

### 11.2 Medium Priority

- [ ] **P2** _____ (Owner: _____, Due: _____)
- [ ] **P2** _____ (Owner: _____, Due: _____)

### 11.3 Long-term

- [ ] **P3** _____ (Owner: _____, Due: _____)

---

## References

- **Dashboards**: [Links]
- **Incident Reports**: [Links]
- **Cost Reports**: [Links]
- **Previous Month's Report**: [Link]

---

**Report Status**: 🔴 Draft / 🟡 Under Review / 🟢 Published

**Next Report Date**: _____

---

**Template Usage**:
1. Generate this report on the 1st of each month
2. Run all Datadog queries to populate metrics
3. Compare to previous month's report
4. Share with engineering team
5. Archive in Datadog Notebook: `/save-to-notebook`

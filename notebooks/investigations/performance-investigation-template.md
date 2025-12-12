---
title: Performance Investigation
type: investigation
version: 1.0
created: 2025-12-12
tags: [investigation, performance, latency, throughput]
---

# Performance Investigation

**Metadata**
- Date: {{DATE}}
- Owner: {{OWNER}}
- Status: In Progress
- Priority: {{PRIORITY}}
- Related Services: {{SERVICES}}
- Incident ID: {{INCIDENT_ID}} (if applicable)

## Objective

Systematically investigate performance degradation, identify root cause, and implement resolution to restore service performance to baseline levels.

## Success Criteria
- [ ] Root cause identified with evidence
- [ ] Performance baseline re-established
- [ ] Resolution implemented and validated
- [ ] Prevention measures documented
- [ ] Postmortem completed (if SEV-1/2)

## Symptom Description

### Initial Report

**Reporter**: _____
**Reported Time**: _____
**Symptom**: _____

### Affected Components

- **Services**: _____
- **Endpoints**: _____
- **Regions**: _____
- **User Impact**: _____ (% of users or requests affected)

### Time Window

- **Degradation Start**: _____
- **Detection Time**: _____
- **Investigation Start**: _____
- **Resolution Time**: _____ (if resolved)

## Baseline Comparison

### Performance Metrics - Normal vs Current

| Metric | Baseline | Current | Degradation |
|--------|----------|---------|-------------|
| p50 Latency | _____ ms | _____ ms | +/- ____% |
| p95 Latency | _____ ms | _____ ms | +/- ____% |
| p99 Latency | _____ ms | _____ ms | +/- ____% |
| Throughput (req/s) | _____ | _____ | +/- ____% |
| Error Rate | ____% | ____% | +/- ____% |

**Query for baseline**:
```
get_datadog_metric(
  queries=[
    "avg:trace.{{SERVICE}}.request{*}",
    "p95:trace.{{SERVICE}}.request{*}",
    "p99:trace.{{SERVICE}}.request{*}"
  ],
  from="now-7d",
  to="{{DEGRADATION_START}}"
)
```

**Query for current state**:
```
get_datadog_metric(
  queries=[
    "avg:trace.{{SERVICE}}.request{*}",
    "p95:trace.{{SERVICE}}.request{*}",
    "p99:trace.{{SERVICE}}.request{*}"
  ],
  from="{{DEGRADATION_START}}",
  to="now"
)
```

## Data Collection

### 1. APM Trace Analysis

**Query top slow traces**:
```
search_datadog_spans(
  query="service:{{SERVICE}} status:ok",
  from="{{DEGRADATION_START}}",
  to="now",
  custom_attributes=["http.url", "http.method", "http.status_code"]
)
```

**Findings**:
- Slowest endpoints: _____
- Average span duration: _____
- Span count: _____
- Common patterns: _____

### 2. Service Performance Metrics

**Query service health**:
```
get_datadog_metric(
  queries=[
    "avg:trace.{{SERVICE}}.request.duration{*}",
    "avg:trace.{{SERVICE}}.request.hits{*}.as_rate()",
    "avg:trace.{{SERVICE}}.request.errors{*}.as_rate()"
  ],
  from="now-24h"
)
```

**Findings**:
- Request duration: _____
- Request rate: _____
- Error rate: _____
- Anomalies: _____

### 3. Database Performance

**Query database metrics**:
```
get_datadog_metric(
  queries=[
    "avg:postgresql.queries{*}",
    "avg:postgresql.connections{*}",
    "max:postgresql.locks{*}",
    "avg:postgresql.bgwriter.write_time{*}"
  ],
  from="now-24h"
)
```

**Findings**:
- Query count: _____
- Connection pool usage: _____
- Lock contentions: _____
- Slow queries: _____

### 4. External Dependencies

**Query external service calls**:
```
search_datadog_spans(
  query="service:{{SERVICE}} resource_name:*external* OR resource_name:*http*",
  from="{{DEGRADATION_START}}"
)
```

**Findings**:
- External services called: _____
- Response times: _____
- Timeout rate: _____
- Degraded dependencies: _____

### 5. Resource Utilization

**Query infrastructure metrics**:
```
get_datadog_metric(
  queries=[
    "avg:system.cpu.user{service:{{SERVICE}}}",
    "avg:system.mem.used{service:{{SERVICE}}}",
    "avg:system.net.bytes_sent{service:{{SERVICE}}}",
    "avg:system.disk.io.time{service:{{SERVICE}}}"
  ],
  from="now-24h"
)
```

**Findings**:
- CPU Usage: _____%
- Memory Usage: _____%
- Network I/O: _____
- Disk I/O: _____
- Saturation: ✅ / ❌

### 6. Recent Deployments

**Query deployment events**:
```
search_datadog_events(
  query="service:{{SERVICE}} (deployment OR release)",
  from="{{DEGRADATION_START_MINUS_2H}}",
  to="now"
)
```

**Findings**:
- Recent deployments: _____
- Deployment time: _____
- Correlation with degradation: ✅ / ❌
- Version: _____

## Analysis Framework

### Hypothesis 1: _____

**Evidence for**:
-
-

**Evidence against**:
-
-

**Test**:
```
[Query or action to validate hypothesis]
```

**Result**: ✅ Confirmed / ❌ Rejected

---

### Hypothesis 2: _____

**Evidence for**:
-
-

**Evidence against**:
-
-

**Test**:
```
[Query or action to validate hypothesis]
```

**Result**: ✅ Confirmed / ❌ Rejected

---

### Hypothesis 3: _____

**Evidence for**:
-
-

**Evidence against**:
-
-

**Test**:
```
[Query or action to validate hypothesis]
```

**Result**: ✅ Confirmed / ❌ Rejected

## Root Cause Determination

### Identified Root Cause

**Category**: [Code Issue / Infrastructure / Dependency / Configuration / Capacity]

**Description**:

**Evidence**:
1.
2.
3.

**Impact Scope**:
- Affected services: _____
- Affected users: _____
- Business impact: _____

### Contributing Factors

1. **Factor 1**
   - Description:
   - Contribution: _____%

2. **Factor 2**
   - Description:
   - Contribution: _____%

## Resolution Plan

### Immediate Actions (Stop the Bleeding)

1. [ ] Action 1 (Owner: _____, ETA: _____)
   - Description:
   - Risk:
   - Rollback plan:

2. [ ] Action 2 (Owner: _____, ETA: _____)
   - Description:
   - Risk:
   - Rollback plan:

### Long-term Fixes (Prevent Recurrence)

1. [ ] Fix 1 (Owner: _____, Due: _____)
   - Description:
   - Effort:
   - Priority:

2. [ ] Fix 2 (Owner: _____, Due: _____)
   - Description:
   - Effort:
   - Priority:

## Validation

### Performance Restored

**Re-run baseline query**:
```
get_datadog_metric(
  queries=[
    "avg:trace.{{SERVICE}}.request{*}",
    "p95:trace.{{SERVICE}}.request{*}",
    "p99:trace.{{SERVICE}}.request{*}"
  ],
  from="{{RESOLUTION_TIME}}",
  to="now"
)
```

**Validation Metrics**:
- [ ] p50 latency within 10% of baseline
- [ ] p95 latency within 15% of baseline
- [ ] p99 latency within 20% of baseline
- [ ] Error rate <1%
- [ ] No new alerts

**Status**: ✅ Validated / ❌ Not Validated

## Prevention Measures

### Monitoring Improvements

1. **New Monitor**: _____
   - Query:
   - Threshold:
   - Action:

2. **Enhanced Dashboard**: _____
   - Widgets added:
   - Use case:

### Process Improvements

1. **Improvement 1**
   - Current gap:
   - Proposed change:
   - Owner:

2. **Improvement 2**
   - Current gap:
   - Proposed change:
   - Owner:

### Technical Improvements

1. **Improvement 1**
   - Technical debt identified:
   - Remediation plan:
   - Priority:

2. **Improvement 2**
   - Technical debt identified:
   - Remediation plan:
   - Priority:

## Timeline Summary

| Time | Event | Duration |
|------|-------|----------|
| {{DEGRADATION_START}} | Degradation begins | - |
| {{DETECTION_TIME}} | Issue detected | +_____ min |
| {{INVESTIGATION_START}} | Investigation starts | +_____ min |
| {{ROOT_CAUSE_FOUND}} | Root cause found | +_____ min |
| {{RESOLUTION_TIME}} | Resolution deployed | +_____ min |
| {{VALIDATION_TIME}} | Performance validated | +_____ min |

**Total Time to Resolution**: _____ minutes

**MTTR**: _____ minutes (from detection to resolution)

## Lessons Learned

### What Went Well
1.
2.
3.

### What Could Be Improved
1.
2.
3.

### Action Items
- [ ] Update runbook (Owner: _____, Due: _____)
- [ ] Add monitoring (Owner: _____, Due: _____)
- [ ] Technical fix (Owner: _____, Due: _____)
- [ ] Process improvement (Owner: _____, Due: _____)
- [ ] Team training (Owner: _____, Due: _____)

## References

- **Service Dashboard**: [Link]
- **APM Service Page**: [Link]
- **Related Incidents**: [Links]
- **Slack Channel**: [Link]
- **Postmortem** (if SEV-1/2): [Link]

---

**Investigation Status**: 🔴 Open / 🟡 In Progress / 🟢 Resolved

**Next Review**: _____

---

**Template Usage Notes**:
1. Copy this template when performance degradation is detected
2. Fill in metadata and symptom description immediately
3. Run data collection queries systematically
4. Test hypotheses with evidence
5. Document root cause with proof
6. Implement and validate resolution
7. Complete prevention measures
8. Share with team for learning
9. Archive in Datadog Notebook: `/save-to-notebook`

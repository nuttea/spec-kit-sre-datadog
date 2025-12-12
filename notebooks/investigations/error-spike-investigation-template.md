---
title: Error Spike Investigation
type: investigation
version: 1.0
created: 2025-12-12
tags: [investigation, errors, debugging, root-cause]
---

# Error Spike Investigation

**Metadata**
- Date: {{DATE}}
- Owner: {{OWNER}}
- Status: In Progress
- Priority: {{PRIORITY}}
- Related Services: {{SERVICES}}
- Incident ID: {{INCIDENT_ID}} (if applicable)

## Objective

Investigate sudden increase in error rate, identify root cause, and implement resolution to restore service health.

## Success Criteria
- [ ] Error spike cause identified
- [ ] Error rate returned to baseline
- [ ] No customer-facing impact
- [ ] Prevention measures implemented
- [ ] Monitoring improved

## Error Spike Summary

### Initial Detection

**Detection Method**: [Monitor Alert / User Report / Dashboard Review]
**Detection Time**: _____
**Alert Link**: _____

### Baseline vs Current

| Metric | Baseline | Current | Increase |
|--------|----------|---------|----------|
| Error Count | _____ | _____ | +____% |
| Error Rate | ____% | ____% | +____% |
| Affected Services | _____ | _____ | +_____ |
| User Impact | ____% | ____% | +____% |

## Data Collection

### 1. Error Timeline Analysis

**Query error spike timeline**:
```
analyze_datadog_logs(
  filter="status:error service:{{SERVICE}}",
  sql_query="SELECT date_trunc('minute', timestamp) as time, count(*) as errors FROM logs GROUP BY time ORDER BY time",
  from="now-6h"
)
```

**Findings**:
- Spike start time: _____
- Peak error rate: _____
- Duration: _____
- Pattern: [Gradual / Sudden / Intermittent]

**Visualization**: [Paste graph URL or describe pattern]

### 2. Error Type Distribution

**Query error breakdown**:
```
analyze_datadog_logs(
  filter="status:error service:{{SERVICE}}",
  sql_query="SELECT status, error.kind, count(*) as count FROM logs GROUP BY status, error.kind ORDER BY count DESC LIMIT 10",
  from="now-6h"
)
```

**Top Errors**:

| Error Type | Count | % of Total | First Seen |
|-----------|-------|------------|------------|
| | | | |
| | | | |
| | | | |

### 3. Error Message Patterns

**Query error messages**:
```
search_datadog_logs(
  query="status:error service:{{SERVICE}}",
  from="now-6h",
  extra_fields=["error.message", "error.stack"]
)
```

**Common Patterns** (use `/analyze_datadog_logs` for pattern detection):
```
analyze_datadog_logs(
  filter="status:error service:{{SERVICE}}",
  sql_query="",
  from="now-6h"
)
```

**Pattern 1**: _____
- Frequency: _____
- Sample message: _____

**Pattern 2**: _____
- Frequency: _____
- Sample message: _____

### 4. Affected Services and Endpoints

**Query affected services**:
```
analyze_datadog_logs(
  filter="status:error",
  sql_query="SELECT service, count(*) as errors FROM logs GROUP BY service ORDER BY errors DESC LIMIT 10",
  from="now-6h"
)
```

**Service Impact**:

| Service | Error Count | % Change | Critical |
|---------|-------------|----------|----------|
| | | | ✅ / ❌ |
| | | | ✅ / ❌ |

**Query affected endpoints**:
```
search_datadog_spans(
  query="service:{{SERVICE}} status:error",
  from="now-6h",
  custom_attributes=["http.url", "http.method", "http.status_code"]
)
```

**Endpoint Impact**:

| Endpoint | Method | Error Count | Status Codes |
|----------|--------|-------------|--------------|
| | | | |
| | | | |

### 5. Recent Deployments

**Query deployment events**:
```
search_datadog_events(
  query="service:{{SERVICE}} (deployment OR release OR config)",
  from="{{SPIKE_START_MINUS_2H}}",
  to="now"
)
```

**Recent Changes**:
- [ ] Code deployment at _____
- [ ] Configuration change at _____
- [ ] Infrastructure change at _____
- [ ] Dependency update at _____

**Correlation**: ✅ Likely related / ❌ No correlation

### 6. Trace Analysis

**Query error traces**:
```
search_datadog_spans(
  query="service:{{SERVICE}} status:error",
  from="now-6h"
)
```

**Sample Error Traces**:

**Trace ID**: _____
- Root span: _____
- Error span: _____
- Error message: _____
- Stack trace snippet: _____

**Trace ID**: _____
- Root span: _____
- Error span: _____
- Error message: _____
- Stack trace snippet: _____

### 7. External Dependencies

**Query external service health**:
```
search_datadog_spans(
  query="service:{{DEPENDENCY_SERVICE}} status:error",
  from="now-6h"
)

get_datadog_metric(
  queries=["avg:trace.{{DEPENDENCY_SERVICE}}.request.duration{*}"],
  from="now-6h"
)
```

**Dependency Health**:

| Dependency | Status | Response Time | Error Rate |
|-----------|--------|---------------|------------|
| | 🟢 / 🟡 / 🔴 | _____ ms | ____% |
| | 🟢 / 🟡 / 🔴 | _____ ms | ____% |

### 8. Infrastructure Metrics

**Query resource utilization**:
```
get_datadog_metric(
  queries=[
    "avg:system.cpu.user{service:{{SERVICE}}}",
    "avg:system.mem.used{service:{{SERVICE}}}",
    "avg:system.net.bytes_rcvd{service:{{SERVICE}}}",
    "avg:system.disk.io.time{service:{{SERVICE}}}"
  ],
  from="now-6h"
)
```

**Resource Status**:
- CPU: _____%
- Memory: _____%
- Network: _____
- Disk I/O: _____
- Saturation: ✅ / ❌

## Root Cause Analysis

### Hypothesis Testing

#### Hypothesis 1: Recent Deployment

**Evidence for**:
- Deployment at _____ correlates with spike start
- Error pattern matches code change in _____
- Rollback testing shows _____

**Evidence against**:
- Deployment was _____ hours before spike
- Errors also occurring in non-deployed services
- _____

**Test**: _____

**Result**: ✅ Confirmed / ❌ Rejected / 🟡 Partial

---

#### Hypothesis 2: External Dependency Failure

**Evidence for**:
- {{DEPENDENCY}} error rate increased at _____
- Error messages reference {{DEPENDENCY}}
- Timeout errors correlate with dependency latency

**Evidence against**:
- {{DEPENDENCY}} reports healthy status
- Not all requests to {{DEPENDENCY}} failing
- _____

**Test**: _____

**Result**: ✅ Confirmed / ❌ Rejected / 🟡 Partial

---

#### Hypothesis 3: Configuration Change

**Evidence for**:
- Config change deployed at _____
- Errors match misconfiguration pattern
- Specific endpoints affected by config

**Evidence against**:
- Config change was in different service
- Errors pre-date configuration change
- _____

**Test**: _____

**Result**: ✅ Confirmed / ❌ Rejected / 🟡 Partial

---

#### Hypothesis 4: Capacity/Load Issue

**Evidence for**:
- Traffic spike at _____
- Resource saturation observed
- Errors correlate with high load periods

**Evidence against**:
- Traffic within normal parameters
- Resources not saturated
- _____

**Test**: _____

**Result**: ✅ Confirmed / ❌ Rejected / 🟡 Partial

### Root Cause Determination

**Identified Root Cause**:

**Category**: [Code Bug / Deployment / Configuration / Dependency / Capacity / Data Issue]

**Detailed Description**:

**Supporting Evidence**:
1. _____
2. _____
3. _____

**First Occurrence**: _____

**Trigger**: _____

### Contributing Factors

1. **Factor 1**:
   - Description:
   - Contribution:

2. **Factor 2**:
   - Description:
   - Contribution:

## Impact Assessment

### Customer Impact

- **Affected Users**: _____ (_____ %)
- **Failed Requests**: _____
- **Duration**: _____ minutes
- **User-Facing Errors**: ✅ Yes / ❌ No
- **Severity**: SEV-0 / SEV-1 / SEV-2 / SEV-3 / SEV-4

### Business Impact

- **Revenue Impact**: $_____
- **SLO Impact**: _____%
- **Customer Complaints**: _____
- **Support Tickets**: _____

## Mitigation Actions

### Immediate Actions (Taken)

1. ✅ **Action 1** (_____:_____ timestamp)
   - Description:
   - Result:
   - Impact:

2. ✅ **Action 2** (_____:_____ timestamp)
   - Description:
   - Result:
   - Impact:

### Resolution

**Resolution Method**: [Rollback / Hotfix / Config Revert / Scale Up / Manual Intervention]

**Implementation Time**: _____

**Validation**:
```
analyze_datadog_logs(
  filter="status:error service:{{SERVICE}}",
  sql_query="SELECT count(*) FROM logs",
  from="{{RESOLUTION_TIME}}",
  to="now"
)
```

**Current Error Rate**: _____ (Baseline: _____)

**Status**: ✅ Resolved / 🟡 Partially Resolved / 🔴 Still Impacted

## Prevention Measures

### Immediate Improvements

1. **Monitor Enhancement**
   - [ ] Create/update monitor for this error pattern
   - Query:
   - Threshold:
   - Owner:
   - Due:

2. **Alerting Improvement**
   - [ ] Add early warning alert
   - Condition:
   - Owner:
   - Due:

### Short-term Fixes (Next Sprint)

1. [ ] **Fix 1** (Owner: _____, Due: _____)
   - Description:
   - Priority: P_____
   - Effort: _____ days

2. [ ] **Fix 2** (Owner: _____, Due: _____)
   - Description:
   - Priority: P_____
   - Effort: _____ days

### Long-term Improvements

1. [ ] **Improvement 1** (Owner: _____, Due: _____)
   - Description:
   - Priority:
   - Effort:

2. [ ] **Improvement 2** (Owner: _____, Due: _____)
   - Description:
   - Priority:
   - Effort:

### Process Improvements

1. **Detection**
   - Current gap:
   - Proposed improvement:
   - Owner:

2. **Response**
   - Current gap:
   - Proposed improvement:
   - Owner:

3. **Prevention**
   - Current gap:
   - Proposed improvement:
   - Owner:

## Timeline

| Time | Event | Action | Owner |
|------|-------|--------|-------|
| {{SPIKE_START}} | Error spike begins | - | - |
| {{DETECTION}} | Spike detected | Alert fired | System |
| {{ACKNOWLEDGE}} | Investigation starts | On-call acknowledged | {{ONCALL}} |
| {{ROOT_CAUSE}} | Root cause identified | Analysis complete | {{OWNER}} |
| {{MITIGATION}} | Mitigation deployed | Resolution implemented | {{OWNER}} |
| {{VALIDATION}} | Resolution validated | Error rate normalized | {{OWNER}} |

**Total Duration**: _____ minutes

**MTTD**: _____ minutes (Mean Time To Detect)
**MTTR**: _____ minutes (Mean Time To Resolve)

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
- [ ] Add test case (Owner: _____, Due: _____)
- [ ] Improve monitoring (Owner: _____, Due: _____)
- [ ] Team training (Owner: _____, Due: _____)
- [ ] Update documentation (Owner: _____, Due: _____)

## References

- **Service Dashboard**: [Link]
- **Error Dashboard**: [Link]
- **Alert Definition**: [Link]
- **Related Incidents**: [Links]
- **Slack Thread**: [Link]
- **Postmortem** (if SEV-1/2): [Link]

---

**Investigation Status**: 🔴 Open / 🟡 In Progress / 🟢 Resolved

**Follow-up Review**: _____

---

**Template Usage Notes**:
1. Start investigation immediately when error spike detected
2. Work through data collection systematically
3. Test multiple hypotheses with evidence
4. Document root cause with proof
5. Implement and validate mitigation
6. Complete all prevention measures
7. Share findings with team
8. Archive in Datadog Notebook: `/save-to-notebook`

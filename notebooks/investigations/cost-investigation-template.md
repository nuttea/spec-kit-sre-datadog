---
title: Cost Anomaly Investigation
type: investigation
version: 1.0
created: 2025-12-12
tags: [investigation, cost, finops, optimization]
---

# Cost Anomaly Investigation

**Metadata**
- Date: {{DATE}}
- Owner: {{OWNER}}
- Status: In Progress
- Priority: {{PRIORITY}}
- Affected Period: {{START_DATE}} to {{END_DATE}}

## Objective

Investigate unexpected cost increase, identify root cause, and implement cost optimization measures to return to baseline spending.

## Success Criteria
- [ ] Cost anomaly cause identified
- [ ] Cost spike quantified ($$$)
- [ ] Optimization opportunities identified
- [ ] Cost reduction plan created
- [ ] Savings targets set and tracked

## Cost Anomaly Summary

### Detection

**Detection Method**: [Cost Alert / Budget Review / Dashboard]
**Detection Date**: _____
**Anomaly Period**: _____ to _____

### Cost Impact

| Metric | Baseline | Current | Increase |
|--------|----------|---------|----------|
| Daily Cost | $_____ | $_____ | +$_____ (+____%) |
| Monthly Projection | $_____ | $_____ | +$_____ (+____%) |
| Annual Impact | $_____ | $_____ | +$_____ (+____%) |

**Urgency**: 🔴 Critical / 🟡 Elevated / 🟢 Minor

## Data Collection

### 1. Cost Timeline Analysis

**Query cost trend**:
```
get_datadog_metric(
  queries=["sum:all.cost{*}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-90d",
  to="now"
)
```

**Findings**:
- Spike start date: _____
- Cost baseline (before spike): $_____/day
- Peak cost: $_____/day
- Current cost: $_____/day
- Total anomaly cost: $_____

**Pattern**: [Gradual / Sudden / Periodic / Sustained]

### 2. Cost Breakdown by Service

**Query service costs**:
```
get_datadog_metric(
  queries=["sum:all.cost{*} by {service}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-30d"
)
```

**Top Cost Increases**:

| Service | Baseline | Current | Increase | % Change |
|---------|----------|---------|----------|----------|
| | $_____ | $_____ | $_____ | +____% |
| | $_____ | $_____ | $_____ | +____% |
| | $_____ | $_____ | $_____ | +____% |
| | $_____ | $_____ | $_____ | +____% |
| | $_____ | $_____ | $_____ | +____% |

**Most Impactful Service**: _____

### 3. Cost Breakdown by Team

**Query team costs**:
```
get_datadog_metric(
  queries=["sum:all.cost{*} by {team}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-30d"
)
```

**Team Cost Changes**:

| Team | Baseline | Current | Increase | % Change |
|------|----------|---------|----------|----------|
| | $_____ | $_____ | $_____ | +____% |
| | $_____ | $_____ | $_____ | +____% |
| | $_____ | $_____ | $_____ | +____% |

### 4. Cost Breakdown by Environment

**Query environment costs**:
```
get_datadog_metric(
  queries=["sum:all.cost{*} by {env}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-30d"
)
```

**Environment Costs**:

| Environment | Baseline | Current | Increase | % Change |
|-------------|----------|---------|----------|----------|
| Production | $_____ | $_____ | $_____ | +____% |
| Staging | $_____ | $_____ | $_____ | +____% |
| Development | $_____ | $_____ | $_____ | +____% |

### 5. Resource Utilization Analysis

**Query resource usage**:
```
search_datadog_hosts(query="*")

get_datadog_metric(
  queries=[
    "avg:system.cpu.user{*} by {host}",
    "avg:system.mem.used{*} by {host}"
  ],
  from="now-30d"
)
```

**Resource Utilization**:

| Resource Type | Count | Avg CPU | Avg Memory | Idle Count |
|--------------|-------|---------|------------|------------|
| Compute | _____ | ____% | ____% | _____ |
| Database | _____ | ____% | ____% | _____ |
| Cache | _____ | ____% | ____% | _____ |

**Idle/Underutilized Resources**: _____ (cost: $_____/month)

### 6. Log Volume Analysis

**Query log volume**:
```
analyze_datadog_logs(
  filter="*",
  sql_query="SELECT date_trunc('day', timestamp) as day, count(*) as logs FROM logs GROUP BY day ORDER BY day",
  from="now-30d"
)
```

**Log Volume**:
- Baseline: _____ logs/day
- Current: _____ logs/day
- Increase: +_____%
- Estimated cost impact: $_____/month

**Top log sources**:
```
analyze_datadog_logs(
  filter="*",
  sql_query="SELECT source, service, count(*) as logs FROM logs GROUP BY source, service ORDER BY logs DESC LIMIT 10",
  from="now-7d"
)
```

| Source | Service | Volume | % of Total |
|--------|---------|--------|------------|
| | | | |
| | | | |

### 7. Metric Cardinality Analysis

**Query metric volume**:
```
search_datadog_metrics(
  name_filter="*",
  from="now-30d"
)
```

**High Cardinality Metrics**:
- Total custom metrics: _____
- Baseline metrics: _____
- New metrics: _____
- High cardinality metrics (>1000 series): _____

**Cost Impact**: $_____/month

### 8. Recent Changes

**Query infrastructure events**:
```
search_datadog_events(
  query="(deployment OR scaling OR provisioning OR configuration)",
  from="{{SPIKE_START_MINUS_7D}}",
  to="now"
)
```

**Recent Changes**:
- [ ] New service deployment: _____
- [ ] Scaling event: _____
- [ ] Configuration change: _____
- [ ] Feature flag enabled: _____
- [ ] Traffic increase: _____

## Root Cause Analysis

### Hypothesis 1: New Service or Feature

**Evidence for**:
- New service {{SERVICE_NAME}} deployed on _____
- Service cost: $_____/day
- Represents ____% of cost increase

**Evidence against**:
- Service was deployed before spike started
- Cost increase exceeds service's projected cost
- _____

**Validation**:
```
get_datadog_metric(
  queries=["sum:all.cost{service:{{SERVICE_NAME}}}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-30d"
)
```

**Result**: ✅ Confirmed / ❌ Rejected / 🟡 Partial

---

### Hypothesis 2: Traffic/Load Increase

**Evidence for**:
- Request volume increased ____% on _____
- Auto-scaling triggered
- Compute costs increased proportionally

**Evidence against**:
- Traffic increase doesn't account for full cost spike
- Non-compute costs also increased
- _____

**Validation**:
```
get_datadog_metric(
  queries=["sum:trace.requests{*}.as_count().rollup(sum, daily)"],
  from="now-30d"
)
```

**Result**: ✅ Confirmed / ❌ Rejected / 🟡 Partial

---

### Hypothesis 3: Resource Inefficiency

**Evidence for**:
- _____ idle instances identified
- Average CPU utilization <20%
- Over-provisioned resources

**Evidence against**:
- Resources were right-sized in previous review
- No recent provisioning changes
- _____

**Validation**:
```
search_datadog_hosts(query="*")
# Identify hosts with CPU <20% for 7+ days
```

**Result**: ✅ Confirmed / ❌ Rejected / 🟡 Partial

---

### Hypothesis 4: Data Volume Explosion

**Evidence for**:
- Log volume increased ____% to _____ GB/day
- Metrics increased ____% to _____ series
- Storage costs spiked

**Evidence against**:
- Data retention policy unchanged
- No new log sources added
- _____

**Validation**:
```
analyze_datadog_logs(
  filter="*",
  sql_query="SELECT count(*) FROM logs",
  from="now-30d"
)
```

**Result**: ✅ Confirmed / ❌ Rejected / 🟡 Partial

---

### Hypothesis 5: Configuration Error

**Evidence for**:
- Configuration change on _____
- Accidentally enabled verbose logging
- Retention period increased

**Evidence against**:
- Configuration audit shows no changes
- Multiple services affected
- _____

**Validation**: _____

**Result**: ✅ Confirmed / ❌ Rejected / 🟡 Partial

### Root Cause Determination

**Identified Root Cause(s)**:

**Primary Cause**:
- Description:
- Cost Impact: $_____/month
- Evidence:

**Contributing Factors**:
1. Factor 1: _____ (Impact: $_____/month)
2. Factor 2: _____ (Impact: $_____/month)
3. Factor 3: _____ (Impact: $_____/month)

**Total Anomaly Cost**: $_____/month

## Optimization Opportunities

### Immediate Quick Wins (0-2 weeks)

#### Opportunity 1: _____

**Type**: [Right-sizing / Decommission / Configuration / Data Optimization]

**Description**:

**Implementation**:
1. Step 1
2. Step 2
3. Step 3

**Potential Savings**: $_____/month

**Effort**: [Low / Medium / High]

**Risk**: [Low / Medium / High]

**Owner**: _____

**Target Date**: _____

---

#### Opportunity 2: _____

**Type**: [Right-sizing / Decommission / Configuration / Data Optimization]

**Description**:

**Implementation**:
1. Step 1
2. Step 2

**Potential Savings**: $_____/month

**Effort**: [Low / Medium / High]

**Risk**: [Low / Medium / High]

**Owner**: _____

**Target Date**: _____

### Short-term Optimizations (1-3 months)

#### Opportunity 3: _____

**Description**:

**Potential Savings**: $_____/month

**Effort**: _____ days

**Owner**: _____

**Target Date**: _____

---

#### Opportunity 4: _____

**Description**:

**Potential Savings**: $_____/month

**Effort**: _____ days

**Owner**: _____

**Target Date**: _____

### Long-term Strategic Optimizations (3-6 months)

#### Opportunity 5: _____

**Description**:

**Potential Savings**: $_____/month

**Effort**: _____ weeks

**Owner**: _____

**Target Date**: _____

## Cost Reduction Roadmap

### Prioritization Matrix

| Opportunity | Savings | Effort | Risk | Priority | Status |
|------------|---------|--------|------|----------|--------|
| #1 | $_____/mo | Low | Low | P1 | 🟡 In Progress |
| #2 | $_____/mo | Low | Low | P1 | ⚪ Not Started |
| #3 | $_____/mo | Med | Med | P2 | ⚪ Not Started |
| #4 | $_____/mo | High | Low | P2 | ⚪ Not Started |
| #5 | $_____/mo | Med | High | P3 | ⚪ Not Started |

### Implementation Timeline

**Month 1**:
- [ ] Opportunity 1 (Savings: $_____/mo)
- [ ] Opportunity 2 (Savings: $_____/mo)
- **Target Savings**: $_____/mo

**Month 2**:
- [ ] Opportunity 3 (Savings: $_____/mo)
- [ ] Opportunity 4 (Savings: $_____/mo)
- **Target Savings**: $_____/mo

**Month 3**:
- [ ] Opportunity 5 (Savings: $_____/mo)
- **Target Savings**: $_____/mo

**Total Projected Savings**: $_____/month (____% reduction)

## Cost Governance Improvements

### Monitoring Enhancements

1. **Cost Anomaly Alert**
   - [ ] Create alert for >10% daily cost increase
   - Query:
   - Notification: _____
   - Owner: _____

2. **Budget Alerts**
   - [ ] Set monthly budget: $_____
   - [ ] 80% warning threshold
   - [ ] 100% critical threshold
   - Owner: _____

3. **Service Cost Dashboard**
   - [ ] Create cost dashboard by service
   - [ ] Add week-over-week comparison
   - [ ] Add budget vs actual
   - Owner: _____

### Process Improvements

1. **Monthly Cost Review**
   - [ ] Establish monthly review process
   - [ ] Assign cost owners per service
   - [ ] Create review template
   - Owner: _____

2. **Cost Allocation**
   - [ ] Implement chargeback model
   - [ ] Tag all resources with team/service
   - [ ] Generate monthly cost reports
   - Owner: _____

3. **Optimization Tracking**
   - [ ] Create optimization backlog
   - [ ] Track savings over time
   - [ ] Report ROI to leadership
   - Owner: _____

## Action Items

### Immediate (This Week)
- [ ] Stop cost bleed: _____ (Owner: _____, Due: _____)
- [ ] Implement quick win #1: _____ (Owner: _____, Due: _____)
- [ ] Set up cost alerts: _____ (Owner: _____, Due: _____)

### Short-term (This Month)
- [ ] Optimization 1: _____ (Owner: _____, Due: _____)
- [ ] Optimization 2: _____ (Owner: _____, Due: _____)
- [ ] Cost dashboard: _____ (Owner: _____, Due: _____)

### Long-term (This Quarter)
- [ ] Strategic optimization: _____ (Owner: _____, Due: _____)
- [ ] Cost governance: _____ (Owner: _____, Due: _____)
- [ ] Quarterly review: _____ (Owner: _____, Due: _____)

## Validation and Tracking

### Savings Validation

**Re-run cost query**:
```
get_datadog_metric(
  queries=["sum:all.cost{*}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="{{IMPLEMENTATION_DATE}}",
  to="now"
)
```

### Savings Tracking

| Week | Baseline Cost | Actual Cost | Savings | Cumulative |
|------|---------------|-------------|---------|------------|
| Week 1 | $_____ | $_____ | $_____ | $_____ |
| Week 2 | $_____ | $_____ | $_____ | $_____ |
| Week 3 | $_____ | $_____ | $_____ | $_____ |
| Week 4 | $_____ | $_____ | $_____ | $_____ |

**Total Savings**: $_____/month

**Target Achievement**: _____%

## Lessons Learned

### What Caused the Spike
-
-

### How We Could Have Prevented It
-
-

### What We'll Do Differently
-
-

## References

- **Cost Dashboard**: [Link]
- **Budget Plan**: [Link]
- **Previous Cost Reports**: [Links]
- **Optimization Backlog**: [Link]
- **Slack Discussion**: [Link]

---

**Investigation Status**: 🔴 Open / 🟡 In Progress / 🟢 Resolved

**Next Review**: _____

---

**Template Usage Notes**:
1. Start investigation when cost anomaly detected
2. Quantify the impact first
3. Analyze cost breakdown systematically
4. Test hypotheses with data
5. Identify optimization opportunities
6. Prioritize by savings/effort/risk
7. Track savings weekly
8. Share findings with leadership
9. Archive in Datadog Notebook: `/save-to-notebook`

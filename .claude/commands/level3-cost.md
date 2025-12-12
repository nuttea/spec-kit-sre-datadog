# Level 3: Cost Optimization Analysis

Execute comprehensive cost optimization analysis for Level 3 (Managed).

**Target:** Achieve 20%+ cost reduction from baseline through optimization

**Step 1: Query Current Cost Metrics**

**Total Spend:**
```
get_datadog_metric(
    context="Level 3: Current cloud spend analysis",
    queries=["sum:all.cost{*}.rollup(sum, monthly)"],
    use_cloud_cost=True,
    from="now-90d"
)
```

**Cost by Service:**
```
get_datadog_metric(
    context="Cost breakdown by service",
    queries=["sum:all.cost{*} by {service}.rollup(sum, daily)"],
    use_cloud_cost=True,
    from="now-30d"
)
```

**Cost by Team:**
```
get_datadog_metric(
    context="Cost breakdown by team",
    queries=["sum:all.cost{*} by {team}.rollup(sum, daily)"],
    use_cloud_cost=True,
    from="now-30d"
)
```

**Step 2: Identify Optimization Opportunities**

**A. Unused/Idle Services:**
```
get_datadog_metric(
    context="Find low-traffic services",
    queries=["sum:trace.requests{*} by {service}"],
    from="now-30d"
)

search_datadog_services(
    context="Service catalog analysis",
    query="*"
)
```

Identify services with:
- <100 requests/day: Consider for decommission
- No requests in 30 days: Strong decommission candidate
- No recent deployments: Potentially stale

**B. Log Optimization:**
```
search_datadog_logs(
    context="High-volume log sources",
    query="*",
    from="now-24h",
    indexes=["*"]
)

analyze_datadog_logs(
    context="Log pattern analysis for exclusion",
    filter="*",
    from="now-24h"
)
```

Identify:
- Debug logs in production indexes
- High-volume, low-value logs
- Repetitive patterns for exclusion
- Over-retained logs

**C. Metric Cardinality:**
```
search_datadog_metrics(
    context="High cardinality metrics",
    query="*"
)
```

Look for:
- Metrics with unbounded tags
- High cardinality custom metrics
- Redundant metrics

**D. Infrastructure Right-Sizing:**
Query for:
- Oversized instances (low utilization)
- Unused reserved capacity
- Non-production over-provisioning

**Step 3: Calculate Potential Savings**

For each optimization opportunity:

**Opportunity Template:**
```
## Optimization: [Name]

**Current Cost:** $[Amount]/month
**Potential Savings:** $[Amount]/month ([%])
**Effort:** [Low/Medium/High]
**Risk:** [Low/Medium/High]
**Impact on Observability:** [None/Minor/Significant]

**Implementation:**
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Validation:**
- MCP Query: [Query to confirm]
- Success Metric: [Measurement]
```

**Step 4: Prioritization Matrix**

| Opportunity | Savings | Effort | Risk | Priority |
|-------------|---------|--------|------|----------|
| [Opp 1] | $[X]/mo | Low | Low | P0 (Do first) |
| [Opp 2] | $[X]/mo | Med | Low | P1 |
| [Opp 3] | $[X]/mo | High | Med | P2 |

**Priority Calculation:**
- P0: High savings, low effort, low risk
- P1: High savings, medium effort, low risk OR medium savings, low effort
- P2: Everything else

**Step 5: Create Implementation Plan**

## Cost Optimization Roadmap

### Phase 1: Quick Wins (Week 1-2)
**Target Savings:** $[Amount]/month

- [ ] **Decommission unused services**
  - Services: [LIST]
  - Savings: $[Amount]/month
  - Owner: [Team]
  - Validation: Service request count = 0 for 30 days

- [ ] **Exclude debug logs from production**
  - Current volume: [N] logs/day
  - Potential exclusion: [%]
  - Savings: $[Amount]/month
  - Owner: [Team]
  - Validation: Log volume reduced by [%]

### Phase 2: Structural Improvements (Week 3-6)
**Target Savings:** $[Amount]/month

- [ ] **Right-size non-production environments**
  - Environments: [LIST]
  - Savings: $[Amount]/month
  - Owner: [Team]

- [ ] **Optimize metric cardinality**
  - Metrics to optimize: [LIST]
  - Savings: $[Amount]/month
  - Owner: [Team]

### Phase 3: Advanced Optimization (Ongoing)
**Target Savings:** $[Amount]/month

- [ ] **Implement Flex Logs**
  - Use cases: [DESCRIPTION]
  - Savings: $[Amount]/month

- [ ] **Reserved capacity optimization**
  - Savings: $[Amount]/month

**Step 6: Cost Governance**

Implement ongoing cost management:

1. **Cost Attribution by Team**
   - Track spending per team
   - Set budgets and alerts
   - Monthly reviews

2. **Automated Alerts**
   - Alert on cost spikes >20%
   - Alert on budget overruns
   - Alert on unused resources

3. **Regular Reviews**
   - Monthly cost review meetings
   - Quarterly optimization sprints
   - Annual architecture reviews

**Report Deliverables:**

## Level 3 Cost Optimization Report

### Executive Summary
- Current Monthly Spend: $[Amount]
- Baseline (Level 0): $[Amount]
- Optimization Target (20%): $[Amount] savings
- Identified Opportunities: $[Amount] ([%])
- Status: [✅ Exceeds target / ⚠️ On track / ❌ Below target]

### Current Cost Breakdown
[Charts/tables showing spend by service, team, environment]

### Optimization Opportunities
[Detailed list with savings calculations]

### Implementation Roadmap
[Phased approach with timeline]

### Cost Governance
[Policies and procedures for ongoing management]

### Success Metrics
- Monthly spend: $[Current] → $[Target]
- Cost per service: $[Current] → $[Target]
- Observability ROI: [Improvement]

---

**Save Report To:**
`maturity-levels/level-3-managed/cost-optimization-report-[DATE].md`

**Track Progress:**
```
# Re-run monthly to track optimization progress
/level3-cost

# Compare against baseline
Current: $[Amount]
Target: $[Baseline × 0.80]
Progress: [%] toward goal
```
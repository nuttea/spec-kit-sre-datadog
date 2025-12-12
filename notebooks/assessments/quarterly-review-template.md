---
title: Quarterly SRE Business Review
type: assessment
version: 1.0
created: 2025-12-12
tags: [assessment, quarterly, business-review, executive]
---

# Quarterly SRE Business Review

**Metadata**
- Quarter: Q{{QUARTER}} {{YEAR}}
- Date Range: {{START_DATE}} to {{END_DATE}}
- Owner: {{OWNER}}
- Status: Draft
- Priority: P1
- Audience: Executive Leadership, Engineering Leadership

## Executive Summary (1 Page)

### Quarter Highlights

**Maturity Level**: _____ → _____ (Change: _____)

**Overall Score**: _____ / 100 (Change: +/- _____)

**Key Achievements**:
1.
2.
3.

**Business Impact**:
- Availability: _____% (Target: _____%)
- MTTR: _____ minutes (Change: _____%)
- Cost Efficiency: $_____ (Change: _____%)
- Incident Reduction: _____% fewer incidents

### ROI Summary

| Investment Area | Cost | Benefit | ROI |
|----------------|------|---------|-----|
| Infrastructure | $_____ | _____ | _____% |
| Tooling | $_____ | _____ | _____% |
| Training | $_____ | _____ | _____% |
| **Total** | **$_____** | **_____** | **_____%** |

## Quarter Scorecard

### All 8 Dimensions

```
Data Collection Period: Last 90 days
```

#### 1. Infrastructure Coverage (Weight: 15%)

**Query**:
```
search_datadog_hosts(query="*")
get_datadog_metric(queries=["avg:system.cpu.user{*}"], from="now-90d")
```

**Metrics**:
- Total Hosts: _____
- Agent Coverage: _____%
- Active Monitoring: _____

**Score**: _____ / 100 (Q-1: _____, Change: +/- _____)

**Assessment**:

#### 2. Service Catalog (Weight: 10%)

**Query**:
```
search_datadog_services(query="*", detailed_output=true)
```

**Metrics**:
- Total Services: _____
- Documented Services: _____%
- APM Instrumented: _____

**Score**: _____ / 100 (Q-1: _____, Change: +/- _____)

**Assessment**:

#### 3. Tagging Compliance (Weight: 15%)

**Query**:
```
search_datadog_hosts(query="*", include_all_tags=true)
analyze_datadog_logs(filter="*", sql_query="SELECT count(*) FROM logs WHERE env IS NOT NULL", from="now-90d")
```

**Metrics**:
- UST Coverage (env, service, version): _____%
- Recommended Tags (team, application): _____%
- Tag Quality Score: _____ / 100

**Score**: _____ / 100 (Q-1: _____, Change: +/- _____)

**Assessment**:

#### 4. Monitoring Quality (Weight: 15%)

**Query**:
```
search_datadog_monitors(query="*")
search_datadog_monitors(query="status:alert")
search_datadog_monitors(query="status:'No Data'")
```

**Metrics**:
- Total Monitors: _____
- Coverage (critical services): _____%
- Alert/No Data Rate: _____%
- Monitor Quality Score: _____ / 100

**Score**: _____ / 100 (Q-1: _____, Change: +/- _____)

**Assessment**:

#### 5. Log Management (Weight: 10%)

**Query**:
```
analyze_datadog_logs(filter="*", sql_query="SELECT count(*) FROM logs", from="now-90d")
analyze_datadog_logs(filter="status:error", sql_query="SELECT count(*) FROM logs", from="now-90d")
```

**Metrics**:
- Total Logs (90d): _____
- Error Rate: _____%
- Index Efficiency: _____%

**Score**: _____ / 100 (Q-1: _____, Change: +/- _____)

**Assessment**:

#### 6. Cost Optimization (Weight: 10%)

**Query**:
```
get_datadog_metric(queries=["sum:all.cost{*}.rollup(sum, daily)"], use_cloud_cost=true, from="now-90d")
```

**Metrics**:
- Quarterly Cost: $_____
- Cost per Service: $_____
- Optimization Savings: $_____

**Score**: _____ / 100 (Q-1: _____, Change: +/- _____)

**Assessment**:

#### 7. Incident Management (Weight: 15%)

**Query**:
```
search_datadog_incidents(query="state:resolved", from="now-90d")
get_datadog_incident(incident_id="LATEST_INCIDENT_ID")
```

**Metrics**:
- Total Incidents: _____
- Average MTTR: _____ minutes
- SEV-1 Incidents: _____
- Incident Rate Trend: _____

**Score**: _____ / 100 (Q-1: _____, Change: +/- _____)

**Assessment**:

#### 8. Advanced Capabilities (Weight: 10%)

**Query**:
```
search_datadog_spans(query="*", from="now-90d")
search_datadog_dashboards(query="*")
```

**Metrics**:
- APM Span Volume: _____
- Custom Dashboards: _____
- SLO Adoption: _____%

**Score**: _____ / 100 (Q-1: _____, Change: +/- _____)

**Assessment**:

## Trend Analysis

### Quarter-over-Quarter Progression

| Dimension | Q-3 | Q-2 | Q-1 | Current | Trend |
|-----------|-----|-----|-----|---------|-------|
| Infrastructure Coverage | | | | | |
| Service Catalog | | | | | |
| Tagging Compliance | | | | | |
| Monitoring Quality | | | | | |
| Log Management | | | | | |
| Cost Optimization | | | | | |
| Incident Management | | | | | |
| Advanced Capabilities | | | | | |

**Overall Maturity Trend**: Level _____ → Level _____ → Level _____ → Level _____

### Infrastructure Changes

**Query**:
```
search_datadog_hosts(query="*")
search_datadog_events(query="source:infrastructure", from="now-90d")
```

**Summary**:
- Hosts Added: _____
- Hosts Removed: _____
- Major Migrations: _____
- Infrastructure Projects: _____

## ROI Calculations

### Incident Cost Avoidance

**Formula**: (Incidents Prevented × Avg Cost per Incident) + (MTTR Reduction × Hourly Rate × Incident Count)

| Metric | Q-1 | Current | Improvement |
|--------|-----|---------|-------------|
| Total Incidents | | | |
| Average MTTR (min) | | | |
| Estimated Cost/Incident | $_____ | $_____ | $_____ |
| **Total Savings** | | | **$_____** |

### Operational Efficiency

| Area | Time Saved (hrs) | Hourly Rate | Value |
|------|------------------|-------------|-------|
| Reduced investigation time | | $_____ | $_____ |
| Automated remediation | | $_____ | $_____ |
| Improved on-call | | $_____ | $_____ |
| **Total** | **_____** | | **$_____** |

### Cost Optimization

| Optimization | Previous Cost | Current Cost | Savings |
|-------------|---------------|--------------|---------|
| Cloud resources | $_____ | $_____ | $_____ |
| Log optimization | $_____ | $_____ | $_____ |
| Metric cardinality | $_____ | $_____ | $_____ |
| **Total** | **$_____** | **$_____** | **$_____** |

## Team Highlights

### Accomplishments

1. **Major Achievement 1**
   - Description:
   - Impact:
   - Metrics:
   - Recognition:

2. **Major Achievement 2**
   - Description:
   - Impact:
   - Metrics:
   - Recognition:

3. **Major Achievement 3**
   - Description:
   - Impact:
   - Metrics:
   - Recognition:

### Challenges Overcome

1.
2.
3.

### Team Growth

- Training Hours: _____
- Certifications Earned: _____
- Knowledge Sharing Sessions: _____
- Team Size: _____ (Change: _____)

## Cost Analysis

### Quarterly Spend Breakdown

**Query**:
```
get_datadog_metric(
  queries=[
    "sum:all.cost{*} by {service}.rollup(sum, daily)",
    "sum:all.cost{*} by {team}.rollup(sum, daily)",
    "sum:all.cost{*} by {env}.rollup(sum, daily)"
  ],
  use_cloud_cost=true,
  from="now-90d"
)
```

#### By Service (Top 10)

| Service | Cost | % of Total | Change |
|---------|------|------------|--------|
| | $_____ | ____% | +/- ____% |
| | $_____ | ____% | +/- ____% |
| | $_____ | ____% | +/- ____% |

#### By Team

| Team | Cost | % of Total | Change |
|------|------|------------|--------|
| | $_____ | ____% | +/- ____% |
| | $_____ | ____% | +/- ____% |

#### By Environment

| Environment | Cost | % of Total | Change |
|-------------|------|------------|--------|
| Production | $_____ | ____% | +/- ____% |
| Staging | $_____ | ____% | +/- ____% |
| Development | $_____ | ____% | +/- ____% |

## Next Quarter Roadmap

### Strategic Priorities

1. **Priority 1: _____**
   - Objective:
   - Success Metrics:
   - Timeline:
   - Resources Required:

2. **Priority 2: _____**
   - Objective:
   - Success Metrics:
   - Timeline:
   - Resources Required:

3. **Priority 3: _____**
   - Objective:
   - Success Metrics:
   - Timeline:
   - Resources Required:

### Target Maturity Level

**Current**: Level _____
**Target**: Level _____
**Gap Analysis**: See `/gap-analysis` command output
**Upgrade Plan**: See `/upgrade-plan` command output

### Investment Requests

| Initiative | Cost | Expected ROI | Priority |
|-----------|------|--------------|----------|
| | $_____ | _____% | P_____ |
| | $_____ | _____% | P_____ |
| | $_____ | _____% | P_____ |

## Action Items

### Immediate (This Month)
- [ ] Action 1 (Owner: _____, Due: _____)
- [ ] Action 2 (Owner: _____, Due: _____)
- [ ] Action 3 (Owner: _____, Due: _____)

### Short-term (Next Quarter)
- [ ] Action 1 (Owner: _____, Due: _____)
- [ ] Action 2 (Owner: _____, Due: _____)
- [ ] Action 3 (Owner: _____, Due: _____)

### Long-term (Future Quarters)
- [ ] Action 1 (Owner: _____, Due: _____)
- [ ] Action 2 (Owner: _____, Due: _____)

## References

- **Previous Quarter Review**: [Link]
- **Executive Dashboard**: [Link]
- **Cost Dashboard**: [Link]
- **Incident Log**: [Link]
- **Team Objectives**: [Link]
- **Related Notebooks**: [Links]

---

**Template Usage Notes**:
1. Start this review 2 weeks before quarter end
2. Run all data collection queries
3. Compile trend data from previous quarters
4. Calculate ROI metrics
5. Prepare executive presentation
6. Share draft with leadership 1 week before QBR
7. Finalize and present at QBR meeting
8. Archive in Datadog Notebook: `/save-to-notebook`

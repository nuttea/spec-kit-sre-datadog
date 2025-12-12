---
title: Weekly SRE Maturity Assessment
type: assessment
version: 1.0
created: 2025-12-12
tags: [assessment, weekly, maturity, sre]
---

# Weekly SRE Maturity Assessment

**Metadata**
- Week Number: W{{WEEK_NUMBER}}
- Date Range: {{START_DATE}} to {{END_DATE}}
- Owner: {{OWNER}}
- Status: Draft
- Priority: P2

## Objective

Quick weekly checkpoint to track SRE maturity progress across 8 dimensions and identify blockers requiring immediate attention.

## Success Criteria
- [ ] All 8 dimension scores updated
- [ ] Week-over-week changes calculated
- [ ] Top blockers identified
- [ ] Action items assigned for next week

## Data Collection

### Infrastructure Coverage

```
Query: search_datadog_hosts(query="*")
Result: {{HOST_COUNT}} hosts
```

**Score (0-100)**: _____

### Service Catalog

```
Query: search_datadog_services(query="*")
Result: {{SERVICE_COUNT}} services
```

**Score (0-100)**: _____

### Monitoring Quality

```
Query: search_datadog_monitors(query="*")
Active: _____ | Alert: _____ | No Data: _____
```

**Score (0-100)**: _____

### Incident Management

```
Query: search_datadog_incidents(query="state:(active OR stable)", from="now-7d")
Result: {{INCIDENT_COUNT}} incidents this week
```

**Score (0-100)**: _____

### Log Management

```
Query: analyze_datadog_logs(filter="*", sql_query="SELECT count(*) FROM logs", from="now-7d")
Result: {{LOG_COUNT}} logs
```

**Score (0-100)**: _____

### Tagging Compliance

```
Query: search_datadog_hosts(query="*", include_all_tags=true)
UST Coverage: ____%
```

**Score (0-100)**: _____

### Cost Optimization

```
Query: get_datadog_metric(queries=["sum:all.cost{*}.rollup(sum, daily)"], use_cloud_cost=true, from="now-7d")
Weekly Cost: $_____
```

**Score (0-100)**: _____

### Advanced Capabilities

```
APM Spans: search_datadog_spans(query="*", from="now-7d")
Result: {{SPAN_COUNT}} spans
```

**Score (0-100)**: _____

## Week Summary

### Overall Maturity
- **Level**: _____ (0-5)
- **Average Score**: _____ / 100
- **Change from last week**: +/- _____

### Week-over-Week Changes

| Dimension | Last Week | This Week | Change |
|-----------|-----------|-----------|--------|
| Infrastructure Coverage | | | |
| Service Catalog | | | |
| Monitoring Quality | | | |
| Incident Management | | | |
| Log Management | | | |
| Tagging Compliance | | | |
| Cost Optimization | | | |
| Advanced Capabilities | | | |

## Top 3 Accomplishments

1. **Accomplishment 1**
   - Description:
   - Impact:
   - Evidence:

2. **Accomplishment 2**
   - Description:
   - Impact:
   - Evidence:

3. **Accomplishment 3**
   - Description:
   - Impact:
   - Evidence:

## Top 3 Blockers

1. **Blocker 1**
   - Issue:
   - Impact:
   - Owner:
   - Status:

2. **Blocker 2**
   - Issue:
   - Impact:
   - Owner:
   - Status:

3. **Blocker 3**
   - Issue:
   - Impact:
   - Owner:
   - Status:

## Action Items for Next Week

- [ ] Task 1 (Owner: _____, Priority: _____)
- [ ] Task 2 (Owner: _____, Priority: _____)
- [ ] Task 3 (Owner: _____, Priority: _____)
- [ ] Task 4 (Owner: _____, Priority: _____)
- [ ] Task 5 (Owner: _____, Priority: _____)

## References

- **Previous Week Assessment**: [Link]
- **Dashboard**: [Link to main SRE dashboard]
- **Incident Log**: [Link to incident tracker]
- **Related Notebooks**: [Links]

---

**Template Usage Notes**:
1. Copy this template at the start of each week
2. Run the pre-filled queries against your Datadog account
3. Fill in scores based on query results and maturity definitions
4. Compare to previous week's assessment
5. Share with team and stakeholders
6. Optionally push to Datadog Notebook: `/save-to-notebook`
---
title: Cost Optimization Runbook
type: runbook
version: 1.0
created: 2025-12-12
tags: [runbook, cost, finops, optimization]
---

# Cost Optimization Runbook

**Purpose**: Step-by-step guide for identifying and implementing cost optimization opportunities

## Cost Optimization Framework

```
Cost Baseline → Identify Waste → Prioritize → Implement → Validate → Monitor
```

## Phase 1: Establish Cost Baseline

### Step 1.1: Calculate Total Cost

**Query 90-day cost**:
```
get_datadog_metric(
  queries=["sum:all.cost{*}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-90d"
)
```

**Baseline Metrics**:
- Daily average: $_____
- Monthly projection: $_____
- 90-day total: $_____

### Step 1.2: Cost Breakdown by Service

**Query**:
```
get_datadog_metric(
  queries=["sum:all.cost{*} by {service}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-30d"
)
```

**Top 10 Services by Cost**:
| Service | Monthly Cost | % of Total |
|---------|-------------|------------|
| | $_____ | ____% |
| | $_____ | ____% |

### Step 1.3: Cost Breakdown by Team

**Query**:
```
get_datadog_metric(
  queries=["sum:all.cost{*} by {team}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-30d"
)
```

**Cost by Team**:
| Team | Monthly Cost | Services | Priority |
|------|-------------|----------|----------|
| | $_____ | _____ | P_____ |

---

## Phase 2: Identify Waste

### Category 1: Idle/Unused Resources

**Step 2.1: Find Idle Hosts**

**Query low CPU hosts**:
```
search_datadog_hosts(query="*")

get_datadog_metric(
  queries=["avg:system.cpu.user{*} by {host}"],
  from="now-7d"
)
```

**Criteria**: CPU <5% for 7+ days

**Idle Hosts**:
| Host | Avg CPU | Service | Cost/Month | Action |
|------|---------|---------|------------|--------|
| | ____% | | $_____ | Decommission |

**Potential Savings**: $_____/month

**Implementation**:
- [ ] Verify with service owner
- [ ] Check if dev/test environment
- [ ] Schedule decommission
- [ ] Update inventory

---

**Step 2.2: Identify Unused Services**

**Query services with no traffic**:
```
search_datadog_services(query="*")

get_datadog_metric(
  queries=["sum:trace.*.request.hits{*} by {service}.as_rate()"],
  from="now-30d"
)
```

**Criteria**: 0 requests for 30+ days

**Unused Services**:
| Service | Last Request | Cost/Month | Owner | Action |
|---------|-------------|------------|-------|--------|
| | | $_____ | | Archive |

**Potential Savings**: $_____/month

---

### Category 2: Over-Provisioned Resources

**Step 2.3: Right-Size Instances**

**Query under-utilized instances**:
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

**Criteria**: CPU <20% AND Memory <40% for 30 days

**Right-Sizing Opportunities**:
| Host | Current Size | CPU | Memory | Target Size | Savings |
|------|-------------|-----|--------|-------------|---------|
| | m5.2xlarge | 15% | 35% | m5.xlarge | $_____ |

**Potential Savings**: $_____/month

**Implementation Checklist**:
- [ ] Test in staging first
- [ ] Schedule maintenance window
- [ ] Update capacity planning
- [ ] Monitor post-change
- [ ] Validate savings

---

### Category 3: Log Optimization

**Step 2.4: Analyze Log Volume**

**Query log volume by service**:
```
analyze_datadog_logs(
  filter="*",
  sql_query="SELECT service, count(*) as logs, sum(length(message)) as bytes FROM logs GROUP BY service ORDER BY logs DESC LIMIT 20",
  from="now-7d"
)
```

**High Volume Services**:
| Service | Logs/Day | GB/Day | Cost/Month | Optimization |
|---------|----------|--------|------------|--------------|
| | _____ M | _____ | $_____ | Sampling |

**Potential Savings**: $_____/month

**Optimization Techniques**:

1. **Debug Log Filtering**:
   ```
   # Exclude debug logs in production
   Create exclusion filter: status:debug env:prod
   ```

2. **Sampling**:
   ```
   # Sample 10% of high-volume non-error logs
   Create sampling rule: 10% for status:info service:high-volume
   ```

3. **Deduplication**:
   ```
   # Remove duplicate logs
   Configure log aggregation at source
   ```

4. **Structured Logging**:
   ```
   # Use JSON logging to reduce size
   # Remove redundant fields
   ```

---

**Step 2.5: Optimize Log Retention**

**Query log indexes**:
```
# Via Datadog UI: Logs → Configuration → Indexes
# Review retention periods
```

**Index Optimization**:
| Index | Current Retention | Volume/Day | Cost/Month | Target Retention | Savings |
|-------|------------------|------------|------------|------------------|---------|
| main | 15 days | 100GB | $_____ | 7 days | $_____ |
| debug | 15 days | 50GB | $_____ | 3 days | $_____ |

**Potential Savings**: $_____/month

**Implementation**:
- [ ] Archive old logs to S3
- [ ] Update retention policies
- [ ] Configure Flex Logs for long retention
- [ ] Validate accessibility

---

### Category 4: Metric Optimization

**Step 2.6: Identify High Cardinality Metrics**

**Query custom metrics**:
```
search_datadog_metrics(name_filter="*")
```

**High Cardinality Metrics**:
| Metric | Cardinality | Cost/Month | Reason | Action |
|--------|-------------|------------|--------|--------|
| | >10K series | $_____ | Unbounded tag | Remove tag |

**Potential Savings**: $_____/month

**Common High Cardinality Sources**:
- User IDs in tags
- Request IDs in tags
- Timestamps in tags
- Session IDs in tags

**Remediation**:
- [ ] Remove unbounded tags
- [ ] Aggregate metrics
- [ ] Use metrics without limits
- [ ] Configure tag limits

---

### Category 5: Storage Optimization

**Step 2.7: Archive Old Data**

**Query storage costs**:
```
get_datadog_metric(
  queries=["sum:aws.s3.bucket_size_bytes{*} by {bucket_name}"],
  from="now-30d"
)
```

**Storage Optimization**:
| Type | Current | Target | Method | Savings |
|------|---------|--------|--------|---------|
| Logs | S3 Standard | S3 Glacier | Lifecycle policy | $_____ |
| Traces | 30 days | 15 days | Retention config | $_____ |

**Potential Savings**: $_____/month

---

## Phase 3: Prioritization Matrix

### Calculate ROI for Each Optimization

| Opportunity | Savings/Mo | Effort | Risk | ROI | Priority |
|------------|-----------|--------|------|-----|----------|
| Decommission idle hosts | $_____ | Low | Low | High | P1 |
| Right-size instances | $_____ | Med | Med | Med | P1 |
| Log sampling | $_____ | Low | Low | High | P1 |
| Archive old data | $_____ | Low | Low | High | P2 |
| Reduce retention | $_____ | Med | Med | Med | P2 |
| Fix high cardinality | $_____ | High | Low | Low | P3 |

**Total Potential Savings**: $_____/month (____% reduction)

---

## Phase 4: Implementation

### P1 Optimizations (Week 1-2)

#### Task 1: Decommission Idle Resources

**Checklist**:
- [ ] Get approval from service owners
- [ ] Verify no dependencies
- [ ] Take final snapshot
- [ ] Terminate resources
- [ ] Update inventory
- [ ] Validate savings

**Timeline**: _____ days
**Owner**: _____
**Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete

---

#### Task 2: Implement Log Sampling

**Checklist**:
- [ ] Identify high-volume services
- [ ] Configure exclusion filters
- [ ] Set up sampling rules
- [ ] Test in staging
- [ ] Deploy to production
- [ ] Monitor impact

**Timeline**: _____ days
**Owner**: _____
**Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete

---

#### Task 3: Right-Size Instances

**Checklist**:
- [ ] Select instances to resize
- [ ] Test new size in staging
- [ ] Schedule maintenance
- [ ] Resize instances
- [ ] Monitor performance
- [ ] Validate no degradation

**Timeline**: _____ days
**Owner**: _____
**Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete

---

### P2 Optimizations (Week 3-4)

[Similar structure for P2 tasks]

---

## Phase 5: Validation

### Validate Savings

**Re-run baseline query**:
```
get_datadog_metric(
  queries=["sum:all.cost{*}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="{{IMPLEMENTATION_DATE}}",
  to="now"
)
```

**Savings Tracking**:
| Optimization | Target Savings | Actual Savings | Achievement |
|-------------|---------------|----------------|-------------|
| Idle hosts | $_____ | $_____ | ____% |
| Log sampling | $_____ | $_____ | ____% |
| Right-sizing | $_____ | $_____ | ____% |
| **Total** | **$_____** | **$_____** | **____%** |

### Validate No Degradation

**Check service health**:
- [ ] Error rates stable
- [ ] Latency unchanged
- [ ] No customer complaints
- [ ] Monitoring coverage maintained

---

## Phase 6: Cost Governance

### Ongoing Monitoring

**Set up cost alerts**:
```
# Alert on 10%+ daily cost increase
Monitor: sum(last_1d):sum:all.cost{*} > 1.1 * avg(last_7d):sum:all.cost{*}
```

**Alerts**:
- [ ] Daily cost anomaly alert
- [ ] Monthly budget threshold (80%)
- [ ] Service cost spike alert
- [ ] Idle resource alert

### Monthly Cost Review Process

**Schedule**: First Monday of each month

**Agenda**:
1. Review total cost vs budget
2. Analyze cost changes (service/team)
3. Review optimization backlog
4. Identify new opportunities
5. Assign optimization tasks

**Attendees**:
- Engineering Manager
- FinOps Lead
- Service Owners
- SRE Team

### Cost Allocation

**Implement chargeback**:
- [ ] Tag all resources with team/service
- [ ] Generate monthly cost reports
- [ ] Share with team leads
- [ ] Set team budgets
- [ ] Track team-level optimization

### Cost Optimization Backlog

**Maintain backlog**:
| Opportunity | Savings | Effort | Priority | Owner | Status |
|------------|---------|--------|----------|-------|--------|
| | $_____ | | P_____ | | ⚪ |
| | $_____ | | P_____ | | 🟡 |

---

## Common Pitfalls

### Avoid These Mistakes

1. **Optimizing without measurement**
   - Always establish baseline first
   - Track savings with data

2. **Ignoring service owner input**
   - Get approval before changes
   - Understand usage patterns

3. **Over-aggressive optimization**
   - Don't compromise performance
   - Test thoroughly

4. **One-time optimization**
   - Make it ongoing process
   - Review monthly

5. **Lack of governance**
   - Set budgets
   - Regular reviews
   - Accountability

---

## Success Metrics

Track these KPIs monthly:

| Metric | Target | Current | Status |
|--------|--------|---------|--------|
| Total monthly cost | <$_____ | $_____ | 🟢/🟡/🔴 |
| Cost per service | <$_____ | $_____ | 🟢/🟡/🔴 |
| Idle resource rate | <5% | ____% | 🟢/🟡/🔴 |
| Cost optimization savings | >$_____ | $_____ | 🟢/🟡/🔴 |
| Cost growth rate | <10%/quarter | ____% | 🟢/🟡/🔴 |

---

## References

- **Cost Dashboard**: [Link]
- **Budget Tracking**: [Spreadsheet]
- **Optimization Backlog**: [Jira]
- **Team Cost Reports**: [Link]
- **FinOps Documentation**: [Link]

---

**Runbook Version**: 1.0
**Last Optimization**: _____
**Next Review**: _____
**Total Savings This Year**: $_____

---

**Template Usage Notes**:
1. Run this runbook monthly or quarterly
2. Customize thresholds for your organization
3. Track all optimizations in backlog
4. Celebrate wins with team
5. Share learnings across teams
6. Archive results in Datadog Notebook: `/save-to-notebook`

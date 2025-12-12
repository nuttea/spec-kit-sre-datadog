---
title: Alert Response Runbook
type: runbook
version: 1.0
created: 2025-12-12
tags: [runbook, alerts, incident-response, on-call]
---

# Alert Response Runbook

**Purpose**: Standard operating procedures for responding to Datadog alerts

## Alert Triage Decision Tree

```
Alert Received
    │
    ├─> Severity: P0/P1 (Critical)
    │   ├─> Customer impact?: YES → Declare incident (SEV-1 or SEV-2)
    │   ├─> Service down?: YES → Immediate escalation + war room
    │   └─> False alarm?: YES → Acknowledge + fix monitor
    │
    ├─> Severity: P2 (Warning)
    │   ├─> Trending worse?: YES → Investigate immediately
    │   ├─> Known issue?: YES → Follow existing plan
    │   └─> Intermittent?: YES → Investigate during business hours
    │
    └─> Severity: P3/P4 (Info)
        └─> Acknowledge + add to backlog
```

## Initial Response Checklist

When alert fires:
- [ ] **Acknowledge** alert within 5 minutes
- [ ] **Assess** severity and customer impact
- [ ] **Check** service dashboard
- [ ] **Review** recent changes (deployments, config)
- [ ] **Escalate** if needed
- [ ] **Communicate** status

## Common Alert Types

### 1. High Latency Alert

**Alert**: `avg:trace.{service}.request.duration{env:prod} > 2000ms`

**Triage Steps**:
1. Check service dashboard for request volume spike
2. Review recent deployments (last 2 hours)
3. Check database performance
4. Check external dependencies

**Investigation Queries**:
```
# Get slow traces
search_datadog_spans(
  query="service:{{SERVICE}} resource_name:* duration:>2s",
  from="now-15m"
)

# Check request volume
get_datadog_metric(
  queries=["sum:trace.{{SERVICE}}.request.hits{*}.as_rate()"],
  from="now-1h"
)

# Check database latency
get_datadog_metric(
  queries=["avg:postgresql.queries{*}"],
  from="now-1h"
)
```

**Common Causes**:
- Database slow queries
- External API degradation
- Resource saturation (CPU/Memory)
- Cache misses
- Inefficient code deployed

**Resolution Steps**:
1. If deployment-related: Consider rollback
2. If database: Check query plan, add indexes
3. If external: Implement circuit breaker
4. If resource: Scale up
5. If cache: Clear/warm cache

---

### 2. High Error Rate Alert

**Alert**: `error_rate > 5%`

**Triage Steps**:
1. Check error types and messages
2. Review recent deployments
3. Check dependency health
4. Sample error traces

**Investigation Queries**:
```
# Get error distribution
analyze_datadog_logs(
  filter="status:error service:{{SERVICE}}",
  sql_query="SELECT error.kind, count(*) as errors FROM logs GROUP BY error.kind ORDER BY errors DESC LIMIT 10",
  from="now-15m"
)

# Get error traces
search_datadog_spans(
  query="service:{{SERVICE}} status:error",
  from="now-15m",
  custom_attributes=["error.message", "http.status_code"]
)

# Check deployment events
search_datadog_events(
  query="service:{{SERVICE}} deployment",
  from="now-2h"
)
```

**Common Causes**:
- Recent deployment with bugs
- External dependency failure
- Database connection issues
- Invalid input/requests
- Configuration error

**Resolution Steps**:
1. If new errors after deployment: Rollback immediately
2. If dependency: Implement fallback
3. If database: Check connection pool
4. If validation: Add input validation
5. If config: Revert configuration

---

### 3. Low Throughput Alert

**Alert**: `request_rate < 10/s for 15 minutes`

**Triage Steps**:
1. Check if service is up
2. Check load balancer health
3. Check upstream services
4. Check network connectivity

**Investigation Queries**:
```
# Check service health
search_datadog_hosts(query="service:{{SERVICE}}")

# Check request rate
get_datadog_metric(
  queries=["sum:trace.{{SERVICE}}.request.hits{*}.as_rate()"],
  from="now-1h"
)

# Check upstream services
search_datadog_services(query="*")
```

**Common Causes**:
- Service down/crashed
- Load balancer misconfiguration
- Network partition
- Upstream service blocking traffic
- DNS issues

**Resolution Steps**:
1. If service down: Restart service
2. If load balancer: Check routing rules
3. If network: Check firewall/security groups
4. If upstream: Fix upstream issue
5. If DNS: Check DNS records

---

### 4. Resource Saturation Alert

**Alert**: `system.cpu.user > 90%` or `system.mem.used > 95%`

**Triage Steps**:
1. Check recent traffic changes
2. Review resource usage trends
3. Check for memory leaks
4. Check for runaway processes

**Investigation Queries**:
```
# CPU usage by host
get_datadog_metric(
  queries=["avg:system.cpu.user{service:{{SERVICE}}} by {host}"],
  from="now-1h"
)

# Memory usage by host
get_datadog_metric(
  queries=["avg:system.mem.used{service:{{SERVICE}}} by {host}"],
  from="now-1h"
)

# Process list (if process integration enabled)
# Check logs for OOM errors
search_datadog_logs(
  query="service:{{SERVICE}} (OOM OR 'out of memory')",
  from="now-1h"
)
```

**Common Causes**:
- Traffic spike
- Memory leak
- Inefficient code
- Under-provisioned resources
- Zombie processes

**Resolution Steps**:
1. If traffic spike: Scale horizontally
2. If memory leak: Restart affected instances
3. If inefficient: Optimize code
4. If under-provisioned: Scale vertically
5. If zombies: Kill processes

---

### 5. Database Connection Pool Exhaustion

**Alert**: `database.connection.used > 90%`

**Triage Steps**:
1. Check active connections
2. Check long-running queries
3. Check connection leak
4. Check request volume

**Investigation Queries**:
```
# Connection pool usage
get_datadog_metric(
  queries=["avg:postgresql.connections{*}"],
  from="now-1h"
)

# Active queries
get_datadog_metric(
  queries=["avg:postgresql.queries{*}"],
  from="now-1h"
)

# Check for slow queries
search_datadog_logs(
  query="service:{{SERVICE}} slow_query",
  from="now-1h"
)
```

**Common Causes**:
- Connection leak (not closed)
- Slow queries holding connections
- Traffic spike
- Pool size too small
- Long-running transactions

**Resolution Steps**:
1. If leak: Restart application
2. If slow queries: Kill long-running queries
3. If traffic: Increase pool size
4. If transactions: Set timeout
5. Long-term: Fix connection handling code

---

## Escalation Procedures

### When to Escalate

Escalate if:
- [ ] Unable to resolve within 15 minutes
- [ ] Customer-facing impact (SEV-1/SEV-2)
- [ ] Service completely down
- [ ] Unclear root cause
- [ ] Need additional expertise
- [ ] Multi-service issue

### Escalation Paths

**Level 1** → On-call Engineer (You)
- Initial response
- Basic troubleshooting
- Common issues

**Level 2** → Senior Engineer / Tech Lead
- Complex issues
- Requires deep system knowledge
- Architecture decisions

**Level 3** → Engineering Manager
- Business decisions
- Resource allocation
- Customer communication

**Level 4** → CTO / VP Engineering
- Severe incidents (SEV-0, SEV-1)
- Executive communication
- Major business impact

### How to Escalate

1. **Document** current state and findings
2. **Page** next level using PagerDuty
3. **Brief** on Slack with summary
4. **Share** dashboard and relevant data
5. **Stay available** for questions

## Communication Guidelines

### Internal Communication (Slack)

**Alert channel**: `#alerts-{{SERVICE}}`

**Format**:
```
🔴 [SEV-1] {{SERVICE}} High Error Rate Alert

Status: Investigating
Started: 10:15 AM PST
Impact: 20% of users seeing errors
On-call: @engineer

Investigation:
- Error rate spiked to 25% at 10:15 AM
- Recent deployment at 10:00 AM (v1.2.3)
- Errors: "Database connection timeout"

Next steps:
- Rolling back to v1.2.2
- ETA: 5 minutes
```

**Update frequency**:
- SEV-1: Every 15 minutes
- SEV-2: Every 30 minutes
- SEV-3: When status changes

### External Communication (Status Page)

**When to post**:
- SEV-1: Always
- SEV-2: If customer-reported
- SEV-3: Generally no

**Message template**:
```
[{{DATE}} {{TIME}}] Investigating

We are investigating reports of {{ISSUE}}.
Updates will be provided as we learn more.

Affected Services: {{SERVICES}}
Impact: {{IMPACT_DESCRIPTION}}
```

## Post-Alert Actions

After alert resolved:
- [ ] **Document** resolution in alert comments
- [ ] **Update** runbook if new issue
- [ ] **Create** Jira ticket if needed
- [ ] **Review** alert threshold if false alarm
- [ ] **Schedule** postmortem if SEV-1/SEV-2
- [ ] **Communicate** resolution

## Alert Quality Management

### Alert Review Checklist

Review alerts weekly:
- [ ] Noise ratio acceptable? (<5 alerts/day)
- [ ] True positive rate high? (>80%)
- [ ] Actionable alerts? (clear next steps)
- [ ] Appropriate thresholds? (not too sensitive)
- [ ] Runbook links working?

### Improving Alert Quality

**If too many false positives**:
- Increase threshold
- Add multi-condition checks
- Increase evaluation window
- Add time-of-day logic

**If missing real issues**:
- Decrease threshold
- Add more granular monitors
- Monitor more signals
- Add anomaly detection

**If unclear what to do**:
- Add runbook links
- Add context in alert message
- Add suggested queries
- Link to dashboard

## On-Call Best Practices

1. **Prepare**:
   - Keep laptop charged
   - Test PagerDuty notifications
   - Review common alerts
   - Bookmark key dashboards

2. **During On-Call**:
   - Acknowledge alerts promptly
   - Document everything
   - Escalate when needed
   - Communicate proactively

3. **Handoff**:
   - Brief next on-call
   - Share ongoing issues
   - Update runbooks
   - Document learnings

## References

- **Service Dashboards**: [Link]
- **Monitor Definitions**: [Link]
- **PagerDuty Schedules**: [Link]
- **Escalation Matrix**: [Link]
- **Service Catalog**: [Link]

---

**Runbook Version**: 1.0
**Last Updated**: {{DATE}}
**Next Review**: {{NEXT_REVIEW_DATE}}

---

**Template Usage Notes**:
1. Customize for your services and alert types
2. Add service-specific alerts
3. Update escalation paths
4. Test procedures regularly
5. Keep runbook up-to-date
6. Review after each incident
7. Archive in Datadog Notebook: `/save-to-notebook`

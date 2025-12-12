# Level 1: Reactive Assessment

Assess readiness and compliance for Level 1 (Reactive - Initial Implementation).

**Level 1 Core Capabilities:**
- ≥80% agent deployment coverage
- Basic monitors configured for critical services
- Essential dashboards created
- Log collection from production services
- Incident response process established

**Execute these checks:**

1. **Agent Deployment Coverage** (Target: ≥80%)
   - Query: `search_datadog_hosts(filter="*")`
   - Query: `get_datadog_metric(queries=["count:datadog.agent.running{*} by {env}"])`
   - Calculate coverage percentage
   - Identify gaps by environment
   - Status: ✅ Pass (≥80%) / ❌ Fail (<80%)

2. **Monitor Coverage** (Target: ≥5 critical monitors)
   - Query: `search_datadog_monitors(query="priority:p1 OR priority:p2")`
   - Count configured monitors
   - Verify critical service coverage
   - Check monitor status and routing
   - Status: ✅ Pass (≥5 monitors) / ❌ Fail (<5)

3. **Dashboard Creation** (Target: Core dashboards exist)
   - Query: `search_datadog_dashboards(query="*")`
   - Verify infrastructure dashboard exists
   - Check service health dashboard
   - Validate log overview dashboard
   - Status: ✅ Pass (≥3 dashboards) / ❌ Fail (<3)

4. **Log Collection** (Target: Production services logging)
   - Query: `search_datadog_logs(query="env:prod", from="now-24h")`
   - Verify log sources from production
   - Check log volume consistency
   - Identify services not logging
   - Status: ✅ Pass (logs flowing) / ❌ Fail (no logs)

5. **Incident Tracking** (Target: Process documented)
   - Query: `search_datadog_incidents(query="*", from="now-30d")`
   - Verify incidents are being tracked
   - Check MTTR baseline exists
   - Validate on-call rotation
   - Status: ✅ Pass (tracking active) / ❌ Fail (not tracking)

**Graduation Criteria to Level 2:**
- ✅ Agent coverage validated >80% via MCP
- ✅ At least 10 actionable monitors configured
- ✅ Team using dashboards daily
- ✅ Log ingestion stable
- ✅ Incidents tracked in Datadog

**Deliver:**
- Overall Level 1 readiness: % complete
- Capability-by-capability status
- Gaps preventing graduation to Level 2
- Remediation steps with priorities
- Estimated timeline to Level 2

**Output:** Save to `maturity-levels/level-1-reactive/assessment-results.md`
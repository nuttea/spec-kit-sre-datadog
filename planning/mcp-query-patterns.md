# Datadog MCP Query Patterns for SRE Assessment

This document provides reusable query patterns for assessing SRE maturity using Datadog MCP tools.

## Overview

The Datadog MCP Server provides comprehensive access to observability data. This document organizes common query patterns by:
1. **Resource Type** (Hosts, Services, Logs, Metrics, etc.)
2. **Assessment Purpose** (Coverage, Compliance, Cost, Performance)
3. **Maturity Level** (Which level uses this pattern)

---

## Infrastructure Assessment Patterns

### Pattern: Complete Infrastructure Inventory

**Purpose**: Discover all monitored infrastructure
**Maturity Levels**: 0, 1
**Use Cases**: Initial discovery, coverage validation

```python
# Pattern: Full infrastructure inventory
search_datadog_hosts(
    context="Discovering all monitored infrastructure",
    filter="*",
    include_all_tags=True,
    max_tokens=50000
)
```

**Interpretation**:
- Count hosts by environment: `filter="env:prod"` vs `filter="env:*"`
- Identify untagged hosts: Look for hosts missing `env`, `service`, or `team` tags
- Calculate agent coverage: Running agents vs total cloud instances

**Follow-up Queries**:
```python
# Cloud provider comparison
search_datadog_hosts(filter="cloud_provider:aws")
search_datadog_hosts(filter="cloud_provider:azure")
search_datadog_hosts(filter="cloud_provider:gcp")

# Agent version distribution
search_datadog_hosts(filter="agent_version:*")
```

---

### Pattern: Agent Deployment Coverage

**Purpose**: Validate Datadog agent deployment percentage
**Maturity Levels**: 1, 2
**Use Cases**: Level 1 graduation, continuous monitoring

```python
# Pattern: Agent running metrics
get_datadog_metric(
    context="Calculating agent deployment coverage",
    queries=[
        "count:datadog.agent.running{*}",
        "count:datadog.agent.running{*} by {env}",
        "count:datadog.agent.running{*} by {cloud_provider}"
    ],
    from="now-1h",
    to="now"
)
```

**Calculation**:
```
Agent Coverage % = (Hosts with Agent Running / Total Cloud Instances) * 100

Level 1 Target: ≥80%
Level 2 Target: ≥95%
Level 3 Target: ≥98%
```

**Combined with Cloud Inventory**:
```python
# Get cloud instances (would need cloud integration metrics)
get_datadog_metric(
    queries=[
        "count:aws.ec2.host_ok{*}",
        "count:azure.vm.status{*}",
        "count:gcp.gce.instance.count{*}"
    ],
    from="now-1h"
)
```

---

## Tagging Compliance Patterns

### Pattern: Unified Service Tagging Compliance

**Purpose**: Validate env, service, version tag coverage
**Maturity Levels**: 2, 3
**Use Cases**: Level 2 assessment, continuous compliance

```python
# Pattern: Tagging compliance audit
search_datadog_hosts(
    context="Auditing unified service tagging compliance",
    filter="*",
    include_all_tags=True,
    max_tokens=30000
)
```

**Analysis Algorithm**:
```python
# Pseudo-code for compliance calculation
hosts = [all hosts from query]
required_tags = ["env", "service", "version"]  # UST tags

compliant_hosts = 0
for host in hosts:
    if all(tag in host.tags for tag in required_tags):
        compliant_hosts += 1

compliance_rate = (compliant_hosts / len(hosts)) * 100

# Level 2 Target: ≥95%
# Level 3 Target: ≥98%
```

**Detailed Tag Analysis**:
```python
# Pattern: Tag coverage by tag key
search_datadog_hosts(filter="env:*")  # Has env tag
search_datadog_hosts(filter="service:*")  # Has service tag
search_datadog_hosts(filter="version:*")  # Has version tag
search_datadog_hosts(filter="team:*")  # Has team tag
```

**Anti-Pattern Detection**:
```python
# Detect common tagging issues
search_datadog_hosts(filter="env:production")  # Should be "prod"
search_datadog_hosts(filter="env:dev")  # Correct format
search_datadog_hosts(filter="service:*-*-*")  # Overly complex names
```

---

## Service Assessment Patterns

### Pattern: Service Catalog Completeness

**Purpose**: Verify all services are catalogued with ownership
**Maturity Levels**: 2, 3
**Use Cases**: Service ownership validation, gap analysis

```python
# Pattern: Complete service inventory
search_datadog_services(
    context="Analyzing service catalog completeness",
    query="*",
    detailed_output=True,
    max_tokens=30000
)
```

**Ownership Analysis**:
```python
# Check for services without team assignment
search_datadog_services(query="name:*")
# Then filter for services missing team metadata

# Validate critical services have SLOs
# (Would combine with SLO query - not shown, custom implementation)
```

**Service Maturity Scorecard**:
```
For each service, check:
- ✅ Has team ownership
- ✅ Has APM instrumentation
- ✅ Has defined SLO
- ✅ Has dashboard
- ✅ Has monitors
- ✅ Appears in service catalog

Score = (Checks Passed / Total Checks) * 100
```

---

### Pattern: APM Coverage Analysis

**Purpose**: Validate APM instrumentation across services
**Maturity Levels**: 2, 3, 4
**Use Cases**: APM adoption tracking, trace coverage

```python
# Pattern: APM service coverage
search_datadog_services(
    context="Analyzing APM instrumentation coverage",
    query="*",
    detailed_output=False
)

# Pattern: Recent trace activity
search_datadog_spans(
    context="Validating active tracing",
    query="*",
    from="now-1h",
    to="now",
    max_tokens=20000
)
```

**Coverage Calculation**:
```
APM Coverage % = (Services with Traces / Total Services) * 100

Level 2 Target: ≥70%
Level 3 Target: ≥85%
Level 4 Target: ≥95%
```

**Service-Level Trace Analysis**:
```python
# Pattern: Trace volume by service
search_datadog_spans(
    query="service:api-gateway",
    from="now-24h",
    max_tokens=10000
)

# Pattern: Error rate in traces
search_datadog_spans(
    query="status:error",
    from="now-24h"
)
```

---

## Log Management Patterns

### Pattern: Log Pipeline Efficiency

**Purpose**: Analyze log ingestion and exclusion ratios
**Maturity Levels**: 2, 3
**Use Cases**: Cost optimization, pipeline validation

```python
# Pattern: Log ingestion analysis
search_datadog_logs(
    context="Analyzing log sources and volume",
    query="*",
    from="now-24h",
    to="now",
    indexes=["*"],
    max_tokens=20000
)

# Pattern: Log pattern clustering
analyze_datadog_logs(
    context="Identifying common log patterns for exclusion",
    filter="*",
    from="now-24h",
    max_tokens=15000
)
```

**Exclusion Ratio Target**:
```
Healthy Exclusion Ratio: 60-80%
(Logs ingested but not indexed / Total logs ingested)

Under 60%: May be over-indexing (cost concern)
Over 80%: May be under-indexing (observability concern)
```

**Pattern Detection for Optimization**:
```python
# Pattern: Debug logs that could be excluded
search_datadog_logs(
    query="status:debug",
    from="now-24h"
)

# Pattern: High-volume low-value logs
analyze_datadog_logs(
    filter="status:info",
    from="now-24h",
    max_tokens=10000
)
# Look for repetitive patterns to exclude
```

---

## Monitor Assessment Patterns

### Pattern: Monitor Coverage and Quality

**Purpose**: Validate alerting coverage and reduce alert fatigue
**Maturity Levels**: 1, 2, 3
**Use Cases**: Monitor audit, alert fatigue analysis

```python
# Pattern: Active monitor inventory
search_datadog_monitors(
    context="Auditing monitor configuration",
    query="*",
    max_tokens=30000
)

# Pattern: Alerting monitors
search_datadog_monitors(
    query="status:alert OR status:warn"
)

# Pattern: Flapping monitors (alert fatigue)
# Note: Would need historical data analysis
search_datadog_monitors(
    query="status:alert"
)
# Then analyze frequency over time
```

**Monitor Quality Metrics**:
```
Essential Monitors (Level 1):
- Service availability checks
- Critical error rate alerts
- Infrastructure resource alerts

Quality Indicators:
- Has priority tag (P1-P5)
- Has team tag for routing
- Has runbook link
- Not flapping (< 15 alerts/week)
```

**Priority-Based Analysis**:
```python
# Pattern: Critical monitor coverage
search_datadog_monitors(query="priority:p1")
search_datadog_monitors(query="priority:p2")

# Pattern: Team-based monitor distribution
search_datadog_monitors(query="team:sre")
search_datadog_monitors(query="team:platform")
```

---

## Cost Optimization Patterns

### Pattern: Cloud Cost Analysis

**Purpose**: Track and optimize cloud spending
**Maturity Levels**: 3, 4, 5
**Use Cases**: Cost attribution, optimization opportunities

```python
# Pattern: Total cloud cost overview
get_datadog_metric(
    context="Analyzing total cloud spend",
    queries=["sum:all.cost{*}.rollup(sum, monthly)"],
    use_cloud_cost=True,
    from="now-90d",
    to="now"
)

# Pattern: Cost by service
get_datadog_metric(
    context="Breaking down cost by service",
    queries=["sum:all.cost{*} by {service}.rollup(sum, daily)"],
    use_cloud_cost=True,
    from="now-30d"
)

# Pattern: Cost by team
get_datadog_metric(
    queries=["sum:all.cost{*} by {team}.rollup(sum, daily)"],
    use_cloud_cost=True,
    from="now-30d"
)
```

**Cost Optimization Opportunities**:
```python
# Pattern: Unused service detection
get_datadog_metric(
    context="Finding low-traffic services for decommissioning",
    queries=["sum:trace.requests{*} by {service}"],
    from="now-30d"
)
# Services with < 100 requests/day are candidates

# Pattern: Log cost optimization
get_datadog_metric(
    queries=["sum:datadog.estimated_usage.logs.ingested_events{*} by {service}"],
    from="now-30d"
)
# Identify high-volume, low-value log sources
```

---

## Dashboard Assessment Patterns

### Pattern: Dashboard Maturity Analysis

**Purpose**: Evaluate dashboard quality and coverage
**Maturity Levels**: 2, 3, 4
**Use Cases**: Dashboard standardization, best practices audit

```python
# Pattern: Dashboard inventory
search_datadog_dashboards(
    context="Analyzing dashboard coverage",
    query="*",
    include_template_variables=True,
    max_tokens=30000
)

# Pattern: Shared team dashboards
search_datadog_dashboards(
    query="is_shared:true AND team:*"
)

# Pattern: Service-specific dashboards
search_datadog_dashboards(
    query="title:*service* OR title:*API*"
)
```

**Dashboard Quality Checklist**:
```
High-Quality Dashboard:
- ✅ Uses template variables for filtering
- ✅ Contains SLO widgets
- ✅ Has descriptive title and tags
- ✅ Shared with appropriate team
- ✅ Includes context links
- ✅ Updated recently (< 90 days)
```

---

## Incident Management Patterns

### Pattern: Incident Analysis

**Purpose**: Track incident trends and MTTR
**Maturity Levels**: 3, 4, 5
**Use Cases**: Incident retrospective, MTTR tracking

```python
# Pattern: Active incidents
search_datadog_incidents(
    context="Analyzing current incidents",
    query="state:active",
    from="now-7d"
)

# Pattern: Incident severity distribution
search_datadog_incidents(
    query="severity:(SEV-1 OR SEV-2)",
    from="now-30d"
)

# Pattern: Team-specific incidents
search_datadog_incidents(
    query="team:platform",
    from="now-30d"
)
```

**MTTR Calculation**:
```
MTTR = Sum(Resolved Time - Created Time) / Number of Incidents

Level 1 Baseline: Establish baseline
Level 2 Target: -20% from baseline
Level 3 Target: -30% from baseline
Level 4 Target: -40% from baseline
```

---

## RUM Assessment Patterns

### Pattern: Real User Monitoring Analysis

**Purpose**: Analyze user experience metrics
**Maturity Levels**: 4, 5
**Use Cases**: Performance optimization, user journey analysis

```python
# Pattern: RUM session overview
search_datadog_rum_events(
    context="Analyzing user sessions",
    query="@type:session",
    from="now-7d",
    detailed_output=True,
    max_tokens=30000
)

# Pattern: Page load performance
search_datadog_rum_events(
    query="@type:view @view.loading_time:>2000",
    from="now-24h",
    detailed_output=True
)

# Pattern: User errors
search_datadog_rum_events(
    query="@type:error",
    from="now-24h"
)
```

**Core Web Vitals Tracking**:
```
Monitor:
- LCP (Largest Contentful Paint): < 2.5s
- FID (First Input Delay): < 100ms
- CLS (Cumulative Layout Shift): < 0.1
```

---

## Synthetic Monitoring Patterns

### Pattern: Synthetic Test Coverage

**Purpose**: Validate critical user journey testing
**Maturity Levels**: 3, 4
**Use Cases**: Uptime monitoring, journey validation

```python
# Pattern: Synthetic test results
# Note: Specific API may vary, this is conceptual
# Would use appropriate Datadog MCP tool when available
```

**Critical Path Coverage**:
```
Essential Synthetic Tests:
- Homepage load
- User login
- Core transaction (purchase, signup, etc.)
- API health checks
- Multi-step user journeys
```

---

## Notebook Assessment Patterns

### Pattern: Investigation Documentation

**Purpose**: Track observability investigations and learnings
**Maturity Levels**: 3, 4, 5
**Use Cases**: Knowledge management, post-mortem tracking

```python
# Pattern: Notebook inventory
search_datadog_notebooks(
    context="Analyzing investigation documentation",
    query="*",
    max_tokens=20000
)

# Pattern: Incident-related notebooks
search_datadog_notebooks(
    query="incident OR post-mortem OR outage"
)

# Pattern: Team notebooks
search_datadog_notebooks(
    query="*",
    filter="author.name:*"
)
```

---

## Composite Assessment Patterns

### Pattern: Complete Maturity Assessment

**Purpose**: Execute comprehensive maturity check
**Maturity Levels**: All
**Use Cases**: Quarterly assessments, leadership reporting

```python
# Pattern: Multi-dimensional maturity assessment
# Execute sequence of queries for complete picture

# 1. Infrastructure
search_datadog_hosts(context="Infrastructure inventory", filter="*")

# 2. Services
search_datadog_services(context="Service catalog", query="*")

# 3. APM
search_datadog_spans(context="APM coverage", query="*", from="now-1h")

# 4. Logs
analyze_datadog_logs(context="Log efficiency", filter="*", from="now-24h")

# 5. Monitors
search_datadog_monitors(context="Alerting coverage", query="*")

# 6. Incidents
search_datadog_incidents(context="Incident trends", query="*", from="now-30d")

# 7. Costs
get_datadog_metric(
    context="Cost analysis",
    queries=["sum:all.cost{*}.rollup(sum, monthly)"],
    use_cloud_cost=True
)
```

**Consolidated Scoring**:
```
Maturity Score = Weighted Average of:
- Agent Coverage (15%)
- Tagging Compliance (15%)
- SLO Coverage (15%)
- APM Adoption (10%)
- Monitor Quality (10%)
- Log Optimization (10%)
- Cost Efficiency (10%)
- Automation Level (15%)
```

---

## Query Optimization Best Practices

### Performance Tips
1. **Use specific filters** instead of wildcards when possible
2. **Limit timeframes** to necessary range (default: 1h-7d)
3. **Use pagination** with `start_at` for large result sets
4. **Set appropriate max_tokens** based on use case
5. **Leverage indexes parameter** for log queries

### Error Handling
```python
# Pattern: Graceful degradation
try:
    result = search_datadog_[resource](...)
    if result.is_truncated:
        # Add pagination or refine filters
except Exception as e:
    # Fall back to broader query or manual check
```

### Caching Strategy
- Cache infrastructure inventory (updates: hourly)
- Cache service catalog (updates: daily)
- Real-time queries for incidents, logs, spans
- Cost data can be cached (updates: daily)

---

## Reference Implementation

See `assessment-tools/mcp-query-library/` for working examples of all patterns organized by resource type.

---

**Note**: This document will evolve as new Datadog MCP capabilities are added. Check Datadog MCP documentation for latest API features.
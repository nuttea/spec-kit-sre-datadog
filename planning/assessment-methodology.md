# SRE Maturity Assessment Methodology

This document defines the comprehensive assessment process for determining an organization's current SRE maturity level using Datadog MCP.

## Assessment Overview

The SRE Maturity Assessment is a **structured, data-driven process** that combines:
1. **Automated MCP Queries** - Objective metrics from Datadog
2. **Capability Checklists** - Process and practice validation
3. **Team Interviews** - Qualitative cultural assessment
4. **Documentation Review** - Knowledge management maturity

**Assessment Duration**: 2-4 hours per organization
**Frequency**: Quarterly for continuous improvement tracking
**Output**: Maturity scorecard with actionable recommendations

---

## Assessment Phases

### Phase 1: Preparation (15 minutes)

#### Pre-Assessment Checklist
- [ ] Datadog MCP Server installed and configured
- [ ] API/App keys with appropriate permissions
- [ ] Atlassian MCP configured (for reference documentation)
- [ ] Assessment template prepared
- [ ] Stakeholders identified and available

#### Required Datadog Permissions
```
Minimum API Key Permissions:
- Read access to: metrics, logs, traces, monitors, dashboards, services
- Read access to: incidents, notebooks, synthetic tests
- Read access to: cloud cost management (if applicable)

API Key Scopes:
- metrics_read
- logs_read
- apm_read
- monitors_read
- dashboards_read
- incidents_read
```

#### Stakeholder Identification
- **Platform/SRE Lead**: Overall observability strategy
- **Engineering Manager**: Team practices and ownership
- **DevOps Engineer**: Implementation details
- **Finance/FinOps (Optional)**: Cost optimization perspective

---

### Phase 2: Automated Assessment (45-60 minutes)

Execute structured MCP queries across all assessment dimensions.

#### Dimension 1: Infrastructure Coverage

**Objective**: Measure agent deployment and infrastructure visibility

```python
# Query 1: Total infrastructure inventory
hosts_result = search_datadog_hosts(
    context="Assessing infrastructure coverage",
    filter="*",
    include_all_tags=True,
    max_tokens=30000
)

# Query 2: Agent deployment metrics
agent_metrics = get_datadog_metric(
    context="Calculating agent deployment rate",
    queries=[
        "count:datadog.agent.running{*}",
        "count:datadog.agent.running{*} by {env}"
    ],
    from="now-1h",
    to="now"
)

# Query 3: Cloud integration status
# For AWS
aws_instances = get_datadog_metric(
    queries=["count:aws.ec2.host_ok{*}"],
    from="now-1h"
)
```

**Scoring Rubric**:
- Level 0: 0-20% coverage
- Level 1: 20-80% coverage
- Level 2: 80-95% coverage
- Level 3: 95-98% coverage
- Level 4+: 98%+ coverage

**Red Flags**:
- ❌ No agents in production environment
- ❌ Agent version fragmentation (>3 versions active)
- ❌ Critical services without agent coverage

---

#### Dimension 2: Tagging Compliance

**Objective**: Measure standardization and metadata quality

```python
# Query 1: Tag coverage analysis
hosts_with_tags = search_datadog_hosts(
    context="Auditing tagging compliance",
    filter="*",
    include_all_tags=True
)

# Query 2: Service-level tagging
services_with_tags = search_datadog_services(
    context="Analyzing service tagging",
    query="*",
    detailed_output=True
)

# Manual Analysis Required:
# Count hosts/services with:
# - env tag (required)
# - service tag (required for Level 2+)
# - version tag (required for Level 2+)
# - team tag (required for Level 3+)
```

**Scoring Rubric**:
- Level 0: No tagging strategy
- Level 1: 20-40% with env tag
- Level 2: 95%+ with env/service/version
- Level 3: 98%+ with env/service/version/team
- Level 4+: 99%+ compliance + custom tag enforcement

**Red Flags**:
- ❌ Inconsistent tag formats (camelCase, UPPERCASE, etc.)
- ❌ Tags from unbounded sources (timestamps, IDs)
- ❌ Critical services untagged

---

#### Dimension 3: Service Catalog Maturity

**Objective**: Measure service inventory and ownership clarity

```python
# Query 1: Complete service catalog
services = search_datadog_services(
    context="Analyzing service catalog completeness",
    query="*",
    detailed_output=True,
    max_tokens=30000
)

# Query 2: APM service coverage
apm_traces = search_datadog_spans(
    context="Validating APM instrumentation",
    query="*",
    from="now-1h",
    max_tokens=20000
)

# Manual Analysis:
# For each service, check:
# - Has team ownership defined
# - Has documentation links
# - Has APM traces
# - Has defined SLO (would need custom query)
```

**Scoring Rubric**:
- Level 0: No service catalog
- Level 1: Services listed, no ownership
- Level 2: 80%+ services with ownership and APM
- Level 3: 90%+ services with SLOs and documentation
- Level 4+: 95%+ services with complete metadata

**Red Flags**:
- ❌ Services with no recent activity (potential zombies)
- ❌ Critical services without ownership
- ❌ Services not in catalog but generating telemetry

---

#### Dimension 4: Monitoring & Alerting Quality

**Objective**: Measure alerting coverage and quality

```python
# Query 1: Monitor inventory
monitors = search_datadog_monitors(
    context="Auditing monitor configuration",
    query="*",
    max_tokens=30000
)

# Query 2: Currently alerting monitors
active_alerts = search_datadog_monitors(
    context="Analyzing active alerts",
    query="status:alert OR status:warn"
)

# Query 3: Monitor distribution by priority
critical_monitors = search_datadog_monitors(
    query="priority:p1 OR priority:p2"
)

# Manual Analysis:
# Calculate:
# - Monitors per service
# - Alert fatigue indicators (>15 alerts/week)
# - Priority tag coverage
# - Team routing coverage
```

**Scoring Rubric**:
- Level 0: No monitors configured
- Level 1: 5-10 basic monitors
- Level 2: Comprehensive monitors with priority tags
- Level 3: Monitors with SLO integration and routing
- Level 4+: Anomaly detection and predictive alerting

**Red Flags**:
- ❌ Monitors without team tags (no routing)
- ❌ Monitors without priority tags
- ❌ High alert frequency (>15/week = alert fatigue)
- ❌ No monitors for critical services

---

#### Dimension 5: Log Management Efficiency

**Objective**: Measure log strategy and cost optimization

```python
# Query 1: Log source inventory
log_sources = search_datadog_logs(
    context="Analyzing log sources",
    query="*",
    from="now-24h",
    indexes=["*"],
    max_tokens=20000
)

# Query 2: Log pattern analysis
log_patterns = analyze_datadog_logs(
    context="Identifying optimization opportunities",
    filter="*",
    from="now-24h",
    max_tokens=15000
)

# Query 3: Log volume metrics
log_volume = get_datadog_metric(
    context="Measuring log ingestion",
    queries=["sum:datadog.estimated_usage.logs.ingested_events{*}"],
    from="now-7d"
)

# Manual Analysis:
# Calculate:
# - Exclusion ratio (ingested vs indexed)
# - Pipeline coverage (% of logs parsed)
# - Cost per log source
```

**Scoring Rubric**:
- Level 0: No log collection
- Level 1: Basic log collection, no pipelines
- Level 2: Pipelines configured, 60%+ exclusion ratio
- Level 3: Optimized indexing, custom indexes by env/type
- Level 4+: Flex logs, intelligent sampling, <30% waste

**Red Flags**:
- ❌ Exclusion ratio <40% (over-indexing, high cost)
- ❌ No log pipelines (unstructured logs)
- ❌ Debug/verbose logs in production indexes

---

#### Dimension 6: Cost Optimization Maturity

**Objective**: Measure cost awareness and optimization practices

```python
# Query 1: Total cloud cost
total_cost = get_datadog_metric(
    context="Analyzing total cloud spend",
    queries=["sum:all.cost{*}.rollup(sum, monthly)"],
    use_cloud_cost=True,
    from="now-90d",
    to="now"
)

# Query 2: Cost by service
cost_by_service = get_datadog_metric(
    context="Breaking down cost by service",
    queries=["sum:all.cost{*} by {service}.rollup(sum, daily)"],
    use_cloud_cost=True,
    from="now-30d"
)

# Query 3: Cost by team
cost_by_team = get_datadog_metric(
    context="Cost attribution by team",
    queries=["sum:all.cost{*} by {team}.rollup(sum, daily)"],
    use_cloud_cost=True,
    from="now-30d"
)

# Manual Analysis:
# Calculate:
# - Observability cost as % of infrastructure
# - Cost per service/team
# - Optimization opportunities (idle resources)
```

**Scoring Rubric**:
- Level 0: No cost tracking
- Level 1: Basic cost awareness, no attribution
- Level 2: Cost per service tracked
- Level 3: Cost optimization active, 20%+ savings
- Level 4+: Predictive cost modeling, automated optimization

**Red Flags**:
- ❌ No cost attribution tags
- ❌ Uncontrolled cost growth >20% MoM
- ❌ No idle resource detection

---

#### Dimension 7: Incident Management Maturity

**Objective**: Measure incident response effectiveness

```python
# Query 1: Recent incidents
incidents = search_datadog_incidents(
    context="Analyzing incident trends",
    query="*",
    from="now-30d",
    max_tokens=20000
)

# Query 2: Active incidents
active_incidents = search_datadog_incidents(
    context="Current active incidents",
    query="state:active",
    from="now-7d"
)

# Query 3: Severity distribution
critical_incidents = search_datadog_incidents(
    query="severity:(SEV-1 OR SEV-2)",
    from="now-90d"
)

# Manual Analysis:
# Calculate:
# - MTTR (Mean Time To Resolution)
# - Incident frequency
# - Repeat incidents (same service)
# - Post-mortem completion rate
```

**Scoring Rubric**:
- Level 0: No incident tracking
- Level 1: Manual incident logging
- Level 2: Incident tracking in Datadog, MTTR measured
- Level 3: Automated incident creation, <30min MTTR
- Level 4+: Predictive incident prevention, <10min MTTR

**Red Flags**:
- ❌ No incident tracking
- ❌ MTTR increasing over time
- ❌ Repeat incidents without remediation

---

#### Dimension 8: Advanced Capabilities

**Objective**: Measure adoption of advanced Datadog features

```python
# Query 1: APM coverage
apm_services = search_datadog_services(
    context="APM instrumentation coverage",
    query="*"
)

# Query 2: RUM implementation (if applicable)
rum_data = search_datadog_rum_events(
    context="Real user monitoring coverage",
    query="@type:session",
    from="now-7d",
    detailed_output=False
)

# Query 3: Synthetic monitoring
# (Would use synthetic test API when available)

# Query 4: Dashboard maturity
dashboards = search_datadog_dashboards(
    context="Dashboard quality assessment",
    query="*",
    include_template_variables=True
)

# Manual Analysis:
# Check for:
# - Workflow automation
# - Fleet automation
# - Synthetic tests on critical paths
# - RUM user journey tracking
```

**Scoring Rubric**:
- Level 0-1: Basic monitoring only
- Level 2: APM deployed
- Level 3: APM + Synthetics + advanced dashboards
- Level 4: APM + RUM + Synthetics + Workflows
- Level 5: Full platform with ML insights

---

### Phase 3: Qualitative Assessment (30-45 minutes)

#### Team Interview Questions

**Ownership & Culture**
- Who owns observability in your organization?
- Do service teams own their monitoring, or is it centralized?
- How are observability improvements prioritized?

**Process Maturity**
- How are new services onboarded to Datadog?
- What's the process for creating monitors and dashboards?
- How are alerts routed to the right teams?

**Documentation & Knowledge**
- Where is observability documentation maintained?
- Are runbooks linked from monitors?
- How are incidents documented and learned from?

**Cost Awareness**
- Who reviews observability costs?
- Are costs attributed to teams/services?
- What cost optimization practices exist?

**Automation**
- What's automated (agent deployment, monitor creation, etc.)?
- Are observability configs in version control?
- Is observability part of CI/CD pipelines?

#### Capability Checklist

Use this checklist during interviews:

**Level 1 Capabilities**
- [ ] Agent deployment process documented
- [ ] Basic monitors configured
- [ ] On-call rotation established
- [ ] Incident response process exists

**Level 2 Capabilities**
- [ ] Tagging standard documented and enforced
- [ ] SLOs defined for critical services
- [ ] APM instrumented for key applications
- [ ] Service catalog maintained
- [ ] Team-based access control configured

**Level 3 Capabilities**
- [ ] Cost tracking by service/team
- [ ] Production readiness checklist
- [ ] Automated compliance checks
- [ ] Fleet automation active
- [ ] Self-service documentation available

**Level 4 Capabilities**
- [ ] Workflow automation for common incidents
- [ ] RUM tracking user journeys
- [ ] Synthetic tests on critical paths
- [ ] Platform engineering team exists
- [ ] Observability in CI/CD pipelines

**Level 5 Capabilities**
- [ ] ML insights driving decisions
- [ ] Observability as product mindset
- [ ] Contributing to Datadog community
- [ ] Public thought leadership
- [ ] Industry recognition

---

### Phase 4: Documentation Review (15-30 minutes)

Review existing documentation for completeness:

#### Essential Documentation
- [ ] Observability strategy document
- [ ] Tagging standards
- [ ] Agent deployment guide
- [ ] Monitor creation guide
- [ ] Dashboard design standards
- [ ] Incident response runbooks
- [ ] Cost optimization playbook

#### Documentation Quality Indicators
- ✅ Updated within last 6 months
- ✅ Version controlled (Git)
- ✅ Searchable and accessible
- ✅ Examples and templates included
- ✅ Linked from relevant tools

---

### Phase 5: Scoring & Report Generation (30 minutes)

#### Maturity Scorecard Calculation

**Weighted Scoring Formula**:
```
Total Maturity Score = Σ (Dimension Score × Weight)

Dimension Weights:
- Infrastructure Coverage: 15%
- Tagging Compliance: 15%
- Service Catalog: 10%
- Monitoring Quality: 15%
- Log Management: 10%
- Cost Optimization: 10%
- Incident Management: 15%
- Advanced Capabilities: 10%
```

**Score to Level Mapping**:
- 0-20%: Level 0 (Foundation)
- 21-40%: Level 1 (Reactive)
- 41-60%: Level 2 (Proactive)
- 61-75%: Level 3 (Managed)
- 76-90%: Level 4 (Optimized)
- 91-100%: Level 5 (Excellence)

#### Report Structure

```markdown
# SRE Maturity Assessment Report

**Organization**: [Name]
**Assessment Date**: [Date]
**Assessor**: [Name]
**Overall Maturity Level**: Level [N]
**Overall Score**: [X]/100

---

## Executive Summary

[2-3 paragraph summary of current state and key findings]

---

## Dimension Scores

| Dimension | Score | Target | Status |
|-----------|-------|--------|--------|
| Infrastructure Coverage | X/100 | Y | ✅/⚠️/❌ |
| Tagging Compliance | X/100 | Y | ✅/⚠️/❌ |
| Service Catalog | X/100 | Y | ✅/⚠️/❌ |
| Monitoring Quality | X/100 | Y | ✅/⚠️/❌ |
| Log Management | X/100 | Y | ✅/⚠️/❌ |
| Cost Optimization | X/100 | Y | ✅/⚠️/❌ |
| Incident Management | X/100 | Y | ✅/⚠️/❌ |
| Advanced Capabilities | X/100 | Y | ✅/⚠️/❌ |

---

## Strengths

1. [Capability where you excel]
2. [Capability where you excel]
3. [Capability where you excel]

---

## Gaps & Recommendations

### High Priority
1. **[Gap]**
   - Current State: [Description]
   - Target State: [Description]
   - Impact: [Business/operational impact]
   - Effort: [Low/Medium/High]
   - Timeline: [Recommended timeframe]

### Medium Priority
[Same structure]

### Low Priority
[Same structure]

---

## Roadmap to Next Level

### Current Level: Level [N]
### Target Level: Level [N+1]

**Required Capabilities**:
- [ ] [Capability 1] - [Status]
- [ ] [Capability 2] - [Status]
- [ ] [Capability 3] - [Status]

**Estimated Timeline**: [X weeks/months]
**Key Milestones**:
1. [Milestone 1] - [Date]
2. [Milestone 2] - [Date]
3. [Milestone 3] - [Date]

---

## Cost-Benefit Analysis

**Current State**:
- Monthly observability spend: $[X]
- Cost per service: $[Y]
- Observability as % of infra: [Z]%

**Projected Improvements** (Level [N+1]):
- Cost reduction: -[X]%
- MTTR reduction: -[X]%
- Service coverage: +[X]%

---

## Appendix: Raw Data

[Include relevant MCP query results, charts, and supporting data]
```

---

## Assessment Best Practices

### Do's
- ✅ Run assessment during business hours (need team input)
- ✅ Combine automated queries with human insight
- ✅ Focus on gaps, not just scores
- ✅ Provide actionable recommendations
- ✅ Link to specific implementation guides
- ✅ Celebrate strengths, not just weaknesses

### Don'ts
- ❌ Rely solely on automated scoring
- ❌ Compare organizations without context
- ❌ Skip qualitative interviews
- ❌ Ignore organizational culture
- ❌ Provide recommendations without effort estimates

---

## Continuous Improvement

**Recommended Assessment Frequency**:
- **Initial Assessment**: Comprehensive (full 4 hours)
- **Quarterly Check-ins**: Abbreviated (1-2 hours, focus on key metrics)
- **Annual Review**: Comprehensive reassessment

**Tracking Progress**:
- Maintain assessment history in version control
- Track dimension scores over time
- Measure actual vs. projected improvements
- Celebrate level graduations with team

---

## Automation Opportunities

Future enhancements to automate:
1. **Automated Scoring Dashboard**: Real-time maturity score in Datadog
2. **Continuous Compliance Checks**: Daily MCP queries validating standards
3. **Regression Alerts**: Alert when maturity scores decrease
4. **Self-Service Assessment**: Teams run their own assessments
5. **Benchmark Comparisons**: Compare against industry standards

---

## Tools & Templates

Available in `assessment-tools/` directory:
- `maturity-scorecard.md` - Interactive scorecard template
- `gap-analysis-generator.md` - Automated gap analysis
- `assessment-report-template.md` - Report generation template
- `mcp-query-library/` - Pre-built MCP queries for each dimension

---

**Note**: This methodology will evolve based on assessment experience and Datadog MCP capabilities. Contribute improvements back to the spec kit repository.
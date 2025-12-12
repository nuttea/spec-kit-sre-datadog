# Notebook Templates Specification

Complete specification for starter notebook templates in the SRE Spec Kit.

## Template Structure Standard

All templates follow this structure:

```markdown
---
title: [Template Name]
type: [assessment|investigation|postmortem|runbook|report]
version: 1.0
created: [YYYY-MM-DD]
tags: [tag1, tag2, tag3]
---

# [Template Title]

**Metadata**
- Date: YYYY-MM-DD
- Owner: [Name/Team]
- Status: [Draft|In Progress|Complete]
- Priority: [P0-P4]
- Related Services: [service1, service2]

## Objective
[Clear statement of what this notebook aims to achieve]

## Success Criteria
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Data Collection

### Required Queries
[Pre-filled Datadog MCP queries]

### Time Range
- Start: [ISO 8601 or relative time]
- End: [ISO 8601 or relative time]

## Analysis
[Structured analysis sections]

## Findings
[Key discoveries and insights]

## Action Items
- [ ] Task 1 (Owner: XX, Due: YYYY-MM-DD)
- [ ] Task 2 (Owner: XX, Due: YYYY-MM-DD)

## References
- [Dashboard links]
- [Monitor links]
- [Related notebooks]
```

---

## Assessment Templates

### 1. Weekly Assessment Template
**File**: `notebooks/assessments/weekly-assessment-template.md`

**Purpose**: Quick weekly checkpoint for tracking maturity progress

**Sections**:
- Week number and date range
- Quick scores (8 dimensions, 0-100)
- Week-over-week changes
- Top 3 accomplishments
- Top 3 blockers
- Action items for next week
- **Pre-filled queries**:
  - Host count: `search_datadog_hosts`
  - Service count: `search_datadog_services`
  - Monitor status: `search_datadog_monitors`
  - Incident count: `search_datadog_incidents`

### 2. Quarterly Review Template
**File**: `notebooks/assessments/quarterly-review-template.md`

**Purpose**: Comprehensive quarterly business review format

**Sections**:
- Executive summary (1 page)
- Quarter scorecard (all 8 dimensions)
- Trend analysis (vs previous quarters)
- ROI calculations
- Team highlights
- Infrastructure changes
- Cost analysis
- Next quarter roadmap
- **Pre-filled queries**:
  - 90-day infrastructure trends
  - Cost metrics by service/team
  - Incident MTTR trends
  - Agent coverage trends

### 3. Level Readiness Template
**File**: `notebooks/assessments/level-readiness-template.md`

**Purpose**: Validate readiness to advance to next maturity level

**Sections**:
- Current level assessment
- Target level requirements
- Gap checklist
- Validation queries for each capability
- Graduation criteria pass/fail
- Remediation plan for gaps
- **Pre-filled queries**: Level-specific validation queries

---

## Investigation Templates

### 4. Performance Investigation Template
**File**: `notebooks/investigations/performance-investigation-template.md`

**Purpose**: Systematic performance degradation analysis

**Sections**:
- Symptom description
- Affected services and endpoints
- Time window of degradation
- Baseline vs current metrics
- Trace analysis (p50/p95/p99 latency)
- Database query performance
- External dependency check
- Resource utilization (CPU, memory, network)
- Root cause hypothesis
- Validation steps
- Resolution plan
- **Pre-filled queries**:
  ```
  search_datadog_spans(
    query="service:YOUR_SERVICE status:ok",
    from="now-24h"
  )
  get_datadog_metric(
    queries=["avg:trace.express.request{service:YOUR_SERVICE}"]
  )
  ```

### 5. Error Spike Investigation Template
**File**: `notebooks/investigations/error-spike-investigation-template.md`

**Purpose**: Root cause analysis for error rate increases

**Sections**:
- Error spike timeline
- Error types and counts
- Affected services/endpoints
- Error message patterns
- Recent deployments/changes
- Log analysis (error sampling)
- Trace correlation
- External factors (dependencies, traffic)
- Root cause determination
- Mitigation steps
- **Pre-filled queries**:
  ```
  analyze_datadog_logs(
    filter="status:error service:YOUR_SERVICE",
    sql_query="SELECT status, count(*) FROM logs GROUP BY status"
  )
  search_datadog_spans(
    query="service:YOUR_SERVICE status:error"
  )
  ```

### 6. Cost Investigation Template
**File**: `notebooks/investigations/cost-investigation-template.md`

**Purpose**: Identify and analyze cost anomalies

**Sections**:
- Cost spike timeline
- Cost breakdown (service/team/environment)
- Usage patterns analysis
- Top cost drivers
- Comparison to baseline
- Idle/unused resource identification
- Optimization opportunities
- Cost reduction roadmap
- **Pre-filled queries**:
  ```
  get_datadog_metric(
    queries=["sum:all.cost{*}.rollup(sum, daily)"],
    use_cloud_cost=true
  )
  search_datadog_services(
    query="*",
    detailed_output=true
  )
  ```

---

## Postmortem Templates

### 7. Incident Postmortem Template
**File**: `notebooks/postmortems/incident-postmortem-template.md`

**Purpose**: Structured incident analysis and learning

**Sections**:
- Incident metadata (ID, severity, duration, impact)
- Executive summary
- Timeline of events (detection → resolution)
- Root cause analysis (5 Whys)
- Contributing factors
- What went well
- What went wrong
- Action items (with owners and deadlines)
- Follow-up items
- **Pre-filled queries**:
  ```
  get_datadog_incident(
    incident_id="INCIDENT_ID"
  )
  search_datadog_logs(
    query="service:YOUR_SERVICE status:error",
    from="INCIDENT_START",
    to="INCIDENT_END"
  )
  ```

### 8. Outage Analysis Template
**File**: `notebooks/postmortems/outage-analysis-template.md`

**Purpose**: Complete outage impact assessment

**Sections**:
- Outage summary
- Customer impact metrics
- Service degradation timeline
- Detection and escalation
- Response timeline
- Mitigation actions
- Root cause deep dive
- Prevention measures
- Communication retrospective
- Lessons learned
- **Pre-filled queries**: Full service health queries

---

## Runbook Templates

### 9. Service Onboarding Runbook
**File**: `notebooks/runbooks/service-onboarding-runbook.md`

**Purpose**: Checklist for monitoring new services

**Sections**:
- Service overview
- Agent installation checklist
- Tagging implementation (UST)
- APM instrumentation
- Log collection setup
- Monitor creation (Golden Signals)
- Dashboard creation
- Alert routing configuration
- Team assignment
- Validation queries
- **Pre-filled queries**: Service discovery and validation

### 10. Alert Response Runbook
**File**: `notebooks/runbooks/alert-response-runbook.md`

**Purpose**: Standard operating procedures for alerts

**Sections**:
- Alert triage decision tree
- Common alert types and responses
- Escalation paths
- Investigation workflows
- Mitigation playbooks
- Communication templates
- Resolution verification
- Documentation requirements
- **Pre-filled queries**: Alert investigation queries

### 11. Cost Optimization Runbook
**File**: `notebooks/runbooks/cost-optimization-runbook.md`

**Purpose**: Step-by-step cost reduction implementation

**Sections**:
- Cost baseline establishment
- Optimization opportunities identification
- Implementation priorities
- Service decommission checklist
- Log optimization steps
- Metric cardinality reduction
- Retention policy review
- Validation and monitoring
- **Pre-filled queries**: Cost analysis queries

---

## Report Templates

### 12. Executive Report Template
**File**: `notebooks/reports/executive-report-template.md`

**Purpose**: Business-focused leadership reporting

**Sections**:
- Executive summary (1 page)
- Maturity scorecard
- Business impact metrics
- Cost efficiency trends
- Key achievements
- Risk factors
- Investment recommendations
- Next quarter priorities
- **Pre-filled queries**: High-level aggregate metrics

### 13. Monthly Metrics Report
**File**: `notebooks/reports/monthly-metrics-report.md`

**Purpose**: KPI tracking and trend analysis

**Sections**:
- Month overview
- Infrastructure metrics
- Application performance (SLOs)
- Incident metrics (MTTD, MTTR)
- Cost metrics
- Tagging compliance
- Month-over-month comparisons
- Trend analysis
- **Pre-filled queries**: 30-day metrics

### 14. Team Health Report
**File**: `notebooks/reports/team-health-report.md`

**Purpose**: Team maturity and performance tracking

**Sections**:
- Team overview
- Maturity level assessment
- Service portfolio health
- On-call metrics
- Incident participation
- Knowledge sharing metrics
- Technical debt tracking
- Training and development
- **Pre-filled queries**: Team-specific metrics

---

## Template Variables

Each template uses standardized variables for easy customization:

```markdown
<!-- Replace these variables when using template -->
- {{DATE}}: Current date in YYYY-MM-DD format
- {{OWNER}}: Person or team name
- {{SERVICE}}: Service name for queries
- {{TEAM}}: Team name for filtering
- {{ENV}}: Environment (dev, staging, prod)
- {{START_TIME}}: Investigation start time
- {{END_TIME}}: Investigation end time
- {{INCIDENT_ID}}: Datadog incident ID
- {{NOTEBOOK_URL}}: Link to Datadog Notebook
```

---

## Template Best Practices

1. **Always include date and owner** - Essential for tracking
2. **Use checklists** - Makes templates actionable
3. **Pre-fill queries** - Reduces cognitive load
4. **Include examples** - Shows proper usage
5. **Link to documentation** - Provides context
6. **Version templates** - Track improvements over time
7. **Keep templates focused** - One purpose per template
8. **Make them git-friendly** - Plain markdown, no binary files

---

## Integration Points

Templates integrate with:
- **Slash commands**: `/assess`, `/level0-infra`, etc. can use templates
- **Datadog Notebooks**: Templates can be pushed via `/save-to-notebook`
- **Git workflow**: Version control for institutional knowledge
- **Team collaboration**: Shared standards and formats
- **Automation**: Templates can be programmatically generated

---

## Template Maintenance

**Monthly Review**:
- Update queries for new Datadog features
- Refine based on team feedback
- Add examples from real usage
- Remove outdated sections

**Quarterly Update**:
- Major version changes
- Align with SRE maturity model updates
- Add new template types based on needs

---

**Version**: 1.0
**Last Updated**: 2025-12-12
**Total Templates**: 14 starter templates
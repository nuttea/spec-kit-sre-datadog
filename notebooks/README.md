# SRE Starter Notebooks

Comprehensive collection of notebook templates for SRE observability workflows using Datadog.

## 📁 Directory Structure

```
notebooks/
├── assessments/          # Regular maturity assessments
├── investigations/       # Root cause analysis workflows
├── postmortems/         # Incident learning and documentation
├── runbooks/            # Standard operating procedures
└── reports/             # Business and team reporting
```

## 📊 Assessment Templates

**Purpose**: Regular checkpoint and maturity tracking

| Template | Purpose | Frequency | Duration |
|----------|---------|-----------|----------|
| [weekly-assessment-template.md](assessments/weekly-assessment-template.md) | Quick weekly checkpoint | Weekly | 15 min |
| [quarterly-review-template.md](assessments/quarterly-review-template.md) | Comprehensive business review | Quarterly | 2-3 hours |
| [level-readiness-template.md](assessments/level-readiness-template.md) | Validate level graduation | As needed | 1-2 hours |

**When to use**:
- Weekly: Track week-over-week progress
- Quarterly: Leadership reporting, trend analysis
- Level Readiness: Before advancing maturity levels

---

## 🔍 Investigation Templates

**Purpose**: Systematic troubleshooting and root cause analysis

| Template | Purpose | Use Case | Pre-filled Queries |
|----------|---------|----------|-------------------|
| [performance-investigation-template.md](investigations/performance-investigation-template.md) | Latency and throughput issues | High p95/p99, slow endpoints | Spans, traces, metrics |
| [error-spike-investigation-template.md](investigations/error-spike-investigation-template.md) | Error rate increases | Sudden error spikes, deployment issues | Logs, traces, events |
| [cost-investigation-template.md](investigations/cost-investigation-template.md) | Cost anomalies | Budget overruns, unexpected charges | Cloud cost metrics |

**When to use**:
- Performance: When latency exceeds SLO
- Error Spike: When error rate >5% or unusual patterns
- Cost: When daily cost increases >10%

---

## 📝 Postmortem Templates

**Purpose**: Blameless learning from incidents

| Template | Purpose | Severity | Depth |
|----------|---------|----------|-------|
| [incident-postmortem-template.md](postmortems/incident-postmortem-template.md) | Standard incident analysis | SEV-2 to SEV-4 | Standard |
| [outage-analysis-template.md](postmortems/outage-analysis-template.md) | Complete outage impact assessment | SEV-0 to SEV-1 | Comprehensive |

**When to use**:
- Incident Postmortem: All SEV-2+ incidents
- Outage Analysis: Complete service outages (SEV-0/SEV-1)

**Key Sections**:
- 5 Whys root cause analysis
- Blameless investigation
- Action items with owners
- Prevention measures

---

## 📖 Runbook Templates

**Purpose**: Standard operating procedures and checklists

| Template | Purpose | Use Case |
|----------|---------|----------|
| [service-onboarding-runbook.md](runbooks/service-onboarding-runbook.md) | Onboard new services | New service monitoring setup |
| [alert-response-runbook.md](runbooks/alert-response-runbook.md) | Respond to common alerts | On-call alert triage |
| [cost-optimization-runbook.md](runbooks/cost-optimization-runbook.md) | Cost reduction workflow | Monthly/quarterly cost reviews |

**When to use**:
- Service Onboarding: Every new service deployment
- Alert Response: Keep handy for on-call engineers
- Cost Optimization: Monthly or when cost spikes occur

**Features**:
- Step-by-step checklists
- Pre-filled validation queries
- Decision trees
- Troubleshooting guides

---

## 📈 Report Templates

**Purpose**: Business and team reporting

| Template | Audience | Frequency | Focus |
|----------|----------|-----------|-------|
| [executive-report-template.md](reports/executive-report-template.md) | Leadership, C-suite | Quarterly | Business impact, ROI, strategy |
| [monthly-metrics-report.md](reports/monthly-metrics-report.md) | Engineering team, management | Monthly | KPIs, trends, metrics |
| [team-health-report.md](reports/team-health-report.md) | Team lead, HR, management | Monthly/Quarterly | Team performance, morale, capacity |

**When to use**:
- Executive: Quarterly business reviews, budget planning
- Monthly Metrics: Regular team updates, trend tracking
- Team Health: Team retrospectives, capacity planning

---

## 🎯 Quick Start Guide

### 1. Choose Your Template

Navigate to the appropriate category and copy the template:
```bash
cp notebooks/investigations/performance-investigation-template.md \
   notebooks/investigations/api-latency-2025-12-12.md
```

### 2. Fill in Metadata

Update the frontmatter and metadata section:
```yaml
---
title: API Latency Investigation
date: 2025-12-12
owner: Jane Doe
status: In Progress
---
```

### 3. Run Pre-filled Queries

Execute the Datadog MCP queries embedded in the template:
```
search_datadog_spans(query="service:api-server status:error", from="now-1h")
```

### 4. Complete the Template

Work through each section systematically, filling in findings and data.

### 5. Share Results

**Option A**: Keep in git
- Commit to repository
- Share via pull request
- Version controlled

**Option B**: Push to Datadog Notebook
```
/save-to-notebook
```
- Collaborative editing
- Visual graphs
- Shareable links

---

## 🔧 Template Features

### Pre-filled Datadog MCP Queries

All templates include ready-to-run queries:
```
search_datadog_hosts(query="*")
get_datadog_metric(queries=["avg:system.cpu.user{*}"], from="now-24h")
analyze_datadog_logs(filter="status:error", sql_query="...", from="now-1h")
search_datadog_spans(query="service:api", from="now-1h")
```

### Variable Substitution

Templates use placeholders for easy customization:
- `{{DATE}}` - Current date
- `{{OWNER}}` - Your name
- `{{SERVICE}}` - Service name
- `{{TEAM}}` - Team name
- `{{ENV}}` - Environment (prod, staging, dev)

### Checklists

Every template includes actionable checklists:
- [ ] Task 1 (Owner: XX, Due: YYYY-MM-DD)
- [ ] Task 2 (Owner: XX, Due: YYYY-MM-DD)

### Decision Frameworks

Structured decision trees and analysis frameworks guide you through complex investigations.

---

## 📚 Best Practices

### 1. Customize for Your Organization

**Edit templates to match**:
- Your tagging conventions
- Your service names
- Your team structure
- Your escalation paths
- Your tooling

### 2. Version Control

**Commit templates to git**:
- Track changes over time
- Share across team
- Maintain consistency
- Review improvements

### 3. Keep Templates Updated

**Monthly maintenance**:
- Update queries for new Datadog features
- Refine based on usage
- Add examples from real investigations
- Remove outdated sections

### 4. Build a Library

**Save completed notebooks**:
- Create `completed/` subdirectories
- Use descriptive filenames: `api-latency-2025-12-12-resolved.md`
- Reference past investigations
- Learn from patterns

### 5. Integrate with Workflows

**Connect to existing processes**:
- Link from runbooks
- Reference in monitor descriptions
- Share in incident channels
- Archive in knowledge base

---

## 🔗 Integration with SRE Spec Kit

### Slash Commands

Use templates with SRE Spec Kit commands:
```bash
# Run assessment and use template
/assess

# Use investigation template after detecting issue
cp notebooks/investigations/performance-investigation-template.md investigation.md

# Save completed investigation to Datadog
/save-to-notebook
```

### Datadog Notebooks

Push completed notebooks to Datadog:
```bash
# Create notebook from template
/save-to-notebook

# Add updates to existing notebook
/append-to-notebook
```

### Assessment Flow

1. `/assess` → Use assessment template
2. Identify gaps → Use investigation template
3. Resolve issue → Use postmortem template
4. Document learnings → Update runbook template
5. Track improvements → Use report template

---

## 📖 Additional Resources

- **Planning Documents**: [../planning/](../planning/)
- **Level Definitions**: [../planning/level-definitions.md](../planning/level-definitions.md)
- **MCP Query Patterns**: [../planning/mcp-query-patterns.md](../planning/mcp-query-patterns.md)
- **Template Specification**: [../planning/notebook-templates-spec.md](../planning/notebook-templates-spec.md)
- **Commands Reference**: [../COMMANDS.md](../COMMANDS.md)

---

## 🆘 Support

### Questions?

1. **Template Usage**: See template header comments
2. **MCP Queries**: Use `/search_datadog_docs` tool
3. **Slash Commands**: Run `/help` for available commands
4. **Issues**: Check [COMMANDS.md](../COMMANDS.md)

### Contributing

**Improvements welcome**:
1. Fork repository
2. Customize template
3. Share learnings
4. Submit improvements

---

**Template Library Version**: 1.0
**Last Updated**: 2025-12-12
**Total Templates**: 14 starter templates

**Categories**:
- 3 Assessment templates
- 3 Investigation templates
- 2 Postmortem templates
- 3 Runbook templates
- 3 Report templates

---

**Generated by**: SRE Spec Kit for Datadog
**Command**: `/create-starter-notebooks`

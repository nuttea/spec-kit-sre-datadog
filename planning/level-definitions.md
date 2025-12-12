# SRE Maturity Level Definitions

This document defines detailed criteria, capabilities, and success metrics for each maturity level in the SRE Spec Kit.

## Maturity Level Framework Overview

Each level builds progressively on the previous, with no level skipping. Organizations must demonstrate capability at one level before advancing to the next.

---

## Level 0: Foundation (Planning & Discovery)

### Description
The foundation phase focuses on understanding the current state of observability, establishing baseline metrics, and planning the Datadog implementation strategy.

### Key Characteristics
- **Posture**: Discovering and documenting
- **Automation**: Minimal to none
- **Ownership**: Centralized (platform team)
- **Response**: Manual investigation
- **Documentation**: Initial scoping documents

### Core Capabilities

| Capability | Criteria | MCP Assessment |
|------------|----------|----------------|
| **Infrastructure Discovery** | Complete inventory of hosts, services, applications | Query all hosts, containers, services via MCP |
| **Current State Analysis** | Document existing monitoring tools and gaps | Analyze agent deployment coverage |
| **Cost Baseline** | Understand current observability spend | Query CCM data, estimate Datadog costs |
| **Tagging Audit** | Inventory existing tags and conventions | Analyze tag coverage across infrastructure |
| **Team Structure** | Map organizational teams to services | Document ownership and contact points |
| **Compliance Requirements** | Identify regulatory requirements (HIPAA, PCI, etc.) | Review data residency and retention needs |

### Success Criteria
- ✅ Complete infrastructure inventory documented
- ✅ Current monitoring gaps identified
- ✅ Cost baseline established
- ✅ Tagging strategy drafted
- ✅ Team ownership mapped
- ✅ Compliance requirements documented
- ✅ Datadog org created (if new)
- ✅ Initial healthcheck completed

### Key Datadog MCP Queries
```
# Infrastructure inventory
search_datadog_hosts(filter="*", include_all_tags=true)

# Service discovery
search_datadog_services(query="")

# Current agent coverage
search_datadog_metrics(query="name:datadog.agent.running")

# Cost baseline
get_datadog_metric(queries=["sum:all.cost{*}.rollup(sum, monthly)"], use_cloud_cost=true)
```

### Typical Duration
2-4 weeks for initial discovery and planning

### Graduation Criteria to Level 1
- Infrastructure inventory complete and validated
- Tagging strategy approved by leadership
- Datadog org provisioned with basic RBAC
- Agent deployment plan created
- Cost model approved

---

## Level 1: Reactive (Initial Implementation)

### Description
Basic monitoring is deployed with manual alerting and incident response. Teams react to issues as they occur.

### Key Characteristics
- **Posture**: Reactive to incidents
- **Automation**: Basic alerting only
- **Ownership**: Centralized platform team
- **Response**: Manual investigation and remediation
- **Documentation**: Runbooks in progress

### Core Capabilities

| Capability | Criteria | MCP Assessment |
|------------|----------|----------------|
| **Agent Deployment** | Agents running on ≥80% of production infrastructure | Query agent.running metrics |
| **Basic Dashboards** | System dashboards for infrastructure and services | Count dashboards with core metrics |
| **Essential Monitors** | Critical alerts for service availability | Query monitors by priority and status |
| **Log Collection** | Basic log ingestion from key services | Query log volume and sources |
| **Incident Response** | On-call rotation with manual response | Check incident count and MTTR |
| **Basic Integration** | Cloud provider integration (AWS/Azure/GCP) | Validate cloud metrics availability |

### Success Criteria
- ✅ ≥80% agent deployment coverage
- ✅ ≥5 critical monitors configured and alerting
- ✅ Core infrastructure dashboards created
- ✅ Log collection from production services
- ✅ Basic on-call rotation established
- ✅ MTTR tracked but not optimized
- ✅ Cloud integration metrics flowing

### Key Datadog MCP Queries
```
# Agent deployment coverage
search_datadog_hosts(filter="agent.running:*")
get_datadog_metric(queries=["count:system.cpu.idle{*}"])

# Monitor coverage
search_datadog_monitors(query="status:alert OR status:warn")

# Log sources
search_datadog_logs(query="*", indexes=["*"], from="now-24h")
analyze_datadog_logs(filter="*", from="now-24h")

# Incident metrics
search_datadog_incidents(query="state:active")
```

### Typical Duration
2-3 months for initial deployment

### Graduation Criteria to Level 2
- Agent coverage >80% validated via MCP
- At least 10 actionable monitors configured
- Team using dashboards daily
- Log ingestion stable
- Incidents are being tracked in Datadog

---

## Level 2: Proactive (Integration & Standardization)

### Description
Automated alerting with SLO tracking, unified tagging, and proactive issue detection. Teams anticipate issues before customer impact.

### Key Characteristics
- **Posture**: Proactive monitoring and alerting
- **Automation**: Automated alerting, basic remediation
- **Ownership**: Shared (platform + service teams)
- **Response**: Automated detection, guided remediation
- **Documentation**: Comprehensive runbooks

### Core Capabilities

| Capability | Criteria | MCP Assessment |
|------------|----------|----------------|
| **Unified Tagging** | ≥95% compliance with tagging standard (env, service, version) | Audit tags via MCP across all resources |
| **SLO Coverage** | SLOs defined for ≥80% of critical services | Query SLO configuration and status |
| **APM Integration** | APM instrumented for ≥70% of services | Query APM service coverage and trace volume |
| **Log Management** | Pipelines, indexes, and exclusion filters optimized | Analyze log pipeline efficiency |
| **Service Catalog** | All services registered with ownership | Query service catalog completeness |
| **Team-Based RBAC** | Datadog Teams mapped to org structure | Validate team membership and permissions |
| **Dashboard Maturity** | Template variables, SLO widgets, standardized layouts | Audit dashboard quality |

### Success Criteria
- ✅ ≥95% tagging compliance (env, service, version)
- ✅ SLOs tracking ≥80% of critical user journeys
- ✅ APM traces available for investigation
- ✅ Log exclusion ratio >60% (cost optimized)
- ✅ Service catalog complete with ownership
- ✅ Team-based access control implemented
- ✅ Dashboards use template variables consistently
- ✅ Error budget tracking established

### Key Datadog MCP Queries
```
# Tagging compliance
search_datadog_hosts(filter="*", include_all_tags=true)
search_datadog_services(query="*", detailed_output=true)

# SLO coverage (example - would need custom query)
# Query service count vs SLO count

# APM coverage
search_datadog_services(query="*")
search_datadog_spans(query="*", from="now-1h")

# Log pipeline efficiency
analyze_datadog_logs(filter="*", from="now-1d")
search_datadog_logs(query="*", from="now-1h")

# Dashboard maturity
search_datadog_dashboards(query="*", include_template_variables=true)
```

### Typical Duration
3-6 months for full standardization

### Graduation Criteria to Level 3
- Tagging compliance validated at >95%
- SLO tracking shows consistent monitoring
- APM providing actionable insights
- Log costs optimized with clear ROI
- Service catalog driving incident response

---

## Level 3: Managed (Optimization & Governance)

### Description
Cost optimization, governance scorecards, and production readiness checks are automated. Clear ownership and accountability established.

### Key Characteristics
- **Posture**: Managed with governance
- **Automation**: Cost optimization, compliance checks
- **Ownership**: Distributed (service teams own their observability)
- **Response**: Automated remediation for known issues
- **Documentation**: Self-service documentation portal

### Core Capabilities

| Capability | Criteria | MCP Assessment |
|------------|----------|----------------|
| **Cost Optimization** | Cost per service tracked, optimization playbook active | Query CCM allocation by team/service |
| **Governance Scorecard** | Production readiness scores for all services | Calculate scorecard metrics via MCP |
| **Unused Resource Detection** | Automated detection and decommissioning | Query low-traffic services |
| **Compliance Automation** | Automated compliance checks (GDPR, HIPAA, etc.) | Validate data residency and retention |
| **Fleet Automation** | Remote configuration for agent updates | Check fleet automation coverage |
| **Security Monitoring** | Security signals and vulnerability tracking | Query security findings |
| **Synthetic Monitoring** | Critical user journeys tested 24/7 | Query synthetic test results |

### Success Criteria
- ✅ Cost per service/team tracked monthly
- ✅ ≥20% cost optimization achieved from Level 2
- ✅ Production readiness scorecard >80% for critical services
- ✅ Unused services identified quarterly
- ✅ Compliance checks automated (100% coverage)
- ✅ Fleet automation managing ≥80% of agents
- ✅ Security findings triaged within SLA
- ✅ Synthetic tests covering critical paths

### Key Datadog MCP Queries
```
# Cost optimization
get_datadog_metric(
  queries=["sum:all.cost{*} by {service}.rollup(sum, daily)"],
  use_cloud_cost=true
)

# Service usage for decommissioning
search_datadog_services(query="*", detailed_output=true)
get_datadog_metric(queries=["sum:trace.requests{*} by {service}"])

# Governance scorecard (custom calculation)
# Combine: agent coverage, SLO existence, dashboard quality, log pipeline

# Compliance validation
search_datadog_logs(query="*", storage_tier="indexes", from="now-30d")
# Check retention policies, data residency

# Synthetic monitoring
# Query synthetic test results (specific API may vary)
```

### Typical Duration
6-12 months for governance maturity

### Graduation Criteria to Level 4
- Cost model validated and driving decisions
- Governance scorecard driving service improvements
- Compliance automation passing audits
- Self-service observability documented
- Teams owning their service observability

---

## Level 4: Optimized (Advanced Automation)

### Description
Self-healing systems, predictive analytics, and platform engineering enable teams to focus on innovation rather than operations.

### Key Characteristics
- **Posture**: Predictive and self-healing
- **Automation**: Workflow automation, auto-remediation
- **Ownership**: Autonomous service teams
- **Response**: Self-healing for common issues
- **Documentation**: Living documentation with AI assistance

### Core Capabilities

| Capability | Criteria | MCP Assessment |
|------------|----------|----------------|
| **Workflow Automation** | Common incidents auto-remediated | Query workflow execution metrics |
| **RUM Implementation** | Real user monitoring for all customer-facing apps | Query RUM session and performance data |
| **Advanced Anomaly Detection** | ML-powered anomaly detection active | Query anomaly detection coverage |
| **Incident Automation** | Automated incident creation and triage | Query incident automation rate |
| **Self-Service Platform** | Internal developer portal for observability | Measure adoption metrics |
| **Error Tracking** | Automated error grouping and prioritization | Query error tracking insights |
| **Platform Engineering** | Observability as a self-service platform | Measure platform adoption |

### Success Criteria
- ✅ ≥30% of incidents auto-remediated
- ✅ RUM data informing product decisions
- ✅ Anomaly detection reducing false positives
- ✅ MTTR reduced by ≥40% from Level 1
- ✅ Self-service platform adoption >70%
- ✅ Error tracking reducing duplicate investigations
- ✅ Platform engineering metrics tracked
- ✅ Observability embedded in CI/CD

### Key Datadog MCP Queries
```
# Workflow automation effectiveness
# Query workflow execution counts and success rates

# RUM performance
search_datadog_rum_events(
  query="@type:view",
  from="now-7d",
  detailed_output=true
)

# Error tracking
search_datadog_logs(query="status:error", from="now-7d")
# Analyze error patterns

# Incident automation metrics
search_datadog_incidents(query="*", from="now-30d")
# Calculate automation percentage

# Platform adoption
search_datadog_services(query="*")
# Compare against service catalog for coverage
```

### Typical Duration
12-18 months for advanced automation

### Graduation Criteria to Level 5
- Self-healing demonstrating clear MTTR reduction
- RUM insights driving product roadmap
- Platform engineering team established
- Observability perceived as competitive advantage
- Teams contributing back improvements

---

## Level 5: Excellence (Innovation & Leadership)

### Description
Industry leadership in observability, contributing to open source, sharing best practices, and driving innovation in SRE practices.

### Key Characteristics
- **Posture**: Innovation and thought leadership
- **Automation**: AI-driven operations
- **Ownership**: Community-driven improvement
- **Response**: Predictive prevention
- **Documentation**: Public best practices and contributions

### Core Capabilities

| Capability | Criteria | MCP Assessment |
|------------|----------|----------------|
| **ML Insights Adoption** | AI-driven insights informing architecture decisions | Query ML insights adoption |
| **Cross-Org Analytics** | Multi-org observability for complex enterprises | Analyze cross-org patterns |
| **Platform Engineering Excellence** | Internal platform recognized industry-wide | External metrics (conference talks, blog posts) |
| **Observability as Product** | Internal platform treated as product | Product metrics tracked |
| **Innovation Contributions** | Contributing to Datadog community, open source | Track contributions |
| **Advanced Use Cases** | Novel uses of observability data | Document unique implementations |
| **Thought Leadership** | Presenting at conferences, publishing content | External visibility metrics |

### Success Criteria
- ✅ AI insights driving architectural decisions
- ✅ Observability platform recognized externally
- ✅ Contributing to Datadog community regularly
- ✅ Publishing observability best practices
- ✅ Internal platform has product roadmap
- ✅ Predictive issue prevention demonstrable
- ✅ Observability driving business KPIs
- ✅ Industry recognition achieved

### Key Datadog MCP Queries
```
# Platform usage analytics
# Query all core metrics to demonstrate maturity
get_datadog_metric(queries=[
  "sum:datadog.agent.running{*}",
  "count:trace.requests{*}",
  "sum:datadog.estimated_usage.logs.ingested_events{*}"
])

# Cross-org analytics (if multi-org)
# Would require multiple org queries and aggregation

# Innovation metrics
# Track custom integrations, workflow automations, unique dashboards
search_datadog_dashboards(query="*")
search_datadog_notebooks(query="*")

# Business impact correlation
# Custom queries linking observability to business KPIs
```

### Typical Duration
18+ months, ongoing improvement

### Characteristics of Level 5 Organizations
- Observability is a competitive advantage
- Platform engineering is recognized discipline
- Innovation is continuous
- Best practices are shared publicly
- Teams seek to work there for observability culture

---

## Maturity Progression Matrix

| Dimension | L0 | L1 | L2 | L3 | L4 | L5 |
|-----------|----|----|----|----|----|----|
| **Agent Coverage** | 0% | 80% | 95% | 98% | 99% | 99%+ |
| **Tagging Compliance** | 0% | 40% | 95% | 98% | 99% | 99%+ |
| **SLO Coverage** | 0% | 0% | 80% | 90% | 95% | 98% |
| **APM Services** | 0% | 20% | 70% | 85% | 95% | 98% |
| **Automation %** | 0% | 10% | 30% | 50% | 70% | 85% |
| **MTTR Reduction** | baseline | 0% | -20% | -30% | -40% | -50%+ |
| **Self-Service %** | 0% | 0% | 20% | 50% | 70% | 85% |
| **Cost Optimization** | baseline | 0% | -10% | -20% | -25% | -30%+ |

---

## Assessment Methodology

Each level should be assessed using:
1. **Automated MCP Queries** - Objective data from Datadog
2. **Capability Checklist** - Manual validation of processes
3. **Team Interviews** - Qualitative assessment of practices
4. **Documentation Review** - Verify documentation completeness

See [assessment-methodology.md](./assessment-methodology.md) for detailed assessment process.
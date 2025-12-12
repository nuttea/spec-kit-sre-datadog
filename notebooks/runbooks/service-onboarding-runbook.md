---
title: Service Onboarding Runbook
type: runbook
version: 1.0
created: 2025-12-12
tags: [runbook, onboarding, monitoring, setup]
---

# Service Onboarding Runbook

**Metadata**
- Service Name: {{SERVICE_NAME}}
- Owner Team: {{TEAM}}
- Onboarding Date: {{DATE}}
- Runbook Author: {{AUTHOR}}
- Status: In Progress

## Service Overview

### Service Information

| Field | Value |
|-------|-------|
| **Service Name** | {{SERVICE_NAME}} |
| **Description** | {{DESCRIPTION}} |
| **Owner Team** | {{TEAM}} |
| **Tech Lead** | {{TECH_LEAD}} |
| **Repository** | [GitHub link] |
| **Documentation** | [Link] |
| **Architecture Diagram** | [Link] |

### Service Classification

- **Tier**: [Tier 0 - Critical / Tier 1 - Core / Tier 2 - Supporting / Tier 3 - Non-critical]
- **Type**: [API / Web Service / Background Worker / Data Pipeline / ML Service]
- **Language/Runtime**: _____
- **Framework**: _____
- **Deployment Method**: [Kubernetes / ECS / Lambda / VM]

### Dependencies

**Upstream Dependencies**:
- Service 1: {{SERVICE_1}}
- Service 2: {{SERVICE_2}}

**Downstream Dependencies**:
- Service 1: {{SERVICE_1}}
- Service 2: {{SERVICE_2}}

**External Dependencies**:
- Database: {{DATABASE}}
- Cache: {{CACHE}}
- Message Queue: {{QUEUE}}
- Third-party APIs: {{APIS}}

## Onboarding Checklist

### Phase 1: Planning (Week 1)

#### 1.1 Service Definition
- [ ] Service name decided and approved
- [ ] Service purpose documented
- [ ] Owner team assigned
- [ ] Tech lead identified
- [ ] On-call rotation planned
- [ ] Service tier classified

#### 1.2 Tagging Strategy
- [ ] UST tags defined:
  - `env`: {{ENV}} (e.g., prod, staging, dev)
  - `service`: {{SERVICE_NAME}}
  - `version`: {{VERSION_SCHEME}} (e.g., semver)
- [ ] Recommended tags planned:
  - `team`: {{TEAM}}
  - `application`: {{APPLICATION}}
- [ ] Tag format validated (lowercase, underscores)
- [ ] Tags documented in service README

#### 1.3 Monitoring Requirements
- [ ] SLIs identified (latency, availability, error rate)
- [ ] SLO targets defined
- [ ] Critical user journeys mapped
- [ ] Alerting thresholds planned
- [ ] On-call escalation defined

### Phase 2: Infrastructure Setup (Week 1-2)

#### 2.1 Datadog Agent Installation

**For Kubernetes**:
```bash
# Verify Datadog agent is deployed
kubectl get daemonset datadog-agent -n datadog

# Add service annotations to deployment
annotations:
  ad.datadoghq.com/{{SERVICE_NAME}}.logs: '[{"source":"{{SERVICE_NAME}}","service":"{{SERVICE_NAME}}"}]'
  ad.datadoghq.com/{{SERVICE_NAME}}.tags: '{"env":"{{ENV}}","service":"{{SERVICE_NAME}}","version":"{{VERSION}}"}'
```

**For Containers (Docker/ECS)**:
```bash
# Add Datadog agent as sidecar
# Configure DD_ENV, DD_SERVICE, DD_VERSION environment variables
```

**For VMs**:
```bash
# Install agent
DD_API_KEY={{DD_API_KEY}} DD_SITE="datadoghq.com" bash -c "$(curl -L https://install.datadoghq.com/scripts/install_script.sh)"

# Configure tags in /etc/datadog-agent/datadog.yaml
tags:
  - env:{{ENV}}
  - service:{{SERVICE_NAME}}
  - version:{{VERSION}}
  - team:{{TEAM}}
```

**Verification**:
```
# Query to verify agent reporting
search_datadog_hosts(query="service:{{SERVICE_NAME}}")
```

- [ ] Agent installed
- [ ] Agent reporting to Datadog
- [ ] Tags configured correctly
- [ ] Agent status: 🟢 Running

#### 2.2 Service Tagging Implementation

**Environment Variables**:
```bash
DD_ENV={{ENV}}
DD_SERVICE={{SERVICE_NAME}}
DD_VERSION={{VERSION}}
DD_TAGS=team:{{TEAM}},application:{{APPLICATION}}
```

**Verification Query**:
```
search_datadog_services(query="service:{{SERVICE_NAME}}")
```

**Expected Result**: Service appears with all tags

- [ ] Environment variables set
- [ ] Service appears in Datadog
- [ ] All UST tags present
- [ ] Recommended tags present
- [ ] Service catalog entry created

### Phase 3: APM Instrumentation (Week 2)

#### 3.1 APM Library Installation

**Node.js**:
```javascript
// Add to package.json
"dd-trace": "^4.0.0"

// Add to app entry point (BEFORE other imports)
require('dd-trace').init({
  env: process.env.DD_ENV,
  service: process.env.DD_SERVICE,
  version: process.env.DD_VERSION
});
```

**Python**:
```python
# requirements.txt
ddtrace

# Run with ddtrace
ddtrace-run python app.py
```

**Java**:
```bash
# Download agent
wget -O dd-java-agent.jar https://dtdg.co/latest-java-tracer

# Run application
java -javaagent:dd-java-agent.jar \
  -Ddd.env={{ENV}} \
  -Ddd.service={{SERVICE_NAME}} \
  -Ddd.version={{VERSION}} \
  -jar application.jar
```

**Go**:
```go
import "gopkg.in/DataDog/dd-trace-go.v1/ddtrace/tracer"

func main() {
    tracer.Start(
        tracer.WithEnv("{{ENV}}"),
        tracer.WithService("{{SERVICE_NAME}}"),
        tracer.WithServiceVersion("{{VERSION}}"),
    )
    defer tracer.Stop()
}
```

- [ ] APM library added to dependencies
- [ ] Tracer initialized in application
- [ ] Environment variables configured
- [ ] Application deployed with APM

#### 3.2 APM Verification

**Query traces**:
```
search_datadog_spans(
  query="service:{{SERVICE_NAME}}",
  from="now-1h"
)
```

**Check metrics**:
```
get_datadog_metric(
  queries=[
    "trace.{{SERVICE_NAME}}.request.hits",
    "trace.{{SERVICE_NAME}}.request.duration",
    "trace.{{SERVICE_NAME}}.request.errors"
  ],
  from="now-1h"
)
```

- [ ] Traces appearing in Datadog
- [ ] Service map shows service
- [ ] Dependencies auto-discovered
- [ ] Request metrics flowing
- [ ] Error traces captured

### Phase 4: Log Collection (Week 2)

#### 4.1 Log Configuration

**Application Logging Standard**:
```json
{
  "timestamp": "2025-12-12T10:00:00Z",
  "level": "INFO",
  "service": "{{SERVICE_NAME}}",
  "env": "{{ENV}}",
  "version": "{{VERSION}}",
  "message": "Request processed",
  "trace_id": "1234567890",
  "span_id": "0987654321",
  "user_id": "user123",
  "http.method": "GET",
  "http.url": "/api/endpoint",
  "http.status_code": 200,
  "duration_ms": 45
}
```

**Kubernetes Log Collection**:
```yaml
# Already configured if annotations added in 2.1
# Logs automatically collected from stdout/stderr
```

**Custom Log Path**:
```yaml
# /etc/datadog-agent/conf.d/{{SERVICE_NAME}}.d/conf.yaml
logs:
  - type: file
    path: "/var/log/{{SERVICE_NAME}}/*.log"
    service: "{{SERVICE_NAME}}"
    source: "{{SERVICE_NAME}}"
    tags:
      - env:{{ENV}}
      - team:{{TEAM}}
```

- [ ] Structured logging implemented
- [ ] Log format standardized (JSON)
- [ ] Trace correlation added (trace_id, span_id)
- [ ] Log collection configured
- [ ] Logs appearing in Datadog

#### 4.2 Log Verification

**Query logs**:
```
search_datadog_logs(
  query="service:{{SERVICE_NAME}}",
  from="now-1h",
  extra_fields=["trace_id", "span_id", "http.status_code"]
)
```

**Expected volume**:
```
analyze_datadog_logs(
  filter="service:{{SERVICE_NAME}}",
  sql_query="SELECT count(*) as logs, status FROM logs GROUP BY status",
  from="now-1h"
)
```

- [ ] Logs flowing to Datadog
- [ ] Log volume reasonable (<10GB/day for typical service)
- [ ] Trace correlation working
- [ ] All log levels present
- [ ] No PII in logs verified

### Phase 5: Monitoring Setup (Week 3)

#### 5.1 Golden Signals Monitors

**1. Latency Monitor**

**Query**:
```
avg(last_5m):avg:trace.{{SERVICE_NAME}}.request.duration{env:{{ENV}}} > 1000
```

**Configuration**:
- Threshold: p95 > 1000ms (warning), p95 > 2000ms (critical)
- Evaluation window: 5 minutes
- Notification: `@slack-{{TEAM}}-alerts @pagerduty-{{SERVICE}}`

**Runbook link**: [Link to latency troubleshooting runbook]

- [ ] Monitor created
- [ ] Thresholds validated with team
- [ ] Notifications configured
- [ ] Runbook linked

---

**2. Error Rate Monitor**

**Query**:
```
sum(last_5m):sum:trace.{{SERVICE_NAME}}.request.errors{env:{{ENV}}} / sum:trace.{{SERVICE_NAME}}.request.hits{env:{{ENV}}} > 0.01
```

**Configuration**:
- Threshold: error rate > 1% (warning), > 5% (critical)
- Evaluation window: 5 minutes
- Notification: `@slack-{{TEAM}}-alerts @pagerduty-{{SERVICE}}`

**Runbook link**: [Link to error investigation runbook]

- [ ] Monitor created
- [ ] Thresholds validated
- [ ] Notifications configured
- [ ] Runbook linked

---

**3. Throughput Monitor**

**Query**:
```
avg(last_15m):avg:trace.{{SERVICE_NAME}}.request.hits{env:{{ENV}}} < 10
```

**Configuration**:
- Threshold: requests < 10/s for 15 min (warning)
- Could indicate service down or traffic issue
- Notification: `@slack-{{TEAM}}-alerts`

- [ ] Monitor created
- [ ] Baseline calculated
- [ ] Notifications configured

---

**4. Saturation Monitor (Resource Usage)**

**Query**:
```
avg(last_10m):avg:system.cpu.user{service:{{SERVICE_NAME}},env:{{ENV}}} > 80
```

**Configuration**:
- CPU threshold: > 80% (warning), > 95% (critical)
- Memory threshold: > 85% (warning), > 95% (critical)
- Notification: `@slack-{{TEAM}}-alerts`

- [ ] CPU monitor created
- [ ] Memory monitor created
- [ ] Disk monitor created (if applicable)
- [ ] Thresholds validated

#### 5.2 Service-Specific Monitors

**Business Metric Monitors** (if applicable):
- [ ] Key business metric 1: _____
- [ ] Key business metric 2: _____

**Dependency Monitors**:
- [ ] Database connection pool monitor
- [ ] Cache hit rate monitor
- [ ] Queue depth monitor
- [ ] Third-party API availability

#### 5.3 Monitor Verification

**Query all monitors**:
```
search_datadog_monitors(query="service:{{SERVICE_NAME}}")
```

**Expected**: At least 4 Golden Signal monitors + service-specific monitors

- [ ] All monitors created
- [ ] All monitors have runbook links
- [ ] All monitors tested (manually trigger)
- [ ] All notification channels work
- [ ] Team acknowledged receipt of test alerts

### Phase 6: Dashboard Creation (Week 3)

#### 6.1 Service Dashboard

**Create dashboard from template**:
- Clone "App Overview Dashboard Template"
- Customize for {{SERVICE_NAME}}

**Required Widgets**:

1. **SLO Summary** (if SLOs defined)
2. **Request Rate** (timeseries)
   - Query: `sum:trace.{{SERVICE_NAME}}.request.hits{*}.as_rate()`
3. **Latency** (timeseries)
   - p50: `p50:trace.{{SERVICE_NAME}}.request.duration{*}`
   - p95: `p95:trace.{{SERVICE_NAME}}.request.duration{*}`
   - p99: `p99:trace.{{SERVICE_NAME}}.request.duration{*}`
4. **Error Rate** (timeseries)
   - Query: `sum:trace.{{SERVICE_NAME}}.request.errors{*}.as_rate()`
5. **Resource Usage** (timeseries)
   - CPU: `avg:system.cpu.user{service:{{SERVICE_NAME}}}`
   - Memory: `avg:system.mem.used{service:{{SERVICE_NAME}}}`
6. **Top Endpoints** (top list)
   - By request count
   - By latency
   - By error rate
7. **Dependency Health** (service map widget)
8. **Log Errors** (log stream)
   - Query: `service:{{SERVICE_NAME}} status:error`

**Template Variables**:
- `$env` - Environment filter
- `$version` - Version filter
- `$host` - Host filter

- [ ] Dashboard created
- [ ] All required widgets added
- [ ] Template variables configured
- [ ] Dashboard shared with team
- [ ] Dashboard URL documented: [Link]

#### 6.2 Dashboard Verification

- [ ] Dashboard loads quickly (<3 seconds)
- [ ] All widgets display data
- [ ] Template variables filter correctly
- [ ] Dashboard useful for troubleshooting
- [ ] Team trained on dashboard usage

### Phase 7: Alert Routing (Week 3)

#### 7.1 On-Call Configuration

**Datadog Teams**:
- [ ] Service added to {{TEAM}} in Datadog Teams
- [ ] Ownership documented
- [ ] Team members added

**PagerDuty Integration**:
- [ ] PagerDuty service created: `{{SERVICE_NAME}}-{{ENV}}`
- [ ] Escalation policy assigned
- [ ] Integration key configured in Datadog
- [ ] Test page sent and acknowledged

**Slack Integration**:
- [ ] Alert channel created: `#alerts-{{SERVICE_NAME}}`
- [ ] Channel added to monitors
- [ ] Team members joined channel

- [ ] Primary on-call: {{ONCALL_PRIMARY}}
- [ ] Secondary on-call: {{ONCALL_SECONDARY}}
- [ ] Escalation path documented

#### 7.2 Notification Testing

- [ ] Test alert sent to Slack
- [ ] Test page sent to PagerDuty
- [ ] Oncall acknowledged within SLA
- [ ] Escalation tested
- [ ] Notification preferences validated

### Phase 8: Documentation (Week 4)

#### 8.1 Service Documentation

**README.md updates**:
- [ ] Monitoring section added
- [ ] Dashboard link added
- [ ] Monitor links added
- [ ] On-call information added
- [ ] Runbook links added

**Service Catalog Entry**:
- [ ] Description updated
- [ ] Team ownership set
- [ ] Links added (repo, docs, dashboard)
- [ ] Dependencies documented
- [ ] SLOs added (if defined)

**Runbooks Created**:
- [ ] Service startup runbook
- [ ] Common alerts runbook
- [ ] Deployment runbook
- [ ] Rollback runbook
- [ ] Troubleshooting guide

#### 8.2 Team Training

- [ ] Team walkthrough scheduled
- [ ] Dashboard tour completed
- [ ] Alert response trained
- [ ] Runbooks reviewed
- [ ] Q&A session held
- [ ] Training materials shared

### Phase 9: SLO Definition (Week 4, Optional)

#### 9.1 SLO Planning

**SLI (Service Level Indicator)**: _____

**SLO (Service Level Objective)**:
- Target: _____% over _____ day rolling window
- Error budget: _____% (_____  requests)

**SLI Query**:
```
sum:trace.{{SERVICE_NAME}}.request.hits{*}.as_count() - sum:trace.{{SERVICE_NAME}}.request.errors{*}.as_count()
_______________________________________________________________________________
sum:trace.{{SERVICE_NAME}}.request.hits{*}.as_count()
```

- [ ] SLI defined
- [ ] SLO target agreed with stakeholders
- [ ] Error budget policy created
- [ ] SLO dashboard created
- [ ] SLO alerts configured

### Phase 10: Validation (Week 4)

#### 10.1 Onboarding Verification

**Run validation queries**:

**1. Service exists with correct tags**:
```
search_datadog_services(query="service:{{SERVICE_NAME}}")
```
Expected: Service found with env, version, team tags

**2. APM traces flowing**:
```
search_datadog_spans(query="service:{{SERVICE_NAME}}", from="now-1h")
```
Expected: >100 spans in last hour

**3. Logs flowing**:
```
analyze_datadog_logs(
  filter="service:{{SERVICE_NAME}}",
  sql_query="SELECT count(*) FROM logs",
  from="now-1h"
)
```
Expected: Logs present

**4. Monitors active**:
```
search_datadog_monitors(query="service:{{SERVICE_NAME}}")
```
Expected: ≥4 monitors (Golden Signals)

**5. Dashboard exists**:
```
search_datadog_dashboards(query="{{SERVICE_NAME}}")
```
Expected: Service dashboard found

#### 10.2 Onboarding Checklist Summary

| Phase | Status | Completion Date |
|-------|--------|----------------|
| Planning | ✅ | _____  |
| Infrastructure Setup | ✅ | _____ |
| APM Instrumentation | ✅ | _____ |
| Log Collection | ✅ | _____ |
| Monitoring Setup | ✅ | _____ |
| Dashboard Creation | ✅ | _____ |
| Alert Routing | ✅ | _____ |
| Documentation | ✅ | _____ |
| SLO Definition | ✅ / ⚪ | _____ |
| Validation | ✅ | _____ |

**Onboarding Complete**: ✅ / ❌

**Sign-off**:
- [ ] Service Owner: _____ (Date: _____)
- [ ] SRE Lead: _____ (Date: _____)
- [ ] On-call Lead: _____ (Date: _____)

## Post-Onboarding

### Week 1 After Onboarding
- [ ] Review alert noise (target: <5 alerts/day)
- [ ] Validate monitoring coverage
- [ ] Collect team feedback
- [ ] Adjust thresholds if needed

### Month 1 After Onboarding
- [ ] Review SLO performance (if applicable)
- [ ] Assess dashboard usage
- [ ] Review on-call experience
- [ ] Update runbooks based on incidents
- [ ] Conduct mini-assessment

## References

- **Service Repository**: [GitHub link]
- **Service Documentation**: [Confluence/Notion link]
- **Dashboard**: [Datadog link]
- **Monitors**: [Datadog link]
- **On-call Schedule**: [PagerDuty link]
- **Team Page**: [Datadog Teams link]

---

**Onboarding Status**: 🔴 Not Started / 🟡 In Progress / 🟢 Complete

**Completion Date**: _____

---

**Template Usage Notes**:
1. Copy this template for each new service
2. Customize all {{PLACEHOLDERS}}
3. Work through phases sequentially
4. Check off items as completed
5. Validate at each phase
6. Sign off when complete
7. Archive in Datadog Notebook: `/save-to-notebook`

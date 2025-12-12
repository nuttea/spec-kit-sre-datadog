---
title: SRE Maturity Level Readiness Assessment
type: assessment
version: 1.0
created: 2025-12-12
tags: [assessment, level-readiness, graduation, validation]
---

# SRE Maturity Level Readiness Assessment

**Metadata**
- Current Level: Level {{CURRENT_LEVEL}}
- Target Level: Level {{TARGET_LEVEL}}
- Date: {{DATE}}
- Owner: {{OWNER}}
- Status: Draft
- Priority: P1

## Objective

Validate readiness to graduate from Level {{CURRENT_LEVEL}} to Level {{TARGET_LEVEL}} by assessing compliance with all target level requirements.

## Success Criteria
- [ ] All critical requirements met (100%)
- [ ] All recommended requirements met (≥80%)
- [ ] Validation queries executed successfully
- [ ] Graduation criteria pass/fail determined
- [ ] Remediation plan created for gaps

## Current Level Assessment

### Level {{CURRENT_LEVEL}} Status

**Overall Compliance**: _____%

**Key Capabilities**:
- Capability 1: ✅ / ❌
- Capability 2: ✅ / ❌
- Capability 3: ✅ / ❌

## Target Level Requirements

### Level {{TARGET_LEVEL}}: {{LEVEL_NAME}}

---

## Level 0: Foundation - Requirements

### Critical Requirements (Must Pass All)

#### 1. Infrastructure Discovery Complete
**Requirement**: Complete inventory of all infrastructure components

**Validation Query**:
```
search_datadog_hosts(query="*")
```

**Criteria**:
- [ ] All production hosts identified
- [ ] Environment breakdown documented
- [ ] Cloud provider distribution known
- [ ] Network architecture mapped

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 2. Tagging Strategy Defined
**Requirement**: Documented tagging standard with UST baseline

**Validation Query**:
```
search_datadog_hosts(query="*", include_all_tags=true)
```

**Criteria**:
- [ ] UST tags defined (env, service, version)
- [ ] Recommended tags identified (team, application)
- [ ] Tag format standards documented
- [ ] Tagging governance process created

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 3. Cost Baseline Established
**Requirement**: 90-day cost baseline with breakdown by service/team

**Validation Query**:
```
get_datadog_metric(
  queries=["sum:all.cost{*}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-90d"
)
```

**Criteria**:
- [ ] Total cost calculated
- [ ] Cost per service identified
- [ ] Cost per team calculated
- [ ] Top cost drivers documented

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 4. Team Structure Documented
**Requirement**: Clear ownership and responsibility model

**Criteria**:
- [ ] SRE team identified
- [ ] Service ownership mapped
- [ ] On-call rotation defined
- [ ] Escalation paths documented

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

## Level 1: Reactive - Requirements

### Critical Requirements (Must Pass All)

#### 1. Agent Deployment ≥80%
**Requirement**: Datadog agent deployed to at least 80% of infrastructure

**Validation Query**:
```
search_datadog_hosts(query="*")
get_datadog_metric(queries=["avg:system.cpu.user{*}"], from="now-7d")
```

**Target**: ≥80% coverage

**Current**: _____%

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 2. Critical Monitors Created
**Requirement**: At least 5 critical monitors covering core services

**Validation Query**:
```
search_datadog_monitors(query="priority:1")
```

**Target**: ≥5 critical monitors

**Current**: _____ monitors

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 3. Core Dashboards Created
**Requirement**: Infrastructure and application dashboards deployed

**Validation Query**:
```
search_datadog_dashboards(query="*")
```

**Criteria**:
- [ ] Infrastructure overview dashboard
- [ ] Application performance dashboard
- [ ] At least 3 service-specific dashboards

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 4. Log Collection Active
**Requirement**: Production logs collected and indexed

**Validation Query**:
```
analyze_datadog_logs(
  filter="env:prod OR env:production",
  sql_query="SELECT count(*) FROM logs",
  from="now-7d"
)
```

**Target**: >100K logs per week

**Current**: _____ logs

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 5. Incident Tracking Process
**Requirement**: Formal incident declaration and tracking

**Validation Query**:
```
search_datadog_incidents(query="*", from="now-30d")
```

**Criteria**:
- [ ] Incident management process documented
- [ ] Incident creation workflow active
- [ ] At least 1 test incident created

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

## Level 2: Proactive - Requirements

### Critical Requirements (Must Pass All)

#### 1. UST Compliance ≥95%
**Requirement**: 95%+ of resources tagged with env, service, version

**Validation Query**:
```
search_datadog_hosts(query="*", include_all_tags=true)
analyze_datadog_logs(
  filter="*",
  sql_query="SELECT count(*) FROM logs WHERE env IS NOT NULL AND service IS NOT NULL",
  from="now-7d"
)
```

**Target**: ≥95%

**Current**: _____%

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 2. SLO Definition
**Requirement**: At least 3 SLOs defined for critical services

**Criteria**:
- [ ] SLO framework adopted
- [ ] 3+ SLOs created
- [ ] SLO dashboards deployed
- [ ] Error budgets tracked

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 3. APM Instrumentation ≥70%
**Requirement**: 70%+ of services instrumented with APM

**Validation Query**:
```
search_datadog_services(query="*")
search_datadog_spans(query="*", from="now-7d")
```

**Target**: ≥70% of services

**Current**: _____%

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 4. Alert Quality >80%
**Requirement**: Monitor health with <20% No Data/Alert rate

**Validation Query**:
```
search_datadog_monitors(query="*")
search_datadog_monitors(query="status:'No Data' OR status:Alert")
```

**Target**: <20% unhealthy monitors

**Current**: _____%

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 5. Automated Runbooks
**Requirement**: Runbooks for top 5 alert types

**Criteria**:
- [ ] Top 5 alert types identified
- [ ] Runbooks created for each
- [ ] Runbooks linked in monitors
- [ ] Team trained on runbooks

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

## Level 3: Managed - Requirements

### Critical Requirements (Must Pass All)

#### 1. Cost Optimization ≥20%
**Requirement**: 20%+ reduction from baseline

**Validation Query**:
```
get_datadog_metric(
  queries=["sum:all.cost{*}.rollup(sum, daily)"],
  use_cloud_cost=true,
  from="now-90d"
)
```

**Baseline Cost**: $_____
**Current Cost**: $_____
**Reduction**: _____%

**Target**: ≥20%

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 2. Incident MTTR <30min
**Requirement**: Average MTTR under 30 minutes

**Validation Query**:
```
search_datadog_incidents(query="state:resolved", from="now-90d")
```

**Target**: <30 minutes average

**Current**: _____ minutes

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 3. Service Catalog 100%
**Requirement**: All services documented in catalog

**Validation Query**:
```
search_datadog_services(query="*", detailed_output=true)
```

**Criteria**:
- [ ] All services have descriptions
- [ ] All services have teams assigned
- [ ] All services have links to docs
- [ ] Service dependencies mapped

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 4. Automated Remediation
**Requirement**: 5+ automated remediation workflows

**Criteria**:
- [ ] Auto-scaling configured
- [ ] Self-healing workflows active
- [ ] Automated rollback capable
- [ ] Synthetic test recovery automated

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

#### 5. Cost Governance
**Requirement**: Monthly cost reviews and optimization

**Criteria**:
- [ ] Monthly cost review process
- [ ] Cost anomaly detection active
- [ ] Budget alerts configured
- [ ] Chargeback/showback implemented

**Status**: ✅ Pass / ❌ Fail

**Evidence**:

---

## Graduation Criteria Summary

### Level {{TARGET_LEVEL}} Compliance

**Critical Requirements**:
- Total: _____
- Passed: _____
- Failed: _____
- **Pass Rate**: _____%

**Recommended Requirements**:
- Total: _____
- Passed: _____
- Failed: _____
- **Pass Rate**: _____%

### Overall Readiness

- [ ] **READY TO GRADUATE** - All critical requirements passed (100%)
- [ ] **NOT READY** - Gaps in critical requirements

## Gap Analysis

### Critical Gaps (Blocking Graduation)

1. **Gap 1**
   - Requirement:
   - Current State:
   - Target State:
   - Effort to Close:
   - Owner:
   - Due Date:

2. **Gap 2**
   - Requirement:
   - Current State:
   - Target State:
   - Effort to Close:
   - Owner:
   - Due Date:

### Recommended Gaps (Not Blocking)

1. **Gap 1**
   - Requirement:
   - Current State:
   - Effort to Close:

## Remediation Plan

### Phase 1: Critical Gaps (Required for Graduation)

| Task | Owner | Effort | Due Date | Status |
|------|-------|--------|----------|--------|
| | | | | |
| | | | | |

**Timeline**: _____ weeks

### Phase 2: Recommended Gaps (Post-Graduation)

| Task | Owner | Effort | Due Date | Status |
|------|-------|--------|----------|--------|
| | | | | |

**Timeline**: _____ weeks

## Validation Timeline

- **Assessment Start**: {{DATE}}
- **Gap Remediation**: _____ weeks
- **Re-validation**: _____
- **Graduation Target**: _____

## Next Steps

1. [ ] Review gaps with team
2. [ ] Assign owners to remediation tasks
3. [ ] Create project plan with timelines
4. [ ] Schedule regular check-ins
5. [ ] Re-run validation queries weekly
6. [ ] Declare graduation when ready
7. [ ] Run `/upgrade-plan` to get detailed implementation steps

## References

- **Current Level Documentation**: `planning/level-definitions.md`
- **Target Level Documentation**: `planning/level-definitions.md`
- **Gap Analysis Tool**: `/gap-analysis` command
- **Upgrade Plan Tool**: `/upgrade-plan` command
- **Assessment History**: [Links to previous assessments]

---

**Template Usage Notes**:
1. Copy this template when planning level graduation
2. Fill in {{CURRENT_LEVEL}} and {{TARGET_LEVEL}} placeholders
3. Run all validation queries
4. Mark each requirement Pass/Fail
5. Document evidence for each requirement
6. Create remediation plan for gaps
7. Re-validate weekly until ready
8. Graduate when all critical requirements pass
9. Save to Datadog Notebook: `/save-to-notebook`

---
title: Outage Analysis and Impact Assessment
type: postmortem
version: 1.0
created: 2025-12-12
tags: [postmortem, outage, sev1, impact-analysis]
---

# Outage Analysis and Impact Assessment

**Metadata**
- Outage ID: {{OUTAGE_ID}}
- Date: {{DATE}}
- Author: {{AUTHOR}}
- Status: Draft
- Severity: SEV-0 / SEV-1
- Systems Affected: {{SYSTEMS}}
- Customer Impact: Critical

## Outage Overview

### Executive Summary (For Leadership)

**What happened** (1-2 sentences):

**Customer impact** (1 sentence):

**Why it happened** (1 sentence):

**What we're doing** (1 sentence):

### Critical Metrics

| Metric | Value |
|--------|-------|
| **Outage Duration** | _____ hours _____ minutes |
| **Total Downtime** | _____ minutes |
| **Affected Customers** | _____ (_____ % of total) |
| **Geographic Scope** | [Global / Regional / Single Region] |
| **Failed Transactions** | _____ |
| **Revenue Impact** | $_____ (estimated) |
| **SLA Breach** | ✅ Yes / ❌ No |
| **SLA Credits** | $_____ |
| **MTTD** | _____ minutes |
| **MTTR** | _____ minutes |

## Outage Timeline

### Pre-Outage (Normal Operations)

**{{TIME}} - Baseline State**
- System health: 🟢 All systems operational
- Traffic level: _____ req/s (normal)
- Error rate: _____ % (normal)
- Key metrics: All within normal ranges

### Outage Begins

**{{TIME}} - First Sign of Issues**
- Initial symptom:
- System affected:
- Data source:
```
[Query showing first anomaly]
```

**{{TIME}} - Service Degradation**
- Degradation level: _____%
- Services impacted:
- User experience:
- Monitoring status:

**{{TIME}} - Complete Outage**
- All systems down: ✅ Yes / ❌ Partial
- Services completely unavailable:
- Error rate: _____%
- Customer-facing status:

### Detection and Response

**{{TIME}} - Outage Detected**
- Detection method:
  - [ ] Automated monitoring alert
  - [ ] Customer reports
  - [ ] Internal discovery
  - [ ] Status page check
- First responder:
- Alert details:

**{{TIME}} - Incident Declared**
- Severity: SEV-_____
- Incident commander:
- War room opened:
- Initial assessment:

**{{TIME}} - All Hands On Deck**
- Teams mobilized:
- Executive notification:
- External communication started:

### Investigation

**{{TIME}} - Investigation Begins**
- Initial hypothesis:
- Investigation approach:
- Systems checked:

**{{TIME}} - First Breakthrough**
- Discovery:
- Evidence:
- Changed strategy:

**{{TIME}} - Root Cause Identified**
- Root cause:
- Confirmation:
- Impact scope understood:

### Recovery

**{{TIME}} - Recovery Plan Formulated**
- Recovery approach:
- Estimated time:
- Risk assessment:
- Approval obtained from:

**{{TIME}} - Recovery Initiated**
- Action taken:
- Teams involved:
- Customer communication sent:

**{{TIME}} - Partial Service Restoration**
- Services restored:
- Percentage recovered: _____%
- Remaining issues:

**{{TIME}} - Full Service Restoration**
- All services operational: ✅ Yes
- Validation:
- Monitoring:

**{{TIME}} - Outage Officially Ended**
- Final status: 🟢 All systems operational
- Post-recovery monitoring:
- Total duration: _____ hours _____ minutes

## Customer Impact Analysis

### Quantitative Impact

**Query customer impact**:
```
analyze_datadog_logs(
  filter="status:error service:{{SERVICE}}",
  sql_query="SELECT count(DISTINCT user_id) as affected_users FROM logs",
  from="{{OUTAGE_START}}",
  to="{{OUTAGE_END}}"
)
```

**Affected Customers**:
- Total customers affected: _____
- Percentage of customer base: _____%
- Enterprise customers affected: _____
- Free tier customers affected: _____

**Failed Transactions**:
```
analyze_datadog_logs(
  filter="status:error",
  sql_query="SELECT service, count(*) as failed_requests FROM logs GROUP BY service",
  from="{{OUTAGE_START}}",
  to="{{OUTAGE_END}}"
)
```

| Service | Failed Requests | Typical Volume | Loss % |
|---------|----------------|----------------|---------|
| | | | ____% |
| | | | ____% |
| | | | ____% |

**Geographic Distribution**:
- North America: _____ customers (____%)
- Europe: _____ customers (____%)
- Asia Pacific: _____ customers (____%)
- Other: _____ customers (____%)

### Qualitative Impact

**Customer Experience**:
- Complete service unavailability: _____ minutes
- Degraded performance: _____ minutes
- Intermittent errors: _____ minutes
- User experience: [Unable to access / Slow / Error messages]

**Customer Segments Affected**:
- Critical business operations: _____
- Revenue-generating activities: _____
- Time-sensitive workflows: _____
- Real-time services: _____

**Social Impact**:
- Twitter mentions: _____
- Support tickets: _____
- Status page views: _____
- Community forum posts: _____

## Business Impact Analysis

### Revenue Impact

**Direct Revenue Loss**:
- Lost transactions: _____ × $_____ = $_____
- Subscription refunds: $_____
- SLA credits: $_____
- **Total direct loss**: $_____

**Indirect Revenue Impact**:
- Customer churn risk (estimated): _____ customers × $_____ LTV = $_____
- Deal pipeline impact: $_____
- Brand reputation cost: $_____ (estimated)
- **Total indirect impact**: $_____

**Total Business Impact**: $_____

### SLA and Commitments

**SLA Status**:
- SLA target: _____% uptime
- Actual uptime this month: _____%
- SLA breach: ✅ Yes / ❌ No
- SLA credits owed: $_____

**Affected Customers by SLA Tier**:
| Tier | Count | SLA | Breach | Credits |
|------|-------|-----|--------|---------|
| Enterprise | _____ | _____% | ✅/❌ | $_____ |
| Business | _____ | _____% | ✅/❌ | $_____ |
| Standard | _____ | _____% | ✅/❌ | $_____ |

### Operational Impact

**Engineering Cost**:
- Total engineering hours: _____ hours
- Teams involved: _____
- Overtime costs: $_____
- Opportunity cost: $_____

**Support Cost**:
- Support tickets created: _____
- Average handle time: _____ minutes
- Total support hours: _____ hours
- Escalations: _____

## Service Degradation Timeline

### Per-Service Impact

#### Service: {{SERVICE_1}}

**Query service health**:
```
get_datadog_metric(
  queries=[
    "avg:trace.{{SERVICE_1}}.request.hits{*}.as_rate()",
    "avg:trace.{{SERVICE_1}}.request.errors{*}.as_rate()",
    "avg:trace.{{SERVICE_1}}.request.duration{*}"
  ],
  from="{{OUTAGE_START_MINUS_1H}}",
  to="{{OUTAGE_END_PLUS_1H}}"
)
```

| Time Period | Status | Availability | Throughput | Error Rate |
|-------------|--------|--------------|------------|------------|
| Pre-outage | 🟢 | 99.9% | _____ req/s | 0.1% |
| During outage | 🔴 | ____% | _____ req/s | ____% |
| Post-recovery | 🟢 | 99.9% | _____ req/s | 0.1% |

**Impact**: [Critical / Severe / Moderate / Minor]

---

#### Service: {{SERVICE_2}}

[Same structure as SERVICE_1]

---

#### Service: {{SERVICE_3}}

[Same structure as SERVICE_1]

## Root Cause Analysis

### Incident Chain of Events

**Trigger Event**:
- What happened:
- When:
- Why it wasn't caught:

**Cascade Failure**:
1. **Event 1**: _____
   - System affected:
   - Propagation:
   - Why it cascaded:

2. **Event 2**: _____
   - System affected:
   - Propagation:
   - Why it cascaded:

3. **Event 3**: _____
   - System affected:
   - Propagation:
   - Why it cascaded:

### Technical Root Cause

**Primary Cause**:

**Technical Details**:
- Component:
- Failure mode:
- Why it failed:
- Why safeguards didn't work:

**Supporting Evidence**:
1. _____
2. _____
3. _____

### Contributing Factors

#### Technical Factors
1. **Factor**: _____
   - How it contributed:
   - Could it alone cause outage?: ✅ Yes / ❌ No

2. **Factor**: _____
   - How it contributed:
   - Could it alone cause outage?: ✅ Yes / ❌ No

#### Process Factors
1. **Factor**: _____
   - Process gap:
   - How it contributed:

2. **Factor**: _____
   - Process gap:
   - How it contributed:

#### Organizational Factors
1. **Factor**: _____
   - Organizational gap:
   - How it contributed:

## What Went Well

### Detection
1.
2.
3.

### Response
1.
2.
3.

### Communication
1.
2.
3.

### Recovery
1.
2.
3.

## What Went Wrong

### Detection Failures
1. **Failure**:
   - Impact:
   - Root cause of failure:
   - Prevention:

### Response Failures
1. **Failure**:
   - Impact:
   - Root cause of failure:
   - Prevention:

### Communication Failures
1. **Failure**:
   - Impact:
   - Root cause of failure:
   - Prevention:

### Recovery Delays
1. **Delay**:
   - Duration: _____ minutes
   - Reason:
   - Prevention:

## Communication Review

### Internal Communication

**Effectiveness**: 🟢 Excellent / 🟡 Good / 🔴 Poor

**What worked**:
1.
2.

**What needs improvement**:
1.
2.

### External Communication

**Timeline of Updates**:

| Time | Channel | Message | Response |
|------|---------|---------|----------|
| | Status page | | |
| | Email | | |
| | Twitter | | |
| | Support | | |

**Effectiveness**: 🟢 Excellent / 🟡 Good / 🔴 Poor

**Customer Feedback**:
-
-

### Executive Communication

**Timeline**:
- **{{TIME}}**: CEO notified
- **{{TIME}}**: Board notified
- **{{TIME}}**: Executive briefing
- **{{TIME}}**: Customer outreach began

## Prevention and Remediation

### Immediate Actions (Completed)

1. ✅ **Action 1**
   - Description:
   - Completed:
   - Verified:

2. ✅ **Action 2**
   - Description:
   - Completed:
   - Verified:

### Critical Action Items (P0 - This Week)

1. **[P0]** _____
   - **Description**:
   - **Owner**: _____
   - **Due**: _____
   - **Status**: ⚪ Not Started
   - **Tracking**: [Link]

2. **[P0]** _____
   - **Description**:
   - **Owner**: _____
   - **Due**: _____
   - **Status**: ⚪ Not Started
   - **Tracking**: [Link]

### High Priority Actions (P1 - This Month)

1. **[P1]** _____
   - **Description**:
   - **Owner**: _____
   - **Due**: _____
   - **Status**: ⚪ Not Started

2. **[P1]** _____
   - **Description**:
   - **Owner**: _____
   - **Due**: _____
   - **Status**: ⚪ Not Started

### Strategic Improvements (P2 - This Quarter)

1. **[P2]** _____
   - **Description**:
   - **Owner**: _____
   - **Due**: _____
   - **Status**: ⚪ Not Started

## System Improvements

### Architecture Changes

1. **Change**: _____
   - **Rationale**:
   - **Approach**:
   - **Timeline**:
   - **Investment**: $_____
   - **Expected benefit**:

### Resilience Improvements

1. **Improvement**: _____
   - **Current weakness**:
   - **Target state**:
   - **Implementation**:
   - **Owner**: _____

2. **Improvement**: _____
   - **Current weakness**:
   - **Target state**:
   - **Implementation**:
   - **Owner**: _____

### Monitoring Enhancements

1. **Monitor**: _____
   - **Purpose**: Early detection of similar issues
   - **Query**:
   - **Threshold**:
   - **Owner**: _____

2. **Dashboard**: _____
   - **Purpose**:
   - **Widgets**:
   - **Owner**: _____

## Lessons Learned

### Technical Lessons
1.
2.
3.

### Process Lessons
1.
2.
3.

### Communication Lessons
1.
2.
3.

### Organizational Lessons
1.
2.
3.

## Similar Incidents

**Previous related outages**:
- [Incident ID] - [Date] - [Similarity] - [Recurrence?: ✅/❌]
- [Incident ID] - [Date] - [Similarity] - [Recurrence?: ✅/❌]

**Pattern Analysis**:
- Recurring root causes:
- Common contributing factors:
- Systemic issues:

**Actions needed to break pattern**:
1.
2.
3.

## Customer Outreach Plan

### Proactive Communication

- [ ] Personal outreach to top 10 customers
- [ ] Email to all affected customers
- [ ] Status page detailed update
- [ ] Blog post explaining incident
- [ ] Support team briefing completed

### SLA Credit Processing

- [ ] Credits calculated: $_____
- [ ] Finance team notified
- [ ] Customer communications prepared
- [ ] Credits will be applied by: _____

### Relationship Management

**At-risk customers**: _____ (high churn probability)

**Mitigation plan**:
1. Customer 1: _____
2. Customer 2: _____
3. Customer 3: _____

## Follow-up and Tracking

### 30-Day Review

**Scheduled for**: _____

**Review scope**:
- [ ] All P0 actions completed
- [ ] All P1 actions in progress
- [ ] Prevention measures validated
- [ ] Monitoring effectiveness assessed
- [ ] Customer satisfaction recovered

### 90-Day Review

**Scheduled for**: _____

**Review scope**:
- [ ] All strategic improvements completed
- [ ] System resilience validated
- [ ] Similar incident recurrence: ✅ Yes / ❌ No
- [ ] Lessons learned integrated

## Approvals and Reviews

- [ ] **Author**: _____ (Date: _____)
- [ ] **Incident Commander**: _____ (Date: _____)
- [ ] **Engineering Manager**: _____ (Date: _____)
- [ ] **VP Engineering**: _____ (Date: _____)
- [ ] **CTO**: _____ (Date: _____)
- [ ] **CEO**: _____ (Date: _____ ) [if SEV-0]

## References

- **Incident Link**: [Datadog Incident]
- **War Room**: [Slack channel]
- **Status Page**: [Link]
- **Dashboard**: [Link]
- **Related Postmortems**: [Links]
- **Customer Communication**: [Links]
- **Media Coverage**: [Links]

---

**Outage Analysis Status**: 🔴 Draft / 🟡 Under Review / 🟢 Approved / 🔵 Published

**Publication Date**: _____ (for public postmortem)

---

**Template Usage Notes**:
1. Start within 6 hours of outage resolution
2. Complete draft within 24 hours
3. Include all quantitative impact data
4. Be thorough and transparent
5. Focus on prevention, not blame
6. Schedule review meetings
7. Track all action items rigorously
8. Follow up at 30 and 90 days
9. Share learnings broadly
10. Archive in Datadog Notebook: `/save-to-notebook`

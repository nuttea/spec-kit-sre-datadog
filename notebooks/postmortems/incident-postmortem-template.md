---
title: Incident Postmortem
type: postmortem
version: 1.0
created: 2025-12-12
tags: [postmortem, incident, learning, blameless]
---

# Incident Postmortem

**Metadata**
- Incident ID: {{INCIDENT_ID}}
- Date: {{DATE}}
- Author: {{AUTHOR}}
- Status: Draft
- Severity: {{SEVERITY}}
- Services Affected: {{SERVICES}}
- Reviewers: {{REVIEWERS}}

## Incident Overview

### Severity Classification

**Severity**: SEV-0 / SEV-1 / SEV-2 / SEV-3 / SEV-4

**Severity Definitions**:
- **SEV-0**: Complete outage, all users affected, business-critical
- **SEV-1**: Major degradation, significant user impact
- **SEV-2**: Partial degradation, some users affected
- **SEV-3**: Minor issues, minimal user impact
- **SEV-4**: No user impact, internal issues

### Executive Summary (3-4 sentences)

**What happened**:

**Why it happened**:

**What we did**:

**What we're doing to prevent it**:

### Quick Stats

| Metric | Value |
|--------|-------|
| **Duration** | _____ hours _____ minutes |
| **Detection Time** | _____ |
| **Time to Resolution** | _____ minutes |
| **MTTD** | _____ minutes |
| **MTTR** | _____ minutes |
| **Affected Users** | _____ (_____ %) |
| **Failed Requests** | _____ |
| **Revenue Impact** | $_____  |
| **SLO Impact** | _____ % |

## Timeline of Events

### Detection Phase

**{{TIME}}** - **Incident Start**
- System behavior:
- First indication:
- Data source:

**{{TIME}}** - **Detection**
- Detection method: [Monitor Alert / User Report / Internal Discovery]
- Alert link:
- Who detected:

**{{TIME}}** - **Acknowledgment**
- On-call engineer: _____
- Initial assessment:
- Severity declared: SEV-_____

### Investigation Phase

**{{TIME}}** - **Investigation Begins**
- First hypothesis:
- Investigation approach:
- Tools used:

**{{TIME}}** - **Escalation** (if applicable)
- Escalated to: _____
- Reason for escalation:
- Additional responders:

**{{TIME}}** - **Key Discovery 1**
- Finding:
- Evidence:
- Data source:

**{{TIME}}** - **Key Discovery 2**
- Finding:
- Evidence:
- Data source:

**{{TIME}}** - **Root Cause Identified**
- Root cause:
- Confirmation method:
- Evidence:

### Mitigation Phase

**{{TIME}}** - **Mitigation Plan Formed**
- Plan:
- Risk assessment:
- Approval:

**{{TIME}}** - **Mitigation Deployed**
- Action taken:
- Deployment method:
- Responsible party:

**{{TIME}}** - **Partial Recovery**
- Status:
- Metrics improving:
- Remaining issues:

**{{TIME}}** - **Full Recovery**
- Status: Fully resolved
- Validation:
- Incident closed:

### Post-Incident Phase

**{{TIME}}** - **Monitoring**
- Continued observation:
- Concerns:

**{{TIME}}** - **Incident Declared Resolved**
- Final status:
- Resolution confirmed:

## Root Cause Analysis (5 Whys)

### Problem Statement

**The incident**: _____

### 5 Whys Analysis

**1. Why did the incident occur?**

Answer:

**2. Why did that happen?**

Answer:

**3. Why did that happen?**

Answer:

**4. Why did that happen?**

Answer:

**5. Why did that happen?**

Answer:

### Root Cause Summary

**Technical Root Cause**:

**Organizational Root Cause**:

**Process Root Cause**:

## Contributing Factors

### Technical Factors

1. **Factor 1**: _____
   - Description:
   - How it contributed:
   - Could it have caused the incident alone?: ✅ Yes / ❌ No

2. **Factor 2**: _____
   - Description:
   - How it contributed:
   - Could it have caused the incident alone?: ✅ Yes / ❌ No

### Process Factors

1. **Factor 1**: _____
   - Description:
   - How it contributed:

2. **Factor 2**: _____
   - Description:
   - How it contributed:

### Human Factors

**Note**: This is a blameless postmortem. We focus on process and system improvements, not individual blame.

1. **Factor 1**: _____
   - Description:
   - System/process gap:
   - How to prevent:

## Impact Analysis

### User Impact

**Query affected users/requests**:
```
analyze_datadog_logs(
  filter="status:error service:{{SERVICE}}",
  sql_query="SELECT count(*) FROM logs",
  from="{{INCIDENT_START}}",
  to="{{INCIDENT_END}}"
)
```

**Metrics**:
- Total affected users: _____
- Percentage of user base: _____%
- Geographic distribution: _____
- User experience: [Complete outage / Degraded / Intermittent]

### Business Impact

**Revenue**:
- Direct revenue loss: $_____
- Calculation method: _____
- Potential revenue loss (if not resolved): $_____

**SLO Impact**:
- SLO target: _____ %
- Actual achievement: _____ %
- Error budget consumed: _____ %
- Error budget remaining: _____ %

**Customer Satisfaction**:
- Support tickets created: _____
- Customer complaints: _____
- Social media mentions: _____
- NPS impact: _____

### Operational Impact

- Engineering hours spent: _____ hours
- Teams involved: _____
- Customer success escalations: _____
- Executive involvement: ✅ Yes / ❌ No

## What Went Well

### Detection

1. **What worked**:
   - How it helped:
   - Why it worked:

2. **What worked**:
   - How it helped:
   - Why it worked:

### Response

1. **What worked**:
   - How it helped:
   - Why it worked:

2. **What worked**:
   - How it helped:
   - Why it worked:

### Communication

1. **What worked**:
   - How it helped:
   - Why it worked:

### Tooling/Systems

1. **What worked**:
   - How it helped:
   - Why it worked:

## What Went Wrong

### Detection Gaps

1. **What failed**:
   - Impact:
   - Why it failed:
   - How to improve:

2. **What failed**:
   - Impact:
   - Why it failed:
   - How to improve:

### Response Gaps

1. **What failed**:
   - Impact:
   - Why it failed:
   - How to improve:

2. **What failed**:
   - Impact:
   - Why it failed:
   - How to improve:

### Communication Gaps

1. **What failed**:
   - Impact:
   - Why it failed:
   - How to improve:

### Tooling/Process Gaps

1. **What failed**:
   - Impact:
   - Why it failed:
   - How to improve:

## Action Items

### Immediate (This Week)

1. **[P0]** _____
   - **Description**:
   - **Owner**: _____
   - **Due Date**: _____
   - **Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete
   - **Tracking**: [Jira/GitHub link]

2. **[P0]** _____
   - **Description**:
   - **Owner**: _____
   - **Due Date**: _____
   - **Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete
   - **Tracking**: [Jira/GitHub link]

### Short-term (This Month)

1. **[P1]** _____
   - **Description**:
   - **Owner**: _____
   - **Due Date**: _____
   - **Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete
   - **Tracking**: [Jira/GitHub link]

2. **[P1]** _____
   - **Description**:
   - **Owner**: _____
   - **Due Date**: _____
   - **Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete
   - **Tracking**: [Jira/GitHub link]

3. **[P2]** _____
   - **Description**:
   - **Owner**: _____
   - **Due Date**: _____
   - **Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete
   - **Tracking**: [Jira/GitHub link]

### Long-term (This Quarter)

1. **[P2]** _____
   - **Description**:
   - **Owner**: _____
   - **Due Date**: _____
   - **Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete
   - **Tracking**: [Jira/GitHub link]

2. **[P3]** _____
   - **Description**:
   - **Owner**: _____
   - **Due Date**: _____
   - **Status**: ⚪ Not Started / 🟡 In Progress / ✅ Complete
   - **Tracking**: [Jira/GitHub link]

## Prevention Measures

### Monitoring Improvements

1. **New Monitor**: _____
   - **Purpose**: Detect similar issues earlier
   - **Query**:
   ```
   [Datadog monitor query]
   ```
   - **Threshold**: _____
   - **Notification**: _____
   - **Owner**: _____
   - **Status**: _____

2. **Enhanced Dashboard**: _____
   - **Purpose**:
   - **Widgets added**:
   - **Link**: _____
   - **Owner**: _____
   - **Status**: _____

### Process Improvements

1. **Process Change**: _____
   - **Current process**: _____
   - **New process**: _____
   - **Expected benefit**: _____
   - **Owner**: _____
   - **Implementation date**: _____

2. **Process Change**: _____
   - **Current process**: _____
   - **New process**: _____
   - **Expected benefit**: _____
   - **Owner**: _____
   - **Implementation date**: _____

### Technical Improvements

1. **Technical Change**: _____
   - **Current state**: _____
   - **Target state**: _____
   - **Implementation plan**: _____
   - **Owner**: _____
   - **Completion date**: _____

2. **Technical Change**: _____
   - **Current state**: _____
   - **Target state**: _____
   - **Implementation plan**: _____
   - **Owner**: _____
   - **Completion date**: _____

### Runbook Updates

1. **Runbook**: _____
   - **Location**: _____
   - **Updates needed**: _____
   - **Owner**: _____
   - **Status**: _____

## Supporting Data

### Logs

**Query relevant logs**:
```
search_datadog_logs(
  query="service:{{SERVICE}} status:error",
  from="{{INCIDENT_START}}",
  to="{{INCIDENT_END}}",
  extra_fields=["error.message", "error.stack"]
)
```

**Key log entries**: [Attach or link to critical logs]

### Traces

**Query relevant traces**:
```
search_datadog_spans(
  query="service:{{SERVICE}} status:error",
  from="{{INCIDENT_START}}",
  to="{{INCIDENT_END}}"
)
```

**Key traces**: [Attach or link to trace IDs]

### Metrics

**Query relevant metrics**:
```
get_datadog_metric(
  queries=[
    "avg:trace.{{SERVICE}}.request.duration{*}",
    "sum:trace.{{SERVICE}}.request.errors{*}.as_rate()"
  ],
  from="{{INCIDENT_START_MINUS_1H}}",
  to="{{INCIDENT_END_PLUS_1H}}"
)
```

**Metric graphs**: [Attach or link to dashboard]

### Events

**Query relevant events**:
```
search_datadog_events(
  query="service:{{SERVICE}}",
  from="{{INCIDENT_START_MINUS_2H}}",
  to="{{INCIDENT_END}}"
)
```

**Key events**: _____

## Communication Log

### Internal Communication

**Incident Channel**: [Slack channel link]

**Key Updates**:
- **{{TIME}}**: _____
- **{{TIME}}**: _____
- **{{TIME}}**: _____

### External Communication

**Status Page Updates**:
- **{{TIME}}**: _____
- **{{TIME}}**: _____
- **{{TIME}}**: _____

**Customer Communication**:
- **Email sent**: ✅ Yes / ❌ No
- **Support notification**: ✅ Yes / ❌ No
- **Customer count notified**: _____

## Lessons Learned

### Key Takeaways

1.
2.
3.
4.
5.

### Similar Incidents

**Previous incidents**:
- [Incident ID] - [Date] - [Similarity]
- [Incident ID] - [Date] - [Similarity]

**Patterns**: _____

**Recurring issues**: _____

### Knowledge Sharing

- [ ] Postmortem review meeting scheduled (Date: _____)
- [ ] Team briefing completed
- [ ] Engineering all-hands presentation
- [ ] Documentation updated
- [ ] Runbook updated
- [ ] Training materials created

## Approvals

- [ ] **Author**: _____ (Date: _____)
- [ ] **Technical Reviewer**: _____ (Date: _____)
- [ ] **Manager**: _____ (Date: _____)
- [ ] **On-call Lead**: _____ (Date: _____)

## References

- **Incident Datadog Link**: [Link]
- **Dashboard**: [Link]
- **Slack Thread**: [Link]
- **Jira Tickets**: [Links]
- **Related Incidents**: [Links]
- **Runbook**: [Link]
- **Architecture Docs**: [Link]

---

**Postmortem Status**: 🔴 Draft / 🟡 Review / 🟢 Approved

**Review Date**: _____

**Follow-up Date**: _____ (30 days after incident)

---

**Template Usage Notes**:
1. Start postmortem within 24 hours of incident resolution
2. Focus on learning, not blame
3. Be specific and actionable
4. Include all supporting data
5. Schedule review meeting
6. Track all action items
7. Follow up on prevention measures
8. Share learnings across teams
9. Archive in Datadog Notebook: `/save-to-notebook`

---

**Remember**: The goal of this postmortem is to learn and improve our systems and processes, not to assign blame. We practice blameless postmortems to encourage honest reflection and continuous improvement.

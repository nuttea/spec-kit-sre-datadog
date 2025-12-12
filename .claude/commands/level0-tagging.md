# Level 0: Tagging Audit

Execute comprehensive tagging audit for Level 0 (Foundation).

**Task: Analyze Current Tagging Practices**

**Step 1: Query All Hosts with Tags**
```
search_datadog_hosts(
    context="Level 0: Auditing current tagging practices",
    filter="*",
    include_all_tags=True,
    max_tokens=50000
)
```

**Step 2: Analyze Required Tag Coverage**

Check coverage for Unified Service Tagging (UST) tags:
- **env tag**: `search_datadog_hosts(filter="env:*")`
- **service tag**: `search_datadog_hosts(filter="service:*")`
- **version tag**: `search_datadog_hosts(filter="version:*")`

Check coverage for business tags:
- **team tag**: `search_datadog_hosts(filter="team:*")`
- **cost_center tag**: `search_datadog_hosts(filter="cost_center:*")`

**Step 3: Identify Tag Format Issues**

Look for common anti-patterns:
- CamelCase tags: `env:Production` (should be `env:prod`)
- Inconsistent values: `env:production` vs `env:prod`
- Unbounded tags: timestamps, user IDs, request IDs in tags
- Special characters causing issues

**Step 4: Service-Level Tagging**
```
search_datadog_services(
    context="Analyzing service tagging",
    query="*",
    detailed_output=True
)
```

Check if services have proper metadata and tags.

**Step 5: Calculate Compliance Rates**

For each tag category:
- Total resources: [COUNT]
- Resources with tag: [COUNT]
- Compliance rate: [%]
- Gap: [COUNT resources missing tag]

**Analyze and Report:**

**Current State:**
1. env tag coverage: [%] - [STATUS]
2. service tag coverage: [%] - [STATUS]
3. version tag coverage: [%] - [STATUS]
4. team tag coverage: [%] - [STATUS]

**Tag Quality Issues:**
1. Format inconsistencies: [LIST]
2. Anti-patterns detected: [LIST]
3. Unbounded tag sources: [LIST]

**Recommended Tagging Strategy:**
1. Required tags: env, service, version
2. Recommended tags: team, cost_center, application
3. Tag format standards: lowercase, underscores
4. Tag validation approach

**Deliverable:**
Create tagging audit report and save to:
`maturity-levels/level-0-foundation/tagging-audit-report.md`

Include:
- Current compliance rates
- Identified issues with examples
- Recommended tagging standard
- Implementation roadmap
- Tag enforcement strategy
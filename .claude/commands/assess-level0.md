# Level 0: Foundation Assessment

Assess readiness for Level 0 (Foundation - Discovery & Planning phase).

**Level 0 Core Capabilities:**
- Complete infrastructure inventory
- Current state analysis and gap identification
- Cost baseline establishment
- Tagging strategy planning
- Team structure documentation

**Execute these checks:**

1. **Infrastructure Discovery**
   - Query: `search_datadog_hosts(filter="*", include_all_tags=True)`
   - Count total hosts vs cloud instances
   - Identify monitored vs unmonitored resources
   - List all environments and services

2. **Current Coverage Analysis**
   - Query: `get_datadog_metric(queries=["count:datadog.agent.running{*}"])`
   - Calculate baseline agent coverage
   - Identify monitoring gaps
   - Document existing tools

3. **Cost Baseline**
   - Query: `get_datadog_metric(queries=["sum:all.cost{*}.rollup(sum, monthly)"], use_cloud_cost=True)`
   - Establish cost baseline
   - Identify top cost drivers
   - Document current spend

4. **Tagging Audit**
   - Analyze existing tag usage
   - Identify tag inconsistencies
   - Document current tagging patterns
   - Recommend tagging strategy

**Success Criteria for Level 0:**
- ✅ Infrastructure inventory complete
- ✅ Cost baseline documented
- ✅ Monitoring gaps identified
- ✅ Tagging strategy drafted
- ✅ Team ownership mapped

**Deliver:**
- Level 0 readiness score
- Checklist of completed items
- Missing prerequisites
- Recommended actions to complete Level 0
- Estimated time to completion

**Output:** Save to `maturity-levels/level-0-foundation/assessment-results.md`
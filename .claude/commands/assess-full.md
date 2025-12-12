# Comprehensive SRE Maturity Assessment

Run a comprehensive SRE maturity assessment (30 minutes) with detailed analysis.

**Execute full assessment across all 8 dimensions:**

1. **Infrastructure Coverage**
   - Query all hosts with `search_datadog_hosts(filter="*", include_all_tags=True)`
   - Calculate agent deployment percentage
   - Identify cloud provider distribution
   - Check agent version consistency

2. **Tagging Compliance**
   - Audit env, service, version, team tags
   - Calculate compliance percentage
   - Identify non-compliant resources
   - Check tag format consistency

3. **Service Catalog**
   - Query all services with `search_datadog_services`
   - Check ownership assignments
   - Validate APM instrumentation
   - Verify documentation links

4. **Monitoring Quality**
   - Query all monitors with `search_datadog_monitors`
   - Check priority and team tags
   - Identify alert fatigue (>15 alerts/week)
   - Validate monitor routing

5. **Log Management**
   - Analyze log patterns with `analyze_datadog_logs`
   - Calculate exclusion ratio
   - Check pipeline coverage
   - Identify optimization opportunities

6. **Cost Optimization**
   - Query cloud costs with `get_datadog_metric(use_cloud_cost=True)`
   - Calculate cost per service/team
   - Identify unused services
   - Analyze spending trends

7. **Incident Management**
   - Query incidents with `search_datadog_incidents`
   - Calculate MTTR
   - Analyze severity distribution
   - Track incident trends

8. **Advanced Capabilities**
   - Check APM coverage with `search_datadog_spans`
   - Verify RUM implementation (if applicable)
   - Analyze dashboard maturity
   - Assess automation level

**Deliver comprehensive report:**
1. Executive summary with overall level
2. Detailed scores for each dimension
3. Strengths and achievements
4. Prioritized gap analysis (High/Medium/Low)
5. Actionable recommendations with effort estimates
6. Upgrade path to next level
7. Cost-benefit analysis

**After completing assessment:**

Automatically create Datadog Notebook with comprehensive results:

```
create_datadog_notebook(
    name="Level [DETECTED_LEVEL] - [Level Name] - Comprehensive Assessment - [DATE]",
    type="documentation",
    cells=... # Include full comprehensive assessment report
)
```

**Notebook naming format:**
- "Level [N] - [Level Name] - Comprehensive Assessment - YYYY-MM-DD"
- Example: "Level 2 - Optimization - Comprehensive Assessment - 2025-12-12"

Return notebook URL for team collaboration and quarterly reviews.
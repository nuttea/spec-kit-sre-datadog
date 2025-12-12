# Level 0: Cost Baseline

Establish cost baseline for Level 0 (Foundation).

**Task: Establish Observability Cost Baseline**

**Step 1: Query Total Cloud Spend (Last 90 Days)**
```
get_datadog_metric(
    context="Level 0: Establishing cost baseline",
    queries=["sum:all.cost{*}.rollup(sum, monthly)"],
    use_cloud_cost=True,
    from="now-90d",
    to="now"
)
```

**Step 2: Cost Breakdown by Service**
```
get_datadog_metric(
    context="Analyzing cost per service",
    queries=["sum:all.cost{*} by {service}.rollup(sum, daily)"],
    use_cloud_cost=True,
    from="now-30d"
)
```

**Step 3: Cost Breakdown by Team**
```
get_datadog_metric(
    context="Analyzing cost per team",
    queries=["sum:all.cost{*} by {team}.rollup(sum, daily)"],
    use_cloud_cost=True,
    from="now-30d"
)
```

**Step 4: Cost Breakdown by Environment**
```
get_datadog_metric(
    context="Analyzing cost by environment",
    queries=["sum:all.cost{*} by {env}.rollup(sum, daily)"],
    use_cloud_cost=True,
    from="now-30d"
)
```

**Step 5: Identify Top Cost Drivers**

Rank by cost:
1. Top 10 services by spend
2. Top 5 teams by spend
3. Top 3 environments by spend
4. Cost trends (increasing/decreasing)

**Step 6: Calculate Key Metrics**

- Total monthly cloud spend: $[AMOUNT]
- Estimated Datadog observability cost: $[AMOUNT]
- Observability as % of infrastructure: [%]
- Cost per service (average): $[AMOUNT]
- Cost per team (average): $[AMOUNT]

**Analyze and Report:**

**Cost Baseline Summary:**
1. **Monthly Spend**: $[AMOUNT]
   - Last 30 days: $[AMOUNT]
   - Previous 30 days: $[AMOUNT]
   - Trend: [↑ Increasing / → Stable / ↓ Decreasing]

2. **Cost Distribution**:
   - Production: [%] ($[AMOUNT])
   - Staging: [%] ($[AMOUNT])
   - Development: [%] ($[AMOUNT])

3. **Top Cost Drivers**:
   - Service: [NAME] - $[AMOUNT]
   - Service: [NAME] - $[AMOUNT]
   - Service: [NAME] - $[AMOUNT]

4. **Optimization Opportunities** (Preliminary):
   - Idle resources: [COUNT]
   - Low-utilization services: [COUNT]
   - Potential savings: $[AMOUNT] ([%])

**Deliverable:**

Automatically create Datadog Notebook with cost baseline:

```
create_datadog_notebook(
    name="Level 0 - Foundation - Cost Baseline - [DATE]",
    type="documentation",
    cells=... # Include cost analysis with charts and trends
)
```

**Notebook naming format:**
- "Level 0 - Foundation - Cost Baseline - YYYY-MM-DD"
- Example: "Level 0 - Foundation - Cost Baseline - 2025-12-12"

Include:
- Executive summary with key numbers
- Cost breakdown charts (tables)
- Trend analysis (if historical data available)
- Top cost drivers by service/team
- Preliminary optimization opportunities
- Baseline metrics for future comparison

Return notebook URL for team review and leadership reporting.
# Level 0: Infrastructure Discovery

Execute comprehensive infrastructure discovery and inventory for Level 0 (Foundation).

**Task: Complete Infrastructure Inventory**

**Step 1: Query All Monitored Hosts**
```
search_datadog_hosts(
    context="Level 0: Discovering all monitored infrastructure",
    filter="*",
    include_all_tags=True,
    max_tokens=50000
)
```

**Step 2: Analyze Cloud Provider Distribution**
Query hosts by cloud provider:
- AWS: `search_datadog_hosts(filter="cloud_provider:aws")`
- Azure: `search_datadog_hosts(filter="cloud_provider:azure")`
- GCP: `search_datadog_hosts(filter="cloud_provider:gcp")`
- On-premise: Identify hosts without cloud_provider tag

**Step 3: Environment Breakdown**
Query by environment:
- Production: `search_datadog_hosts(filter="env:prod")`
- Staging: `search_datadog_hosts(filter="env:staging")`
- Development: `search_datadog_hosts(filter="env:dev")`
- Untagged: Identify hosts missing env tag

**Step 4: Calculate Agent Coverage**
```
get_datadog_metric(
    context="Calculating current agent deployment",
    queries=[
        "count:datadog.agent.running{*}",
        "count:datadog.agent.running{*} by {env}",
        "count:datadog.agent.running{*} by {cloud_provider}"
    ],
    from="now-1h"
)
```

**Step 5: Service Discovery**
```
search_datadog_services(
    context="Discovering all services",
    query="*",
    detailed_output=False
)
```

**Analyze and Report:**
1. Total hosts monitored: [COUNT]
2. Cloud provider breakdown: AWS [%], Azure [%], GCP [%], On-prem [%]
3. Environment distribution: Prod [%], Staging [%], Dev [%]
4. Current agent coverage: [%]
5. Total services discovered: [COUNT]
6. Monitoring gaps identified: [LIST]

**Deliverable:**
Create infrastructure inventory report and save to:
`maturity-levels/level-0-foundation/infrastructure-inventory.md`

Include:
- Summary statistics
- Visual breakdown (tables)
- Identified gaps
- Recommendations for monitoring expansion
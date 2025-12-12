# The Datadog MCP Server

The Datadog MCP Server now supports improved search across Events, Logs, Spans, RUM, notebooks search and creation (in an experimental toolset), log pattern clustering to surface common error patterns with counts, and Cloud Cost Management queries for AWS and GCP cost analysis. Most tools now also use token-efficient TSV/YAML output formats and support selective field retrieval therefore significantly reducing response sizes while providing more focused results.

## Metrics MCP Tools

- Metrics tool calls now return backlinks if you want to view the corresponding queries in the Metrics Explorer in the Datadog UI
- Support for Cloud Cost Management (CCM) queries via v2 timeseries API.
- For example:
  - AWS Cost Breakdown: Summarize AWS cost data for the last 30 days by service using Cloud Cost Management
  - GCP Service Costs: Show GCP compute costs for the past week broken down by region

## Log Management MCP Tools

- Support for Flex Logs.
- Search log patterns with counts using the "group by message" option.
- New extra_fields argument to request only the attributes/tags you need.
- Include error.message content alongside message for better error analysis.
- Full API error details are now surfaced for easier troubleshooting.
- Sample prompts:
  - Error Pattern Analysis: Find error log patterns from shopist-web-ui service in the last 6 hours, group by message to see common issues
  - Targeted Field Retrieval: Search for authentication errors in the last day, include the "our_custom_field" attribute
- Query syntax checking to help agents run better queries based on common search terms and patterns, a few examples:
- Queries with common mistakes:
  - Input: @http.url:http://test.com
  - Returned suggestion: @http.url:"http://test.com"
- Service facets are checked against a comprehensive cache of all facet names, and a list of alternatives are provided.
  - Input: service:acmeServer
  - Returned suggestion: `service:acme-server
- All other facets are provided suggestions if your query yields zero results, e.g.:
  - Input: status:warn
  - Returned suggestion: status:warning, status:error

## APM MCP Tools

- Spans list can return selected custom attributes per request for more focused results.
- Improved query docs including duration examples and boolean expressions.
- Sample Prompts:
  - Performance with Custom Attributes: Find slow checkout operations in the last 4 hours with custom experiment attributes in YAML format
  - Error Analysis with Metadata: Search for error spans from web-store service with custom business context attributes

## Monitors MCP Tools

- Switched to the dedicated search API with simpler arguments and better state filtering.
- Now supports searching by title, notification content, and filtering by tags.
- Sample Prompts:
  - Active Critical Alerts: Find all monitors currently alerting in production environment
  - Service-Specific Monitoring: Search for monitors related to checkout functionality and high error rates

## Dashboards MCP Tools

- Migrated to the Dashboards Search v2 API with richer query and sorting support.
- Improved pagination and token-aware truncation, no longer limited to 10 items per call.
- Optional max_queries_per_dashboard parameter to speed up and control payload size.
- Sample Prompts:
  - Shared Team Dashboards: Find all shared dashboards related to the shopist app and run their key metrics queries
  - Infrastructure Monitoring: Search for dashboards containing system metrics and sort by popularity

## Incident Management MCP Tools

- Support for team:foo filters.
- Optional from/to time range to narrow results.
- Deterministic sorting (most recent first) and updated query syntax docs.
- Sample Prompts:
  - Critical Active Incidents: Show all SEV-1 incidents that are currently active from the last 30 days
  - Team-Specific Issues: Find incidents assigned to SRE team that occurred in the past week

## Services MCP Tools

- Switched to a new search API with proper pagination and a single query field (e.g., name:foo, team:bar) for flexible filtering.
- Fixed pagination so additional pages are fetched if token budget allows.
- Sample Prompts:
  - Service Discovery: Find services containing 'web-store' with detailed documentation links
  - Team Service Mapping: Search for all services owned by the shopist team

## Notebooks MCP Tools

- New experimental tools introduced to create, search, and retrieve notebooks. They need to be enabled separately as following:
- Sample Prompts:
  - Investigation Notebooks: Search for notebooks containing shopist checkout analysis
  - Incident Documentation: Find notebooks created for recent production issues

## Examples for custom agents using the Datadog MCP Server

Here are a few examples for custom agents some of our preview customers are considering the Datadog MCP Server for. Please keep sharing your use cases and requirements with us:

- Efficiency agent detecting unused services for decommissioning: AI agent to identify services with little to no real user traffic so they can be safely sunset. The goal is to help free up resources by retiring unused applications integrated with ticketing systems like Atlassian Jira to document the candidates for decommission.
- Governance agent for dashboard and monitoring best practices: Some companies struggle with disparate maturity of their Datadog adoption. Some teams are deeply integrated and advanced, others much less so. Getting engineers to donate their time can be difficult. An agent can give teams recommendations on how to adhere to internal and general Datadog best practices by comparing "good" dashboards and monitors following best practices against existing dashboards and monitors of specific teams.
- Performance improvement agent suggesting code improvements: Conducting comprehensive analyses of performance issues by correlating traces, versions, etc. whenever a problem arises and can even open a pull request with a proposed code change to resolve the issue. The addressed pain points would be the manual toil in diagnosing slowdowns and then implementing fixes.
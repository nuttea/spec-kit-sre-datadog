# SRE Spec Kit Slash Commands

This directory contains custom slash commands for the SRE Spec Kit.

## Available Commands

Type `/` in Claude Code to see all available commands, or type `/help` for a complete list.

### Assessment Commands (4)
- `/assess` - Quick assessment
- `/assess-full` - Comprehensive assessment
- `/assess-level0` - Level 0 check
- `/assess-level1` - Level 1 check

### Task Commands (6)
- `/level0-infra` - Infrastructure discovery
- `/level0-tagging` - Tagging audit
- `/level0-cost` - Cost baseline
- `/level0-healthcheck` - Health check report
- `/level2-tagging` - Level 2 tagging compliance
- `/level3-cost` - Level 3 cost optimization

### Utility Commands (3)
- `/gap-analysis` - Gap identification
- `/upgrade-plan` - Upgrade roadmap
- `/generate-report` - Executive report

## Usage

Simply type `/` followed by the command name in Claude Code:

```
/assess
```

All commands will:
1. Execute required Datadog MCP queries
2. Analyze results
3. Generate formatted reports
4. Save to appropriate directories
5. Provide actionable recommendations

## Documentation

See `../../COMMANDS.md` for complete documentation of each command.
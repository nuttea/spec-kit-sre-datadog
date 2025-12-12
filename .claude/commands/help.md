# Available SRE Spec Kit Commands

List all available slash commands for the SRE Spec Kit.

## 📊 Assessment Commands

- **`/assess`** - Quick 10-minute maturity assessment
- **`/assess-full`** - Comprehensive 30-minute assessment
- **`/assess-level0`** - Level 0 (Foundation) readiness check
- **`/assess-level1`** - Level 1 (Reactive) compliance check

## 📍 Level 0 Commands

- **`/level0-infra`** - Infrastructure discovery and inventory
- **`/level0-tagging`** - Comprehensive tagging audit
- **`/level0-cost`** - Cost baseline establishment
- **`/level0-healthcheck`** - Complete health check report

## 📍 Level 2+ Commands

- **`/level2-tagging`** - Tagging compliance check (95% target)
- **`/level3-cost`** - Cost optimization analysis (20% savings target)

## 🔧 Utility Commands

- **`/gap-analysis`** - Identify gaps between current and target level
- **`/upgrade-plan`** - Generate step-by-step upgrade roadmap
- **`/generate-report`** - Create executive summary report

## 📓 Notebook Commands (NEW)

- **`/assess-to-notebook`** - Run assessment & save to Datadog Notebook
- **`/save-to-notebook`** - Save any report to Datadog Notebook
- **`/append-to-notebook`** - Append to existing notebook

## 📖 Documentation

- **Full reference:** See `COMMANDS.md` in the repository root
- **Quick start:** See `QUICKSTART.md` in the repository root
- **Planning docs:** See `planning/` directory

## 🚀 Quick Examples

```bash
# First time user
/assess

# Level 0 discovery
/level0-infra
/level0-healthcheck

# Plan next steps
/gap-analysis
/upgrade-plan

# Executive reporting
/assess-full
/generate-report

# Save to Datadog Notebook (NEW)
/assess-to-notebook
/save-to-notebook
```

## 💡 Tips

1. Type `/` to see all available commands
2. Each command saves results automatically
3. Commands can be run multiple times to track progress
4. All commands use Datadog MCP queries for objective data

## 🆘 Not seeing commands?

If you don't see the commands when typing `/`:
1. Make sure you're in the correct directory
2. Try typing the full command name (e.g., `/assess`)
3. Check that `.claude/commands/` directory exists
4. Restart Claude Code if needed

For detailed documentation on each command, see: `COMMANDS.md`
---
name: debug-mining-engine
description: "Capture debugging sessions and transform them into reusable skills, code snippets, and pattern guides. Use when preserving debugging knowledge, building a library of error solutions, or reducing time spent on recurring issues."
user-invocable: true
triggers:
  - capture debugging session
  - save debug solution
  - mine debugging patterns
  - extract skills from errors
  - build debugging library
---

# Debug Mining Engine

Transform every debugging session into reusable skills, code snippets, and pattern guides. Every bug fixed becomes a permanent asset.

## When to Use

- Preserving debugging knowledge instead of losing it after a fix
- Building reusable solutions from errors already resolved
- Creating a growing library of debugging patterns
- Reducing time on recurring issues across projects

## How It Works

### Detection Modes

**AI Auto-Detection** (Passive): Monitors shell for error patterns, detects failures, starts background capture, and prompts after detecting a fix.

**Manual Override** (Active):
```bash
/debug-start "Description of what you're debugging"
# ... debug and fix the issue ...
/debug-end
```

### What Gets Captured

- **Error Context**: Full error message, stack trace, exit code
- **Solution Journey**: All attempts (including failures)
- **Final Solution**: The code/command that worked
- **Environment**: Working directory, relevant files
- **Metadata**: Duration, timestamps, tags

### What Gets Generated

1. **Full Skill** — Complete methodology with scripts, templates, and references in `debugging-patterns/[skill-name]/`
2. **Code Snippet** — Quick copy/paste solution in `debug-snippets/[category]/[name].sh`
3. **Pattern Guide** — Conceptual understanding document in `debug-patterns/[name].md`

## Setup

1. **Install monitoring**: `bash scripts/setup_monitor.sh`
2. **Create storage dirs**:
   ```bash
   mkdir -p ~/debug-sessions ~/debug-snippets/{database,api,filesystem,network,auth} ~/debug-patterns
   ```
3. **Test**: Run `/debug-start "test"`, trigger an error, run `/debug-end`, check `~/debug-sessions/`

## Usage Example

```bash
$ python3 audit_script.py
# Error: Could not find table 'repositories'
# [Debug Mining: Capture started automatically]

$ python3 audit_script.py --validate-schema
# Success! AI detects fix and prompts to save.

# Generated 3 assets:
#   1. Full Skill: supabase-schema-validator
#   2. Code Snippet: supabase-schema-check.sh
#   3. Pattern Guide: database-validation.md
```

## Scripts Reference

| Script | Purpose | Usage |
|--------|---------|-------|
| `setup_monitor.sh` | Install shell monitoring | `bash scripts/setup_monitor.sh` |
| `monitor.py` | Error detection and capture | `python3 scripts/monitor.py --exit-code 1 --command "cmd"` |
| `analyzer.py` | Pattern analysis and extraction | `python3 scripts/analyzer.py --session-id <id>` |
| `generator.py` | Multi-format skill generation | `python3 scripts/generator.py --session-id <id>` |
| `list_sessions.py` | List captured sessions | `python3 scripts/list_sessions.py --days 30` |
| `stats.py` | Show mining statistics | `python3 scripts/stats.py` |
| `search_patterns.py` | Search for similar patterns | `python3 scripts/search_patterns.py --error "table not found"` |

## Templates

- `skill_template/` — Template for generated full skills
- `snippet_template.sh` — Template for code snippets
- `pattern_template.md` — Template for pattern guides

## Best Practices

- **Add context**: `/debug-start "Fixing Supabase query error in audit script"` (not just "debugging")
- **Tag sessions**: `/debug-start "Fixing API timeout" --tags api,network,timeout`
- **Review generated skills** before committing to arsenal
- **Update existing skills** when a better solution is found: `python3 scripts/update_skill.py --skill <name> --session <id>`

## Intelligence Features

- **Pattern Recognition**: Detects recurring error types and suggests pre-flight validation skills
- **Proactive Suggestions**: Recommends new skills based on debugging history frequency
- **Learning Metrics**: Tracks debugging time reduction, skills generated, and reuse count

## Related Skills

- **systematic-debugging** — Methodical debugging approach
- **skill-arsenal-builder** — Build unified skill collections
- **skill-creator** — Create new skills from scratch
- **feature-verification** — Verify fixes work correctly

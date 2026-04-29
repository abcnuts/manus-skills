---
name: skill-arsenal-builder
description: "Build unified, organized skill arsenals with discovery systems, shared utilities, and cross-terminal deployment. Use when organizing 10+ skills into a structured collection, creating skill discovery and composition systems, or deploying skills across multiple terminals."
user-invocable: true
triggers:
  - build skill arsenal
  - organize skills collection
  - create skill registry
  - deploy skills cross-terminal
  - unify skill library
---

# Skill Arsenal Builder

Build unified, organized skill arsenals with discovery systems, shared utilities, meta-skill orchestration, and cross-terminal deployment.

## When to Use

- Building a collection of 10+ related skills into a unified system
- Organizing existing scattered skills into categories with a discovery layer
- Creating skill discovery and composition systems (registry, composer)
- Building meta-skills that orchestrate multi-skill workflows
- Deploying skills across multiple terminals with sync

## 5-Phase Build Process

### Phase 1: Audit & Organize

Understand what exists and structure it.

- `scripts/audit_skills.py` — Audit all skills, generate quality report
- `scripts/categorize_skills.py` — Organize into categories
- `scripts/reorganize_skills.py` — Restructure directories

**Output**: Audit report with quality ratings, organized repo structure, defined categories.

### Phase 2: Build Shared Utilities

Create the foundation layer to prevent code duplication.

- `templates/skill_utils.py` — Common utilities (validation, templates, logging)
- `templates/skill_registry.py` — Discovery system (find, suggest, compose)
- `templates/skill_composer.py` — Workflow orchestration
- `templates/skill_validator.py` — Quality assurance

### Phase 3: Add Discovery System

Make skills discoverable and composable.

- `scripts/generate_manifest.py` — Create `skills.json`
- `scripts/enhance_manifest.py` — Add metadata and relationships

**Output**: `skills.json` registry with full metadata, dependency graph, discovery API.

### Phase 4: Build New Skills (Optional)

Expand the arsenal by importing from verified repositories or building custom skills using templates.

### Phase 5: Integration & Meta-Skills

Create orchestration layer with meta-skills for complex workflows.

- `templates/README_template.md` — Arsenal documentation
- `templates/ARCHITECTURE_template.md` — Technical docs
- `templates/meta_skill_template.py` — Meta-skill orchestrator

## Cross-Terminal Deployment

### Builder Terminal Setup

After building the arsenal (Phases 1-5), create sync scripts and push to GitHub:

- `templates/skill-install` — First-time setup (clones from GitHub)
- `templates/skill-sync` — Pull latest skills
- `templates/skill-check` — Check for updates
- `templates/skill-status` — Show current status

### Receiver Terminal Setup

```bash
# 1. Add to PATH
echo 'export PATH="$PATH:$HOME/skill-sync-system"' >> ~/.bashrc && source ~/.bashrc

# 2. Install (fresh clone — do not merge with existing)
skill-install

# Expected: Cloned repo, installed X skills, registry loaded, ready in ~8 seconds
```

## Architecture

```
Layer 5: Meta-Skills (Orchestration)
Layer 4: Discovery & Dependency System
Layer 3: Individual Skills
Layer 2: Shared Utilities (lib/)
Layer 1: Foundation (Standards & Patterns)
```

### Repository Structure

```
arsenal/
├── lib/                    # Shared utilities
│   ├── skill_utils.py
│   ├── skill_registry.py
│   ├── skill_composer.py
│   └── skill_validator.py
├── meta-skills/            # Orchestrators
├── skills/                 # All skills by category
├── tools/                  # Maintenance scripts
├── docs/                   # Documentation
├── skills.json             # Registry
├── README.md
└── ARCHITECTURE.md
```

## Key Features

**Intelligent Discovery**:
```python
from lib.skill_registry import SkillRegistry
registry = SkillRegistry('skills.json')
db_skills = registry.find_by_tag("database")
workflow = registry.suggest_workflow("build a SaaS app")
complements = registry.get_complements("api-endpoint-builder")
```

**Automatic Dependency Resolution**: Orders skills based on dependencies (e.g., `database-schema-generator` → `api-endpoint-builder` → `testing-framework`).

**Version Tracking**: Every installation tracks commit hash, last sync time, skill count, and categories.

## Best Practices

1. **Start with audit** — always audit existing skills before building
2. **Use shared utilities** — put common functionality in `lib/`, avoid duplication
3. **Document everything** — every skill needs comprehensive SKILL.md with examples
4. **Test systematically** — 4-phase verification: structure, deployment, runtime, end-to-end
5. **Version control** — commit after each phase, use semantic versioning
6. **Fresh install for new terminals** — always fresh clone, not merge

## References

See the `references/` directory for detailed guides:
- `5-layer-architecture.md` — Complete system design
- `repository-structure.md` — Directory layout standards
- `skills-json-schema.md` — Registry format specification
- `github-workflow.md` — Deployment and sync process
- `verification-checklist.md` — Testing methodology
- `cross-terminal-handoff.md` — Multi-terminal deployment guide

## Time Estimates

| Phase | Time | Deliverables |
|-------|------|--------------|
| Phase 1: Audit & Organize | 2-3 days | Audit report, organized structure |
| Phase 2: Shared Utilities | 2 days | 4 utility modules, tests |
| Phase 3: Discovery System | 2-3 days | skills.json, discovery API |
| Phase 4: New Skills | Variable | New skills integrated |
| Phase 5: Meta-Skills | 3 days | Orchestrators, documentation |
| Cross-terminal deploy | ~8 seconds | Per terminal |

## Related Skills

- **skill-creator** — Create individual skills
- **skill-development-workflow** — Automate skill initialization
- **mcp-builder** — Convert skills to MCP servers
- **internet-skill-finder** — Discover skills from repositories

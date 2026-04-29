---
name: full-stack-builder
description: "Orchestrate 7+ skills to build complete full-stack applications from concept to deployment, handling requirements, database, API, auth, testing, deployment, and monitoring. Use when building a new application end-to-end, scaffolding a SaaS product, or coordinating multiple development skills into a single workflow."
type: meta-skill
user-invocable: true
triggers:
  - build full-stack app
  - scaffold new application
  - create SaaS product
  - orchestrate development workflow
  - end-to-end app builder
---

# Full Stack Builder

Meta-skill that orchestrates 7+ individual skills to build complete full-stack applications from concept to deployment.

## When to Use

- Building a new application end-to-end from requirements to production
- Scaffolding a SaaS product with auth, payments, and monitoring
- Coordinating multiple development skills into a sequenced workflow
- Automating the full development lifecycle for a greenfield project

## Workflow

1. **Requirements** — `brainstorming` to explore needs and design
2. **Database** — `database-schema-generator` to design schema from requirements
3. **Backend** — `api-endpoint-builder` to build API endpoints
4. **Auth** — `user-authentication-system` to add authentication
5. **Testing** — `testing-framework` to add comprehensive tests
6. **Deployment** — `deployment-automation` to deploy to production
7. **Monitoring** — `error-monitoring-setup` to configure error tracking

### Optional Skills (added based on requirements)

- `payment-integration` — if payments needed
- `file-upload-system` — if file uploads needed
- `email-system-builder` — if email notifications needed
- `analytics-dashboard` — if analytics needed

## Usage

### Command Line

```bash
python3 meta-skills/full-stack-builder/scripts/build_app.py "SaaS app with auth and payments"
```

### Programmatic

```python
from lib.skill_registry import SkillRegistry
from lib.skill_composer import SkillComposer

registry = SkillRegistry()
composer = SkillComposer(registry)

workflow_skills = [
    "brainstorming",
    "database-schema-generator",
    "api-endpoint-builder",
    "user-authentication-system",
    "testing-framework",
    "deployment-automation"
]

workflow = composer.compose_workflow(workflow_skills)
results = composer.execute_workflow(workflow, {"description": "My SaaS App"})
```

## Time Saved

- **Without meta-skill**: 30-35 hours of manual work
- **With meta-skill**: 4-5 hours of guided work
- **Savings**: 85-90% time reduction per application

## Dependencies

- All orchestrated skills must be available in the skill registry
- `lib/skill_registry.py` and `lib/skill_composer.py` must be initialized

## Notes

- This is a meta-skill — it orchestrates other skills, not implementation code
- Customize by adding or removing skills from the workflow
- Automatically resolves dependencies between skills

---
name: dispatching-parallel-agents
description: "Dispatch one agent per independent problem domain to solve multiple unrelated issues concurrently. Use when facing 2+ independent tasks without shared state, such as fixing failures across different test files, debugging separate subsystems, or parallelizing unrelated investigations."
user-invocable: true
triggers:
  - parallel agent dispatch
  - fix multiple independent failures
  - concurrent debugging
  - split tasks across agents
  - parallelize investigations
---

# Dispatching Parallel Agents

Dispatch one agent per independent problem domain to solve multiple unrelated issues concurrently instead of sequentially.

## When to Use

- 2+ test files failing with different root causes
- Multiple subsystems broken independently
- Each problem can be understood without context from others
- No shared state between investigations

## When NOT to Use

- Failures are related (fixing one might fix others) — investigate together first
- Full system context is required to understand the issue
- Exploratory debugging where the problem isn't yet identified
- Shared state exists (agents would edit same files or use same resources)

## The Pattern

### 1. Identify Independent Domains

Group failures by what's broken. Each domain must be independent — fixing one shouldn't affect another.

Example grouping:
- File A tests: Tool approval flow
- File B tests: Batch completion behavior
- File C tests: Abort functionality

### 2. Create Focused Agent Tasks

Each agent gets:
- **Specific scope**: One test file or subsystem
- **Clear goal**: Make these tests pass (or diagnose this issue)
- **Constraints**: Don't change unrelated code
- **Expected output**: Summary of root cause and changes made

### 3. Dispatch in Parallel

```typescript
Task("Fix agent-tool-abort.test.ts failures")
Task("Fix batch-completion-behavior.test.ts failures")
Task("Fix tool-approval-race-conditions.test.ts failures")
// All three run concurrently
```

### 4. Review and Integrate

- Read each agent's summary
- Check for conflicts (did agents edit same code?)
- Run full test suite to verify all fixes work together
- Spot-check for systematic errors

## Writing Good Agent Prompts

Effective prompts are **focused** (one problem domain), **self-contained** (all context included), and **specific about output** (what to return).

```markdown
Fix the 3 failing tests in src/agents/agent-tool-abort.test.ts:

1. "should abort tool with partial output capture" — expects 'interrupted at'
2. "should handle mixed completed and aborted tools" — fast tool aborted
3. "should properly track pendingToolCount" — expects 3 results, gets 0

These are timing/race condition issues. Your task:
1. Read the test file and understand what each test verifies
2. Identify root cause — timing issues or actual bugs?
3. Fix by replacing arbitrary timeouts with event-based waiting

Do NOT just increase timeouts — find the real issue.
Return: Summary of what you found and what you fixed.
```

### Common Mistakes

| Mistake | Fix |
|---------|-----|
| Too broad: "Fix all the tests" | Scope to one file: "Fix agent-tool-abort.test.ts" |
| No context: "Fix the race condition" | Paste error messages and test names |
| No constraints: agent refactors everything | "Do NOT change production code" |
| Vague output: "Fix it" | "Return summary of root cause and changes" |

## Real-World Example

**Scenario**: 6 test failures across 3 files after major refactoring.

| Agent | File | Root Cause | Fix |
|-------|------|-----------|-----|
| 1 | agent-tool-abort.test.ts (3 failures) | Timing issues | Replaced timeouts with event-based waiting |
| 2 | batch-completion-behavior.test.ts (2 failures) | Event structure bug | Fixed threadId placement |
| 3 | tool-approval-race-conditions.test.ts (1 failure) | Async completion | Added wait for async tool execution |

**Result**: All fixes independent, zero conflicts, full suite green. Three problems solved in the time of one.

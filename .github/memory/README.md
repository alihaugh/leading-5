# Working Memory System

## Purpose

This directory implements a **working memory system** for tracking patterns, decisions, and lessons discovered during development. It acts as a knowledge accumulation layer that helps AI assistants provide more context-aware suggestions based on your project's specific patterns and history.

## Why Two Types of Memory?

### Persistent Memory (`.github/copilot-instructions.md`)
- **Foundational principles** and workflows that rarely change
- **Project setup** and architecture decisions
- **Testing philosophy** and development standards
- **Always loaded** by GitHub Copilot

### Working Memory (`.github/memory/`)
- **Session-specific discoveries** and patterns
- **Code patterns** that emerge during development
- **Active session notes** for current work
- **Referenced on demand** for context-aware suggestions

This separation keeps core instructions focused while allowing detailed discovery documentation to grow over time.

## Directory Structure

```
.github/memory/
├── README.md                    # This file - explains the system
├── session-notes.md             # Historical session summaries (COMMITTED)
├── patterns-discovered.md       # Accumulated code patterns (COMMITTED)
└── scratch/
    ├── .gitignore              # Ignores scratch files
    └── working-notes.md        # Active session notes (NOT COMMITTED)
```

## File Usage Guide

### 1. `session-notes.md` - Historical Record

**Purpose**: Document completed sessions for future reference

**When to use**:
- ✅ **End of each development session** to summarize what was accomplished
- ✅ **After completing major milestones** (all tests passing, feature complete, etc.)
- ✅ **When switching between different work streams** to document progress

**What to include**:
- Session name/number and date
- What was accomplished (features, fixes, improvements)
- Key findings and decisions made
- Outcomes and test results

**Git status**: **COMMITTED** - This is your project's historical record

---

### 2. `patterns-discovered.md` - Pattern Library

**Purpose**: Document recurring code patterns discovered during development

**When to use**:
- ✅ **During TDD workflows** when you discover how code should be structured
- ✅ **During code reviews** when you identify good vs problematic patterns
- ✅ **During refactoring** when you establish better approaches
- ✅ **During debugging** when you find root causes of recurring issues

**What to document**:
- Pattern name and context
- Problem it solves
- Solution approach
- Code example
- Related files

**Git status**: **COMMITTED** - Accumulates knowledge over time

---

### 3. `scratch/working-notes.md` - Active Session

**Purpose**: Track thoughts, approaches, and findings during active development

**When to use**:
- ✅ **TDD workflows**: Document test failures, hypotheses, and implementation notes
- ✅ **Linting workflows**: Track error categories and systematic fixes
- ✅ **Debugging workflows**: Document symptoms, theories, and investigation steps
- ✅ **Implementation workflows**: Plan steps, track progress, note blockers

**Workflow**:
1. **Start of session**: Open `working-notes.md` and document your current task
2. **During work**: Add notes as you discover patterns, make decisions, or hit blockers
3. **End of session**: Review notes and extract key findings
4. **Summarize**: Add important discoveries to `session-notes.md` and `patterns-discovered.md`
5. **Clean**: Clear or archive `working-notes.md` for next session

**Git status**: **NOT COMMITTED** - Ephemeral, session-specific notes

---

## Using the Memory System in Workflows

### TDD Workflow (Red-Green-Refactor)

**Active Session**:
```markdown
## Current Task
Fixing POST /api/todos endpoint tests

## Approach
1. Read failing test to understand requirements
2. Implement minimal code to pass
3. Refactor for quality

## Key Findings
- Test expects 201 status with todo object
- Need to generate unique IDs
- createdAt should be ISO timestamp
```

**After Session**:
- Extract ID generation pattern → `patterns-discovered.md`
- Summarize test fixes → `session-notes.md`

---

### Linting Workflow

**Active Session**:
```markdown
## Current Task
Fix all ESLint errors in backend

## Approach
Fix by category: unused vars, then console logs

## Decisions Made
- Remove truly unused variables
- Replace console.log with proper error handling for production paths
- Keep debug console.logs for development (to be addressed later)
```

**After Session**:
- Document linting patterns → `patterns-discovered.md`
- Note clean code achievement → `session-notes.md`

---

### Debugging Workflow

**Active Session**:
```markdown
## Current Task
Toggle function always sets completed=true

## Investigation
1. Examined PATCH endpoint code
2. Found: `todo.completed = true` instead of `!todo.completed`
3. Root cause: Hardcoded boolean instead of toggle logic

## Blockers
None - straightforward fix

## Next Steps
1. Fix toggle logic
2. Write test to prevent regression
```

**After Session**:
- Document toggle pattern → `patterns-discovered.md`
- Note bug fix → `session-notes.md`

---

## How AI Reads and Applies Patterns

When you provide context from memory files, AI assistants can:

1. **Learn Project Patterns**
   - "Looking at `patterns-discovered.md`, I see you use incrementing ID counters"
   - "Following the service initialization pattern from memory..."

2. **Understand Project History**
   - "Based on your previous session notes, you've been focusing on backend stability"
   - "I see you encountered this toggle bug before..."

3. **Provide Contextual Suggestions**
   - "Applying the error handling pattern you documented..."
   - "Following your established approach for validation..."

4. **Avoid Repeated Mistakes**
   - "Your patterns show empty array initialization works better than null"
   - "Based on past findings, let's check for null references first"

---

## Best Practices

### DO ✅

- **Update `working-notes.md` frequently** during active development
- **Extract patterns** when you solve a problem more than once
- **Summarize sessions** while details are fresh in memory
- **Reference memory files** when asking AI for help
- **Keep patterns concise** with clear examples
- **Date your session notes** for tracking progress

### DON'T ❌

- **Don't commit `scratch/` directory** - it's for ephemeral notes
- **Don't let `working-notes.md` grow indefinitely** - summarize and clear
- **Don't document obvious patterns** - focus on non-trivial discoveries
- **Don't duplicate** what's already in `.github/copilot-instructions.md`
- **Don't skip summarizing** - historical context is valuable

---

## Quick Reference

| File | Purpose | When to Update | Git Status |
|------|---------|----------------|------------|
| `session-notes.md` | Historical session summaries | End of session | COMMITTED |
| `patterns-discovered.md` | Code patterns library | When pattern discovered | COMMITTED |
| `scratch/working-notes.md` | Active session notes | During work | NOT COMMITTED |

---

## Example Workflow

**Start of Session**:
```bash
# Open working notes
code .github/memory/scratch/working-notes.md

# Document current task
"Current Task: Implement DELETE endpoint for todos"
```

**During Development**:
```markdown
## Key Findings
- Need to validate ID format before lookup
- Array.filter() better than splice() for immutability
- Return 204 No Content on successful delete
```

**End of Session**:
1. Extract findings to `patterns-discovered.md`:
   - "Array Manipulation: Prefer filter() over splice()"
2. Add summary to `session-notes.md`:
   - "Session 5.3: DELETE endpoint implemented, all CRUD tests passing"
3. Clear `working-notes.md` for next session

**Result**: Knowledge preserved, ready for next session! 🎯

---

## Getting Started

1. **Start your first session** by opening `scratch/working-notes.md`
2. **Document your work** as you go - don't wait until the end
3. **Extract patterns** when you discover something useful
4. **Summarize** at the end to build your project's knowledge base
5. **Reference** these files when asking AI for context-aware help

Happy developing! 🚀

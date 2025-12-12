# GitHub Copilot Instructions for TODO Application

## Project Context

This is a full-stack TODO application with:
- **Frontend**: React application with modern UI components
- **Backend**: Express REST API with in-memory data storage
- **Development Philosophy**: Iterative, feedback-driven development with emphasis on testing and code quality
- **Current Phase**: Backend stabilization and frontend feature completion

## Documentation References

The project includes comprehensive documentation to guide development:

- [docs/project-overview.md](../docs/project-overview.md) - Architecture, tech stack, and project structure
- [docs/testing-guidelines.md](../docs/testing-guidelines.md) - Test patterns and standards for both frontend and backend
- [docs/workflow-patterns.md](../docs/workflow-patterns.md) - Development workflow guidance and best practices

Consult these documents when working on the project to understand context, patterns, and standards.

## Development Principles

Follow these core principles in all development work:

- **Test-Driven Development (TDD)**: Follow the Red-Green-Refactor cycle
  - Write tests FIRST that fail (RED)
  - Implement minimum code to pass (GREEN)
  - Refactor for quality while keeping tests passing (REFACTOR)
  
- **Incremental Changes**: Make small, focused modifications that are easy to test and review

- **Systematic Debugging**: Use test failures as guides to identify and fix issues methodically

- **Validation Before Commit**: Ensure all tests pass and no lint errors exist before committing code

## Testing Scope

This project uses **unit tests and integration tests ONLY**:

### Backend Testing
- **Framework**: Jest + Supertest
- **Focus**: API endpoint testing, request/response validation, error handling
- **Pattern**: RED-GREEN-REFACTOR - Write tests FIRST, then implement

### Frontend Testing
- **Framework**: React Testing Library
- **Focus**: Component behavior, user interactions, state management
- **Pattern**: RED-GREEN-REFACTOR - Write tests FIRST for component behavior, then implement
- **Manual Testing**: Follow up with manual browser testing for full UI flows

### What NOT to Use
- ❌ DO NOT suggest or implement e2e test frameworks (Playwright, Cypress, Selenium)
- ❌ DO NOT suggest browser automation tools
- ❌ DO NOT propose integration with headless browsers for automated testing

**Reason**: This lab focuses on unit and integration testing patterns without the complexity of end-to-end automation.

### Testing Approach by Context

- **Backend API changes**: Write Jest tests FIRST → Run tests → See failure → Implement code → Tests pass → Refactor
- **Frontend component features**: Write React Testing Library tests FIRST → Run tests → See failure → Implement component → Tests pass → Refactor → Manual browser verification for UI flows

This is **true TDD**: Test first, then code to pass the test.

## Workflow Patterns

Follow these established workflows for different development scenarios:

### 1. TDD Workflow (Red-Green-Refactor)
1. **Write or fix tests** that define the expected behavior
2. **Run tests** to see them fail (RED phase)
3. **Implement minimum code** to make tests pass
4. **Run tests** to verify they pass (GREEN phase)
5. **Refactor** code for quality while keeping tests passing
6. **Re-run tests** to ensure refactoring didn't break anything

### 2. Code Quality Workflow
1. **Run linter** to identify code quality issues
2. **Categorize issues** by type and severity
3. **Fix systematically** starting with critical issues
4. **Re-validate** by running linter again
5. **Commit** once all issues are resolved

### 3. Integration Workflow
1. **Identify issue** through testing or observation
2. **Debug** to understand root cause
3. **Write/update tests** to cover the issue
4. **Fix** the implementation
5. **Verify end-to-end** that the issue is resolved

## Chat Mode Usage

Use specialized chat modes for specific development tasks:

### tdd-developer Mode
Use for:
- Writing new tests before implementing features
- Debugging test failures
- Refactoring code while maintaining test coverage
- Implementing Red-Green-Refactor cycles
- Test-first development workflows

### code-reviewer Mode
Use for:
- Addressing lint errors and warnings
- Code quality improvements
- Code style consistency
- Reviewing code for best practices
- Systematic cleanup of code quality issues

## Memory System

This project implements a **working memory system** for tracking development discoveries and patterns:

- **Persistent Memory**: This file (`.github/copilot-instructions.md`) contains foundational principles and workflows that rarely change
- **Working Memory**: `.github/memory/` directory contains session-specific discoveries, code patterns, and active development notes

### Memory Files

- **`.github/memory/session-notes.md`** (COMMITTED): Historical record of completed sessions with accomplishments, key findings, and outcomes
- **`.github/memory/patterns-discovered.md`** (COMMITTED): Library of recurring code patterns discovered during development
- **`.github/memory/scratch/working-notes.md`** (NOT COMMITTED): Ephemeral notes for active session work

### Usage During Development

- **During active development**: Take notes in `.github/memory/scratch/working-notes.md` to track current task, approach, findings, decisions, and blockers
- **At end of session**: Summarize key findings and accomplishments into `.github/memory/session-notes.md`
- **When discovering patterns**: Document recurring code patterns in `.github/memory/patterns-discovered.md` with context, problem, solution, and examples
- **When asking AI for help**: Reference these files to provide context-aware suggestions based on project history and established patterns

### Why This Helps

The memory system allows AI assistants to:
- Learn your project's specific patterns and conventions
- Understand what has been accomplished in previous sessions
- Avoid suggesting approaches that have already been tried and abandoned
- Provide context-aware recommendations aligned with your project's evolution
- Reference established patterns when implementing new features

See [`.github/memory/README.md`](memory/README.md) for comprehensive usage guide.

## Workflow Utilities

The project uses GitHub CLI for workflow automation. These commands are available to all chat modes:

### Issue Management Commands

```bash
# List all open issues
gh issue list --state open

# View details of a specific issue
gh issue view <issue-number>

# View issue with all comments
gh issue view <issue-number> --comments
```

### Exercise Workflow

- The main exercise issue will have **"Exercise:"** in the title
- Development steps are posted as **comments** on the main exercise issue
- Use `/execute-step` prompt to work on the current step
- Use `/validate-step` prompt to verify step completion before moving forward
- Always check issue comments to understand the current step requirements

## Git Workflow

Follow these Git conventions and practices:

### Conventional Commits

Use conventional commit format for all commits:

- `feat:` - New feature
- `fix:` - Bug fix
- `chore:` - Maintenance tasks (dependencies, config)
- `docs:` - Documentation changes
- `test:` - Test additions or modifications
- `refactor:` - Code refactoring without behavior changes
- `style:` - Code style/formatting changes

**Examples**:
```bash
git commit -m "feat: add delete todo endpoint"
git commit -m "fix: resolve undefined state in TodoList component"
git commit -m "test: add integration tests for PUT /todos/:id"
git commit -m "docs: update testing guidelines with new patterns"
```

### Branch Strategy

- **Feature branches**: `feature/<descriptive-name>`
- **Bug fixes**: `fix/<descriptive-name>`
- **Main branch**: Protected, requires all tests to pass

### Commit Process

1. **Stage all changes**: `git add .`
2. **Commit with conventional format**: `git commit -m "type: description"`
3. **Push to correct branch**: `git push origin <branch-name>`
4. Always ensure tests pass before pushing

---

**Remember**: This is a learning lab focused on TDD practices and iterative development. Prioritize test-first development, incremental changes, and systematic problem-solving over rushing to solutions.

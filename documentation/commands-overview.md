# Commands Overview

This document provides a high-level overview of all available commands in the Claude Code ecosystem.

## Quick Reference

| Command | Purpose |
|---------|---------|
| `/build-fix` | Fix TypeScript and build errors incrementally |
| `/checkpoint` | Create or verify workflow checkpoints |
| `/code-review` | Comprehensive security and quality review |
| `/e2e` | Generate and run end-to-end tests with Playwright |
| `/eval` | Manage eval-driven development workflow |
| `/evolve` | Cluster related instincts into skills, commands, or agents |
| `/go-build` | Fix Go build errors and linter issues |
| `/go-review` | Comprehensive Go code review |
| `/go-test` | Enforce TDD workflow for Go |
| `/instinct-export` | Export instincts for sharing |
| `/instinct-import` | Import instincts from external sources |
| `/instinct-status` | Show all learned instincts with confidence levels |
| `/learn` | Extract reusable patterns from current session |
| `/orchestrate` | Sequential agent workflow for complex tasks |
| `/plan` | Create step-by-step implementation plan |
| `/refactor-clean` | Identify and remove dead code safely |
| `/setup-pm` | Configure preferred package manager |
| `/skill-create` | Generate SKILL.md from git history analysis |
| `/tdd` | Enforce test-driven development workflow |
| `/test-coverage` | Analyze and improve test coverage |
| `/update-codemaps` | Update architecture documentation |
| `/update-docs` | Sync documentation from source-of-truth |
| `/verify` | Run comprehensive verification checks |

---

## Build & Fix Commands

### /build-fix

**Purpose:** Incrementally fix TypeScript and build errors

**When to Use:**
- Build fails with TypeScript errors
- After pulling changes that break the build
- When fixing compilation issues

**How It Works:**
1. Runs build command (npm/pnpm build)
2. Parses and groups errors by file
3. Fixes one error at a time
4. Re-runs build to verify each fix
5. Stops if fix introduces new errors or same error persists after 3 attempts

---

### /go-build

**Purpose:** Fix Go build errors, vet warnings, and linter issues

**When to Use:**
- `go build ./...` fails
- `go vet ./...` reports issues
- `golangci-lint run` shows warnings
- Module dependencies are broken

**How It Works:**
1. Runs diagnostics: `go build`, `go vet`, `staticcheck`
2. Parses errors and groups by file
3. Fixes incrementally with minimal changes
4. Verifies each fix before proceeding

---

## Code Review Commands

### /code-review

**Purpose:** Comprehensive security and quality review of uncommitted changes

**When to Use:**
- Before committing code
- Reviewing pull requests
- After writing new functionality

**Checks For:**
- **Security (CRITICAL):** Hardcoded credentials, SQL injection, XSS, missing input validation
- **Quality (HIGH):** Large functions/files, deep nesting, missing error handling
- **Best Practices (MEDIUM):** Mutation patterns, missing tests, accessibility issues

---

### /go-review

**Purpose:** Go-specific code review for idiomatic patterns, concurrency, and security

**When to Use:**
- After writing or modifying Go code
- Before committing Go changes
- Reviewing Go pull requests

**Review Categories:**
- **CRITICAL:** Race conditions, SQL/command injection, goroutine leaks
- **HIGH:** Missing error wrapping, panic instead of error returns, unbuffered channels
- **MEDIUM:** Non-idiomatic patterns, missing godoc comments

---

## Testing Commands

### /tdd

**Purpose:** Enforce test-driven development workflow

**When to Use:**
- Implementing new features
- Fixing bugs (write failing test first)
- Building critical business logic

**TDD Cycle:**
1. **RED** - Write failing test
2. **GREEN** - Implement minimal code to pass
3. **REFACTOR** - Improve code while keeping tests green
4. **REPEAT** - Next feature/scenario

**Coverage Target:** 80%+ (100% for critical code)

---

### /go-test

**Purpose:** TDD workflow specifically for Go using table-driven tests

**When to Use:**
- Implementing new Go functions
- Adding test coverage to Go code
- Fixing Go bugs

**Features:**
- Table-driven test generation
- Parallel test support
- Coverage verification with `go test -cover`

---

### /e2e

**Purpose:** Generate and run end-to-end tests with Playwright

**When to Use:**
- Testing critical user journeys
- Verifying multi-step flows
- Validating frontend-backend integration
- Preparing for production deployment

**Features:**
- Generates Playwright tests using Page Object Model
- Runs tests across multiple browsers (Chrome, Firefox, Safari)
- Captures screenshots, videos, and traces on failures
- Identifies and quarantines flaky tests

---

### /test-coverage

**Purpose:** Analyze test coverage and generate missing tests

**When to Use:**
- Coverage below 80%
- After adding new code without tests
- Before major releases

**How It Works:**
1. Runs tests with coverage
2. Identifies files below 80% threshold
3. Generates tests for untested code paths
4. Verifies new tests pass

---

## Planning Commands

### /plan

**Purpose:** Create comprehensive implementation plan before writing code

**When to Use:**
- Starting a new feature
- Making architectural changes
- Complex refactoring
- Requirements are unclear

**Output:**
- Restated requirements
- Implementation phases with specific steps
- Dependencies identification
- Risk assessment
- Complexity estimate

**IMPORTANT:** Waits for explicit user confirmation before proceeding.

---

### /orchestrate

**Purpose:** Sequential agent workflow for complex tasks

**Workflow Types:**
- **feature:** planner → tdd-guide → code-reviewer → security-reviewer
- **bugfix:** explorer → tdd-guide → code-reviewer
- **refactor:** architect → code-reviewer → tdd-guide
- **security:** security-reviewer → code-reviewer → architect
- **custom:** User-defined agent sequence

See [orchestrate.md](./orchestrate.md) for detailed documentation.

---

## Verification Commands

### /verify

**Purpose:** Run comprehensive verification on codebase state

**Modes:**
- `quick` - Build + types only
- `full` - All checks (default)
- `pre-commit` - Commit-relevant checks
- `pre-pr` - Full checks plus security scan

**Verification Order:**
1. Build check
2. Type check
3. Lint check
4. Test suite
5. Console.log audit
6. Git status

---

### /checkpoint

**Purpose:** Create or verify workflow checkpoints

**Usage:**
- `create <name>` - Create named checkpoint
- `verify <name>` - Compare current state to checkpoint
- `list` - Show all checkpoints
- `clear` - Remove old checkpoints

**Tracks:**
- Files changed since checkpoint
- Test pass rate changes
- Coverage changes
- Build status

---

## Documentation Commands

### /update-docs

**Purpose:** Sync documentation from source-of-truth

**Generates:**
- `docs/CONTRIB.md` - Development workflow, scripts, environment setup
- `docs/RUNBOOK.md` - Deployment, monitoring, rollback procedures

**Sources:**
- package.json scripts
- .env.example variables

---

### /update-codemaps

**Purpose:** Update architecture documentation

**Generates:**
- `codemaps/architecture.md` - Overall architecture
- `codemaps/backend.md` - Backend structure
- `codemaps/frontend.md` - Frontend structure
- `codemaps/data.md` - Data models and schemas

**Features:**
- Calculates diff from previous version
- Requests approval if changes > 30%
- Adds freshness timestamps

---

## Refactoring Commands

### /refactor-clean

**Purpose:** Safely identify and remove dead code

**Tools Used:**
- knip - Find unused exports and files
- depcheck - Find unused dependencies
- ts-prune - Find unused TypeScript exports

**Safety:**
- Runs full test suite before each deletion
- Rolls back if tests fail
- Categorizes findings by severity (SAFE, CAUTION, DANGER)

---

## Learning & Pattern Commands

### /learn

**Purpose:** Extract reusable patterns from current session

**Extracts:**
- Error resolution patterns
- Debugging techniques
- Workarounds for library quirks
- Project-specific patterns

**Output:** Creates skill file at `~/.claude/skills/learned/[pattern-name].md`

---

### /skill-create

**Purpose:** Analyze git history to extract coding patterns and generate SKILL.md files

**Analysis:**
- Commit conventions
- File co-changes
- Workflow sequences
- Architecture patterns
- Testing patterns

**Usage:**
```
/skill-create                    # Analyze current repo
/skill-create --commits 100      # Last 100 commits
/skill-create --instincts        # Also generate instincts
```

---

### /evolve

**Purpose:** Cluster related instincts into higher-level structures

**Creates:**
- **Commands** - When instincts describe user-invoked actions
- **Skills** - When instincts describe auto-triggered behaviors
- **Agents** - When instincts describe complex, multi-step processes

**Example:**
Multiple instincts about database table creation → `/new-table` command

---

## Instinct Commands

### /instinct-status

**Purpose:** Show all learned instincts with confidence levels

**Displays:**
- Instincts grouped by domain
- Confidence scores (visual bars)
- Source (session-observation, repo-analysis, inherited)
- Last updated timestamp

---

### /instinct-export

**Purpose:** Export instincts for sharing

**Privacy:**
- Includes: Triggers, actions, confidence, domains
- Excludes: Code snippets, file paths, session transcripts

**Formats:** YAML, JSON, Markdown

---

### /instinct-import

**Purpose:** Import instincts from external sources

**Sources:**
- Teammates' exports
- Skill Creator analysis
- Community collections
- Previous machine backups

**Merge Strategies:**
- Higher confidence wins for duplicates
- Conflicting instincts flagged for manual resolution

---

## Configuration Commands

### /setup-pm

**Purpose:** Configure preferred package manager (npm/pnpm/yarn/bun)

**Detection Priority:**
1. Environment variable: `CLAUDE_PACKAGE_MANAGER`
2. Project config: `.claude/package-manager.json`
3. package.json: `packageManager` field
4. Lock file presence
5. Global config: `~/.claude/package-manager.json`
6. Fallback: pnpm > bun > yarn > npm

---

## Eval Commands

### /eval

**Purpose:** Manage eval-driven development workflow

**Subcommands:**
- `define <name>` - Create eval definition
- `check <name>` - Run evals and check status
- `report <name>` - Generate comprehensive report
- `list` - Show all eval definitions

**Metrics:**
- Capability evals: pass@3 > 90%
- Regression evals: pass^3 = 100%

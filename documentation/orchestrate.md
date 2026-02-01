# Orchestrate Command Overview

The `/orchestrate` command enables sequential agent workflows for complex software engineering tasks. It chains multiple specialized agents together, with each agent passing context to the next through structured handoff documents.

## Quick Start

```
/orchestrate [workflow-type] [task-description]
```

**Example:**
```
/orchestrate feature "Add user authentication"
```

## Available Workflows

| Workflow | Agent Chain | Use Case |
|----------|-------------|----------|
| **feature** | planner → tdd-guide → code-reviewer → security-reviewer | New feature implementation |
| **bugfix** | explorer → tdd-guide → code-reviewer | Bug investigation and fix |
| **refactor** | architect → code-reviewer → tdd-guide | Safe code refactoring |
| **security** | security-reviewer → code-reviewer → architect | Security-focused review |
| **custom** | [user-defined sequence] | Custom workflows |

## How It Works

1. **Invoke** the first agent with your task description
2. **Handoff** - agent produces structured output for the next agent
3. **Chain** - each agent receives context from the previous
4. **Report** - final agent produces a comprehensive summary

```
┌─────────┐    ┌───────────┐    ┌───────────────┐    ┌───────────────────┐
│ Planner │ -> │ TDD Guide │ -> │ Code Reviewer │ -> │ Security Reviewer │
└─────────┘    └───────────┘    └───────────────┘    └───────────────────┘
     │              │                  │                      │
   Plan         Tests &            Review &              Security &
  Created     Implementation      Feedback              Final Report
```

## Workflow Details

### Feature Workflow
Best for implementing new functionality from scratch.

- **Planner** - Creates implementation plan, identifies dependencies
- **TDD Guide** - Writes tests first, implements code to pass
- **Code Reviewer** - Reviews quality, suggests improvements
- **Security Reviewer** - Audits for vulnerabilities, gives final approval

### Bugfix Workflow
Best for investigating and fixing bugs.

- **Explorer** - Investigates the bug, identifies root cause
- **TDD Guide** - Writes regression test, implements fix
- **Code Reviewer** - Verifies fix quality and completeness

### Refactor Workflow
Best for restructuring code safely.

- **Architect** - Designs new structure, evaluates trade-offs
- **Code Reviewer** - Reviews changes for quality
- **TDD Guide** - Ensures tests cover refactored code

### Security Workflow
Best for security audits and hardening.

- **Security Reviewer** - Identifies vulnerabilities
- **Code Reviewer** - Reviews remediation changes
- **Architect** - Evaluates security architecture

## Custom Workflows

Create your own agent sequence:

```
/orchestrate custom "architect,tdd-guide,code-reviewer" "Redesign caching layer"
```

## Parallel Execution

For independent checks, agents can run simultaneously:

- code-reviewer (quality)
- security-reviewer (security)
- architect (design)

Results are merged into a single report.

## Final Report

Every orchestration produces a final report containing:

- **Summary** - One paragraph overview
- **Agent Outputs** - Key findings from each agent
- **Files Changed** - All modified files
- **Test Results** - Pass/fail summary
- **Security Status** - Security findings
- **Recommendation** - SHIP / NEEDS WORK / BLOCKED

## Best Practices

1. Use **feature** workflow for complex new functionality
2. Always include **code-reviewer** before merging
3. Use **security-reviewer** for auth, payments, or PII handling
4. Keep handoffs focused on what the next agent needs
5. Run verification between agents when needed

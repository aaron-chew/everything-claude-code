# Available Agents Overview

This document provides a comprehensive overview of all available agents in the Claude Code ecosystem.

## Core Agents

### 1. Planner

**Purpose:** Expert planning specialist for complex features and refactoring

**When to Use:** Proactively for feature implementation, architectural changes, or complex refactoring

**Key Responsibilities:**
- Analyze requirements and create detailed implementation plans
- Break down complex features into manageable steps
- Identify dependencies and potential risks
- Suggest optimal implementation order

---

### 2. TDD Guide

**Purpose:** Test-Driven Development specialist enforcing write-tests-first methodology

**When to Use:** Proactively when writing new features, fixing bugs, or refactoring code

**Key Responsibilities:**
- Enforce tests-before-code methodology
- Guide through Red-Green-Refactor cycle
- Ensure 80%+ test coverage
- Write comprehensive test suites (unit, integration, E2E)

---

### 3. Code Reviewer

**Purpose:** Expert code review specialist for quality, security, and maintainability

**When to Use:** Proactively after writing or modifying code (recommended for all code changes)

**Key Responsibilities:**
- Ensure code is simple and readable
- Check for security issues and exposed secrets
- Verify test coverage
- Analyze performance and time complexity

---

### 4. Security Reviewer

**Purpose:** Security vulnerability detection and remediation specialist

**When to Use:** Proactively after writing code handling user input, authentication, API endpoints, or sensitive data

**Key Responsibilities:**
- Identify OWASP Top 10 vulnerabilities
- Flag hardcoded secrets and injection risks
- Detect SQL injection, XSS, SSRF, CSRF vulnerabilities
- Ensure input validation and proper authentication/authorization

---

### 5. Architect

**Purpose:** Software architecture specialist for system design, scalability, and technical decision-making

**When to Use:** Proactively when planning new features, refactoring large systems, or making architectural decisions

**Key Responsibilities:**
- Design system architecture for new features
- Evaluate technical trade-offs
- Recommend patterns and best practices
- Identify scalability bottlenecks and plan for growth

---

### 6. Build Error Resolver

**Purpose:** Build and TypeScript error resolution specialist

**When to Use:** Proactively when build fails or type errors occur

**Key Responsibilities:**
- Fix TypeScript errors and type inference issues
- Resolve compilation failures and module resolution issues
- Make minimal changes with surgical diffs (no architectural edits)
- Get builds passing quickly

---

### 7. Refactor Cleaner

**Purpose:** Dead code cleanup and consolidation specialist

**When to Use:** Proactively for removing unused code, duplicates, and refactoring

**Key Responsibilities:**
- Run analysis tools (knip, depcheck, ts-prune) to identify dead code
- Consolidate duplicate code
- Remove unused packages and imports
- Maintain deletion logs for all removals

---

### 8. E2E Runner

**Purpose:** End-to-end testing specialist

**When to Use:** Proactively for generating, maintaining, and running E2E tests

**Key Responsibilities:**
- Create and maintain E2E tests for user flows
- Manage flaky test detection and quarantine
- Capture and upload artifacts (screenshots, videos, traces)
- Ensure critical user journeys work correctly

---

### 9. Doc Updater

**Purpose:** Documentation and codemap specialist

**When to Use:** Proactively for updating codemaps and documentation

**Key Responsibilities:**
- Generate architectural maps from codebase structure
- Update READMEs and guides from code
- Perform AST analysis for dependency mapping
- Track imports/exports relationships

---

### 10. Database Reviewer

**Purpose:** PostgreSQL database specialist for query optimization, schema design, security, and performance

**When to Use:** Proactively when writing SQL, creating migrations, designing schemas, or troubleshooting database performance

**Key Responsibilities:**
- Optimize queries and add proper indexes
- Design efficient schemas with proper data types and constraints
- Implement Row Level Security (RLS) and security best practices
- Manage connections, concurrency, and prevent deadlocks

---

### 11. Go Reviewer

**Purpose:** Expert Go code reviewer specializing in idiomatic Go, concurrency patterns, error handling, and performance

**When to Use:** For all Go code changes

**Key Responsibilities:**
- Ensure idiomatic Go patterns
- Review concurrency patterns and detect race conditions
- Verify proper error handling with error wrapping
- Check security issues (SQL injection, command injection, race conditions)

---

### 12. Go Build Resolver

**Purpose:** Go build, vet, and compilation error resolution specialist

**When to Use:** When Go builds fail or vet issues occur

**Key Responsibilities:**
- Fix Go compilation errors
- Resolve `go vet` issues and linter warnings
- Handle module dependency problems
- Fix type errors and interface mismatches

---

## Orchestration Workflows

The `/orchestrate` command supports predefined agent workflows:

| Workflow | Agent Sequence | Purpose |
|----------|----------------|---------|
| **feature** | planner → tdd-guide → code-reviewer → security-reviewer | Full feature implementation |
| **bugfix** | explorer → tdd-guide → code-reviewer | Bug investigation and fix |
| **refactor** | architect → code-reviewer → tdd-guide | Safe refactoring |
| **security** | security-reviewer → code-reviewer → architect | Security-focused review |
| **custom** | [user-defined] | Custom agent sequence |

## Quick Reference

| Agent | Best For |
|-------|----------|
| Planner | Complex features, architectural changes |
| TDD Guide | New features, bug fixes, refactoring |
| Code Reviewer | All code changes |
| Security Reviewer | Auth, user input, API endpoints, sensitive data |
| Architect | System design, technical decisions |
| Build Error Resolver | TypeScript/build failures |
| Refactor Cleaner | Dead code removal, consolidation |
| E2E Runner | End-to-end testing |
| Doc Updater | Documentation, codemaps |
| Database Reviewer | SQL, schemas, database performance |
| Go Reviewer | Go code changes |
| Go Build Resolver | Go compilation issues |

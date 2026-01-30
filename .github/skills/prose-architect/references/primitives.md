# Agent Primitives Guide

Quick reference for each primitive type.

## Instructions (`.instructions.md`)

**Purpose:** Persistent rules that guide agent behavior.

**Key feature:** `applyTo` pattern in frontmatter scopes when rules load.

```markdown
---
applyTo: "**/*.tsx"
description: "React component guidelines"
---
# React Guidelines

- Use functional components with TypeScript
- Implement error boundaries
- Test with React Testing Library
```

**PROSE alignment:** Explicit Hierarchy (E), Scoped Boundaries (S)

---

## Prompts (`.prompt.md`)

**Purpose:** Reusable task templates invoked on demand.

**Key feature:** Complete workflow with phases and validation gates.

```markdown
---
description: "Feature implementation from spec"
---
# Implement Feature

## Phase 1: Planning
1. Review [spec](${specFile})
2. Present approach and **seek approval**

## Phase 2: Implementation
3. Write code following [guidelines](./code.instructions.md)
4. Create tests with 80%+ coverage

## Phase 3: Review
5. Run tests, report results
6. Create PR with summary
```

**PROSE alignment:** Reduced Scope (R), Orchestrated Composition (O)

---

## Agents (`.agent.md`, `.chatmode.md`)

**Purpose:** Role-based personas with bounded capabilities.

**Key feature:** Tool restrictions define what agent can/cannot do.

```yaml
---
description: "Backend specialist with security focus"
tools: ['file_read', 'file_write', 'run_tests', 'search']
# Note: no deploy tools
---
```

```markdown
You are a backend development specialist.

## Expertise
- API design, database optimization, auth systems

## Boundaries
- CAN: Modify backend code, run tests
- CANNOT: Modify frontend, deploy to production
```

**PROSE alignment:** Scoped Boundaries (S)

---

## Skills (`SKILL.md` + directory)

**Purpose:** Packaged capabilities for distribution and auto-discovery.

**Key feature:** Description triggers auto-summoning based on task relevance.

```yaml
---
name: form-builder
description: |
  Build accessible forms with React Hook Form + Zod.
  Use when creating forms, validation, or form components.
---
```

```markdown
# Form Builder

## Stack
React Hook Form + Zod + @hookform/resolvers

## Quick Start
[Contact form example](examples/contact-form.tsx)

## Patterns
See [validation patterns](references/validation.md)
```

**PROSE alignment:** Progressive Disclosure (P), Orchestrated Composition (O)

---

## Context (`.context.md`)

**Purpose:** Reference knowledge loaded on demand.

**Key feature:** Agent fetches when needed, doesn't preload.

```markdown
# API Security Standards

## Authentication
- Use JWT with short expiry (15min)
- Refresh tokens: HttpOnly cookies

## Authorization  
- RBAC with least privilege
- Validate at service layer, not just API gateway
```

**PROSE alignment:** Progressive Disclosure (P)

---

## Memory (`.memory.md`)

**Purpose:** Decisions and learnings that persist across sessions.

**Key feature:** Updated after significant decisions; consulted before similar work.

```markdown
# Project Decisions

## 2026-01-15: Auth Architecture
**Decision:** JWT + refresh tokens over sessions
**Rationale:** Stateless scaling, mobile support
**Trade-off:** More complex token management

## 2026-01-20: Database Choice
**Decision:** PostgreSQL over MongoDB
**Rationale:** Relational data, ACID requirements
```

**PROSE alignment:** Progressive Disclosure (P), context must be explicit (Grounding Principle #2)

---

## Composition Pattern

Primitives work together:

```
User request
    ↓
.agent.md (bounded persona)
    ↓ loads
.instructions.md (domain rules via applyTo)
    ↓ executes
.prompt.md (workflow with phases)
    ↓ references
.context.md / .memory.md (on-demand knowledge)
    ↓ produces
Implementation + updated .memory.md
```

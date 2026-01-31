# Architecture Patterns

Common primitive structures for AI-native applications. Select based on task complexity.

## Pattern Selection

| Complexity | Pattern | When to Use |
|------------|---------|-------------|
| Simple | Single Agent | One role, one domain, clear boundaries |
| Medium | Agent + Prompts | Multiple workflows, same domain |
| High | Multi-Agent + Handoffs | Cross-domain, requires role separation |
| Project-wide | Full Primitive Stack | Legacy brownfield, large team, many domains |

---

## Pattern 1: Single Agent

**Use when:** Task is focused, single domain, clear inputs/outputs.

**Example:** "An agent to review PRs for security issues"

```
.github/agents/
└── security-reviewer.agent.md
```

**Template:**
```markdown
---
name: Security Reviewer
description: Reviews code changes for security vulnerabilities
tools: ['search', 'read', 'githubRepo']
---
# Security Reviewer

You review pull requests for security vulnerabilities.

## Focus Areas
- Injection risks (SQL, XSS, command injection)
- Authentication/authorization flaws
- Secrets exposure
- Dependency vulnerabilities

## Process
1. Read the PR diff
2. Identify security-relevant changes
3. Flag issues with severity and remediation
4. Summarize findings

## Boundaries
- CAN: Read code, search codebase, access PR metadata
- CANNOT: Modify code, approve/merge PRs
- APPROVAL REQUIRED: None (advisory only)
```

---

## Pattern 2: Agent + Prompts

**Use when:** Same agent handles multiple distinct workflows.

**Example:** "A backend developer that can implement features, fix bugs, and refactor"

```
.github/
├── agents/
│   └── backend-dev.agent.md
└── prompts/
    ├── implement-feature.prompt.md
    ├── fix-bug.prompt.md
    └── refactor.prompt.md
```

**Agent Template:**
```markdown
---
name: Backend Developer
description: Backend development specialist
tools: ['search', 'read', 'write', 'terminal']
---
# Backend Developer

You are a backend development specialist.

## Expertise
- Python/FastAPI, PostgreSQL, Redis
- REST API design, database optimization

## Boundaries
- CAN: Modify backend code, run tests, access database schemas
- CANNOT: Modify frontend, deploy to production
```

**Prompt Template (implement-feature.prompt.md):**
```markdown
---
description: Implement a new backend feature
agent: backend-dev
---
# Implement Feature

## Phase 1: Understand
1. Review the feature requirements: ${requirements}
2. Identify affected modules and dependencies
3. **Checkpoint:** Present implementation plan, seek approval

## Phase 2: Implement
4. Create/modify necessary files
5. Add unit tests (minimum 80% coverage for new code)
6. Run test suite

## Phase 3: Finalize
7. Update API documentation if endpoints changed
8. Create summary of changes
```

---

## Pattern 3: Multi-Agent + Handoffs

**Use when:** Task requires different expertise/toolsets at different phases.

**Example:** "Plan a feature, implement it, then review it"

```
.github/agents/
├── planner.agent.md       # Read-only, designs approach
├── implementer.agent.md   # Full edit access
└── reviewer.agent.md      # Read-only, critiques result
```

**Key: Define handoffs in frontmatter:**

```yaml
# planner.agent.md frontmatter
---
name: Planner
description: Creates implementation plans
tools: ['search', 'read', 'fetch']
handoffs:
  - label: Start Implementation
    agent: implementer
    prompt: Implement the plan above.
    send: false
---
```

```yaml
# implementer.agent.md frontmatter
---
name: Implementer
description: Implements features from plans
tools: ['search', 'read', 'write', 'terminal']
handoffs:
  - label: Request Review
    agent: reviewer
    prompt: Review the implementation above.
    send: false
---
```

**Flow:**
```
User → Planner → [handoff button] → Implementer → [handoff button] → Reviewer
```

---

## Pattern 4: Full Primitive Stack

**Use when:** Large project, multiple domains, team-wide standards.

**Example:** "Make this enterprise monorepo AI-native"

```
project/
├── AGENTS.md                           # Project-wide principles
├── .github/
│   ├── agents/
│   │   ├── planner.agent.md
│   │   └── implementer.agent.md
│   ├── instructions/
│   │   ├── code-style.instructions.md      # applyTo: "**/*.{ts,py}"
│   │   ├── frontend.instructions.md        # applyTo: "apps/web/**"
│   │   └── backend.instructions.md         # applyTo: "services/**"
│   ├── prompts/
│   │   ├── implement-feature.prompt.md
│   │   └── fix-incident.prompt.md
│   └── skills/
│       └── domain-expertise/
│           └── SKILL.md
├── services/
│   ├── AGENTS.md                       # Backend-specific rules (inherits root)
│   └── api/
│       └── AGENTS.md                   # API-specific rules (inherits services/)
└── apps/
    └── web/
        └── AGENTS.md                   # Frontend-specific rules
```

**Root AGENTS.md Template:**
```markdown
# Project Principles

## Code Standards
- All code must have tests
- Follow conventional commits
- No secrets in code

## AI Agent Guidelines
- Always run tests before completing implementation
- Seek approval before:
  - Database migrations
  - API breaking changes
  - Dependency updates

## Domain Structure
- `services/` - Backend services (Python/FastAPI)
- `apps/web/` - Frontend application (React/TypeScript)
- `packages/` - Shared libraries
```

---

## Pattern 5: Skill-Based Capability

**Use when:** Capability should be reusable, auto-discoverable, portable across projects.

**Example:** "Help agents build forms with React Hook Form + Zod"

```
.github/skills/
└── form-builder/
    ├── SKILL.md
    ├── examples/
    │   ├── contact-form.tsx
    │   └── login-form.tsx
    └── references/
        └── validation-patterns.md
```

**SKILL.md Template:**
```markdown
---
name: form-builder
description: |
  Build accessible forms with React Hook Form + Zod validation.
  Use when creating forms, form validation, or form components.
---

# Form Builder

## Quick Start
See [contact form example](examples/contact-form.tsx) for standard pattern.

## Process
1. Define Zod schema for validation
2. Create form component with useForm hook
3. Add accessible labels and error messages
4. Test with React Testing Library

## Patterns
- [Validation patterns](references/validation-patterns.md)
- [Async validation](examples/async-validation.tsx)

## Boundaries
- CAN: Generate form components, validation schemas, tests
- CANNOT: Modify API endpoints, database schemas
```

---

## Composition Guidelines

When combining patterns:

1. **Start minimal** — Don't create primitives you don't need yet
2. **Add as complexity grows** — Single agent → add prompts → add more agents
3. **Separate concerns** — Each primitive should have one clear purpose
4. **Design handoffs explicitly** — Don't assume agents will coordinate implicitly
5. **Use instructions for rules, prompts for workflows** — Rules are persistent; workflows are invoked

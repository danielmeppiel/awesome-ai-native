---
layout: docs
title: "Getting Started"
display_title: "Getting Started"
permalink: /docs/getting-started/
nav_order: 2
---

> 📖 **Deep dive in the handbook:** [Chapter 11 — The Instrumented Codebase →](https://danielmeppiel.github.io/agentic-sdlc-handbook/handbook/ch11-the-instrumented-codebase.html)
> This page is the practical, Copilot-focused walkthrough. The handbook gives you the *why* behind the seven primitive types — load mechanics, composition, and the deterministic / probabilistic boundary.

> 🧭 **New to this?** Start with [**The Practice →**](../concepts/) for the 10-minute operating model — three disciplines, one shareable mental map. Then come back here to ship your first primitive.

> **PROSE Focus:** This section is hands-on **P**rompts and **S**kills—building your first primitives.

Now that you understand the [PROSE Specification](https://danielmeppiel.github.io/agentic-sdlc-handbook/handbook/ch12-the-prose-specification.html), it's time to build your AI Native Development environment. This hands-on implementation will give you immediate productivity improvements while establishing the foundation for more advanced workflows.

The setup follows a logical progression: start by installing Skills that provide instant capabilities, then add local instructions for project-specific guidance, configure custom agents for safe boundaries, build reusable prompts for common tasks, and create specification templates that bridge planning to implementation.

## Start with Skills

Before creating custom primitives, leverage the **[Agent Skills](https://agentskills.io)** ecosystem. Skills are pre-packaged capabilities that agents auto-discover and summon based on task relevance—giving you instant productivity without configuration.

**✅ Quick Actions:**
- Install [APM (Agent Package Manager)](https://github.com/danielmeppiel/apm) if you haven't already. Read more at [Tooling](../tooling/).
- Browse [community Skills](https://github.com/github/awesome-copilot/tree/main/skills) for your tech stack
- Install relevant Skills: `apm install awesome-copilot/skill/<skill-name>`

> 💡 **Progressive Context Disclosure**: Once installed, you don't need to explicitly invoke Skills. Agents automatically scan available Skills and load only what's relevant to your current task—reducing context pollution and improving response quality.

**⚠️ Checkpoint:** Skills installed and compiled—agents now have access to packaged capabilities

---

With Skills providing your baseline capabilities, you'll want to add project-specific guidance that doesn't belong in a distributed Skill. This is where local primitives come in.

## Instructions Architecture

Instructions form the bedrock of reliable AI behavior: they're the persistent rules that guide the Agent without cluttering your immediate context. Rather than repeating the same guidance in every conversation, instructions embed your team's knowledge directly into the AI's reasoning process.

The key insight is modularity: instead of one massive instruction file that applies everywhere, you create targeted files that activate only when working with specific technologies or file types. This context engineering approach keeps your AI focused and your guidance relevant.

**✅ Quick Actions:**
- Create the general [`copilot-instructions.md`](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilot-instructionsmd-file) file in the `.github` folder for the repository with common rules
- Create modular [`.instructions.md` files](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-instructionsmd-files) in the `.github/instructions/` folder by domain (frontend, backend, testing, docs, specs...)
- Use [`applyTo: "**/*.{js,ts...}"`](https://code.visualstudio.com/docs/copilot/copilot-customization#_instructions-file-structure) patterns for selective application
- Compile to [AGENTS.md standard](https://agents.md) so your context works across all coding agents. See [Tooling](../tooling/) to learn about **context compilation**

> 💡 **Context Engineering in Action**: Modular instructions preserve context space by loading only relevant guidelines when working on specific file types, leaving maximum buffer for code understanding.

### 🔧 Tools & Files:
```
.github/
├── copilot-instructions.md          # Global repository rules
└── instructions/
    ├── frontend.instructions.md     # applyTo: "**/*.{jsx,tsx,css}"
    ├── backend.instructions.md      # applyTo: "**/*.{py,go,java}"
    └── testing.instructions.md      # applyTo: "**/test/**"

# After context compilation:
# Nested AGENTS.md files auto-generated in optimal locations
```

### Example: Markdown Prompt Engineering in Instructions
Create your `.github/instructions/frontend.instructions.md` file:

```markdown
---
applyTo: "**/*.{ts,tsx}"
description: "TypeScript development guidelines with context engineering"
---
# TypeScript Development Guidelines

## Context Loading
Review [project conventions](../docs/conventions.md) and 
[type definitions](../types/index.ts) before starting.

## Deterministic Requirements
- Use strict TypeScript configuration
- Implement error boundaries for React components
- Apply ESLint TypeScript rules consistently

## Structured Output
Generate code with:
- [ ] JSDoc comments for all public APIs
- [ ] Unit tests in `__tests__/` directory
- [ ] Type exports in appropriate index files
```

**⚠️ Checkpoint:** Instructions are modular, targeted, and ready to compile

## Custom Agents Configuration

With your instruction architecture in place, you need a way to enforce domain boundaries and prevent AI agents from overstepping their expertise. Custom Agents (`.agent.md` files) solve this by creating professional boundaries similar to real-world licensing—architects plan but don't build, engineers execute but don't set strategy.

> 📖 **Deep dive in the handbook:** [Chapter 11 §Agents →](https://danielmeppiel.github.io/agentic-sdlc-handbook/handbook/ch11-the-instrumented-codebase.html) explains the persona-lens model. Custom Agents replaced the legacy `.chatmode.md` files. For composition with Skills, see [Chapter 21 →](https://danielmeppiel.github.io/agentic-sdlc-handbook/handbook/ch21-the-reference-architecture-earned.html).

**✅ Quick Actions:**
- Define domain-specific [Custom Agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents) with MCP tool boundaries
- Encapsulate tech stack knowledge and guidelines per agent
- Define the most appropriate [LLM model](https://code.visualstudio.com/docs/copilot/customization/custom-agents#_custom-agent-example) per agent like `Claude Sonnet 4`
- Configure secure [MCP tool access](https://code.visualstudio.com/docs/copilot/customization/custom-agents#_custom-agent-example) to prevent cross-domain security breaches

> 💡 **Security Through MCP Tool Boundaries**: Each Custom Agent receives only the specific MCP tools needed for their domain - preventing dangerous access escalation and cross-contamination. Like professional licensing, a planning agent can't execute destructive commands, and a frontend agent can't access backend databases.

### 🔧 Tools & Files:
```
.github/
└── agents/
    ├── architect.agent.md             # Planning specialist - designs, cannot execute
    ├── frontend-engineer.agent.md     # UI specialist - builds interfaces, no backend access
    ├── backend-engineer.agent.md      # API specialist - builds services, no UI modification
    └── technical-writer.agent.md      # Documentation specialist - writes docs, cannot run code
```

### Example: MCP Tool Boundary Implementation
Create your `.github/agents/backend-engineer.agent.md` file:

```yaml
---
description: 'Backend development specialist with security focus'
tools: ['changes', 'codebase', 'editFiles', 'runCommands', 'runTasks', 
        'search', 'problems', 'testFailure', 'terminalLastCommand']
model: Claude Sonnet 4
---

You are a backend development specialist focused on secure API development, database design, and server-side architecture. You prioritize security-first design patterns and comprehensive testing strategies.

## Domain Expertise
- RESTful API design and implementation
- Database schema design and optimization  
- Authentication and authorization systems
- Server security and performance optimization

You master the backend of this project thanks to you having read all [the backend docs](../../docs/backend).

## Tool Boundaries
- **CAN**: Modify backend code, run server commands, execute tests
- **CANNOT**: Modify client-side assets
```

### Security & Professional Boundaries:
- **Architect agent**: Research tools only - **cannot execute destructive commands or modify production code**
- **Frontend Engineer agent**: UI development tools only - **cannot access databases or backend services**
- **Backend Engineer agent**: API and database tools only - **cannot modify user interfaces or frontend assets**
- **Technical Writer agent**: Documentation tools only - **cannot run code, deploy, or access sensitive systems**

*Like real-world professional licenses, each Custom Agent operates within its area of competence and cannot overstep into dangerous territory.*

**⚠️ Checkpoint:** Each Custom Agent has clear boundaries and tool restrictions

## Agentic Workflows

Custom Agents create the safety boundaries, but you still need efficient ways to execute complete development processes. **Agentic Workflows** are implemented as reusable `.prompt.md` files that orchestrate all your primitives into systematic, end-to-end processes.

**✅ Quick Actions:**
- Create [`.prompt.md` files](https://code.visualstudio.com/docs/copilot/customization/prompt-files) for complete development processes
- Build in mandatory human validation points
- Design workflows for both local execution and async delegation

> 💡 **Agentic Workflows**: These `.prompt.md` files are your complete systematic processes that combine all primitives (instructions, modes, specs, context) into repeatable workflows that can be executed locally or delegated to async agents.

### 🔧 Tools & Files:
```
.github/prompts/
├── code-review.prompt.md           # With validation checkpoints
├── feature-spec.prompt.md          # Spec-first methodology
└── async-implementation.prompt.md  # GitHub Coding Agent delegation
```

### Example: Complete Agentic Workflow
Create your `.github/prompts/feature-spec.prompt.md` file:

```markdown
---
mode: agent
model: gpt-4
tools: ['file-search', 'semantic-search', 'github']
description: 'Feature implementation workflow with validation gates'
---
# Feature Implementation from Specification

## Context Loading Phase
1. Review [project specification](${specFile})
2. Analyze [existing codebase patterns](./src/patterns/)
3. Check [API documentation](./docs/api.md)

## Deterministic Execution
Use semantic search to find similar implementations
Use file search to locate test patterns: `**/*.test.{js,ts}`

## Structured Output Requirements
Create implementation with:
- [ ] Feature code in appropriate module
- [ ] Comprehensive unit tests (>90% coverage)
- [ ] Integration tests for API endpoints
- [ ] Documentation updates

## Human Validation Gate
🚨 **STOP**: Review implementation plan before proceeding to code generation.
Confirm: Architecture alignment, test strategy, and breaking change impact.
```

**⚠️ Checkpoint:** Prompts include explicit validation gates

## Specification Templates

The final piece of your foundation addresses the gap between planning and implementation. Specification templates transform high-level ideas into implementation-ready blueprints that work consistently whether executed by humans or AI agents.

These `.spec.md` templates are the foundation of **spec-driven team workflows**. When you scale to team contexts (see [Team & Enterprise Scale](../team-adoption/)), product owners use these templates during sprint planning to create explicit, agent-executable specifications. [Spec-Kit](https://github.com/github/spec-kit) provides `/speckit.specify` commands that generate these files following the constitution → specify → plan → tasks → implement pattern, but understanding the underlying template structure gives you flexibility to customize for your team's needs.

**✅ Quick Actions:**
- Create standardized [`.spec.md` templates](https://docs.github.com/en/copilot/copilot-chat/copilot-chat-cookbook) for feature specifications
- Build implementation-ready blueprints with validation criteria
- Design for deterministic handoff between planning and execution phases

> 💡 **Bridge Primitive**: Specification files transform planning-phase thinking into implementation-ready artifacts that work reliably across different executors (human or AI).

### 🔧 Tools & Files:
```
.github/specs/
├── feature-template.spec.md        # Standard feature specification template
├── api-endpoint.spec.md           # API-specific specification template
└── component.spec.md              # UI component specification template
```

### Example: Implementation-Ready Specification

Create a `.github/specs/jwt-auth.spec.md` file:

```markdown
# Feature: User Authentication System

## Problem Statement
Users need secure access to the application with JWT-based authentication.

## Approach
Implement middleware-based authentication with token validation and refresh capabilities.

## Implementation Requirements
### Core Components
- [ ] JWT middleware (`src/middleware/auth.ts`)
- [ ] Token service (`src/services/token.ts`)
- [ ] User validation (`src/services/user.ts`)

### API Contracts
- `POST /auth/login` - Returns JWT token
- `POST /auth/refresh` - Refreshes expired token
- `GET /auth/verify` - Validates current token

### Validation Criteria
- [ ] Handles malformed tokens with 401 status
- [ ] Token expiration properly managed
- [ ] Refresh token rotation implemented
- [ ] Unit tests >90% coverage
- [ ] Integration tests for all endpoints

## Handoff Checklist
- [ ] Architecture approved by team lead
- [ ] Database schema finalized
- [ ] Security review completed
- [ ] Implementation ready for assignment
```

**⚠️ Checkpoint:** Specifications are implementation-ready before delegation

---

## Create Your First Skill

Once you've developed useful patterns—instructions, prompts, or workflows that could benefit other projects—it's time to package them as a **Skill** for distribution and reuse.

Skills have one key file:
- **SKILL.md** (required): Tells agents *what* this Skill does and *when* to use it

**✅ Quick Actions:**
- Identify a reusable agent capability from your project
- Create a Skill package by creating a folder with the skill name under `.github/skills`
- Write the SKILL.md discovery file inside it
- Test locally, then push to GitHub for sharing

### Example: SKILL.md for Agent Discovery

```markdown
---
name: form-builder
description: Build accessible forms with React Hook Form + Zod. Activate when user asks to create any form with thesse frameworks.
---
# Form Builder

Build accessible, type-safe forms in React.

## Stack

- **React Hook Form** — form state, minimal re-renders
- **Zod** — schema validation
- **@hookform/resolvers** — connects them

## Examples

- [Contact form](examples/contact-form.tsx) — full implementation
- [Newsletter signup](examples/newsletter-signup.tsx) — minimal implementation

## Install

npm install react-hook-form @hookform/resolvers zod
```

**⚠️ Checkpoint:** Your patterns are now packaged and shareable with the community

---

## Quick Start Checklist

With Skills and primitives in place, you now have a complete foundation for systematic AI development. The checklist below walks through the implementation sequence.

### Conceptual Foundation
1. **[ ]** Understand **Markdown Prompt Engineering** principles (semantic structure + precision + tools)
2. **[ ]** Grasp **Context Engineering** fundamentals (context window optimization + session strategy)
3. **[ ]** Understand **Skills vs Primitives** (Skills distribute; primitives are internal or local)

### Skills Setup
4. **[ ]** Install [APM](https://github.com/danielmeppiel/apm) for Skills management
5. **[ ]** Install relevant Skills for your tech stack: `apm install owner/skill-name`

### Local Primitives
6. **[ ]** Create [`.github/copilot-instructions.md`](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilot-instructionsmd-file) with project-specific guidelines
7. **[ ]** Set up domain-specific [`.instructions.md` files](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-instructionsmd-files) with `applyTo` patterns
8. **[ ]** Configure [custom agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents) for your tech stack domains
9. **[ ]** Create your first [`.prompt.md` Agentic Workflow](https://code.visualstudio.com/docs/copilot/copilot-customization#_prompt-files-experimental)
10. **[ ]** Build your first `.spec.md` template for feature specifications

### Scale & Share
11. **[ ]** Package reusable patterns as Skills: `apm init skill`
12. **[ ]** Practice spec-first workflow with session splitting

## What's Next?

**Foundation Complete?** You've installed Skills and built local primitives. Continue to [Tooling](../tooling/) to understand the infrastructure that makes these scale—context compilation, Skills composition, and the package management that enables everything that follows.

> 🎯 **Now share *why* this works with your team.** You've shipped your first primitive — that's the hardest part. The piece that turns one engineer's setup into a team standard is **[The Practice →](../concepts/)**: the short, repostable operating model your lead can socialise in Slack, architecture reviews, and onboarding docs. It's the page customers used to mandate this approach across their engineering orgs.

**Ready to jump ahead?** After Tooling, [Agent Delegation](../agent-delegation/) covers execution strategies, and [Team & Enterprise Scale (Handbook Part II)](https://danielmeppiel.github.io/agentic-sdlc-handbook/handbook/ch05-governance-for-ai-assisted-delivery.html) covers governance and organisational rollout.

*You now have Skills installed, local primitives configured, and understand how to package agent capabilities for reuse. The next step is understanding the infrastructure that makes these primitives executable, shareable, and production-ready.*

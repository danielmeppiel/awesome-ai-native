---
layout: docs
title: "Getting Started"
display_title: "Getting Started: Foundation Setup"
permalink: /docs/getting-started/
nav_order: 3
---

Build your first Agent Primitives and experience immediate productivity improvements through systematic implementation of instructions, chat modes, prompts, and specifications.

## A. Instructions Architecture
**✅ Quick Actions:**
- Create the general [`copilot-instructions.md`](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilot-instructionsmd-file) file in the `.github` folder for the repository with common rules
- Create modular [`.instructions.md` files](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-instructionsmd-files) in the `.github/instructions/` folder by domain (frontend, backend, testing, docs, specs...)
- Use [`applyTo: "**/*.{js,ts...}"`](https://code.visualstudio.com/docs/copilot/copilot-customization#_instructions-file-structure) patterns for selective application

> 💡 **Context Engineering in Action**: Modular instructions preserve context space by loading only relevant guidelines when working on specific file types, leaving maximum buffer for code understanding.

### 🔧 Tools & Files:
```
.github/
├── copilot-instructions.md          # Global repository rules
└── instructions/
    ├── frontend.instructions.md     # applyTo: "**/*.{jsx,tsx,css}"
    ├── backend.instructions.md      # applyTo: "**/*.{py,go,java}"
    └── testing.instructions.md      # applyTo: "**/test/**"
```

### Example: Markdown Prompt Engineering in Instructions
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

**⚠️ Checkpoint:** Instructions are context-efficient and non-conflicting

## B. Chat Modes Configuration
**✅ Quick Actions:**
- Define domain-specific [custom chat modes](https://code.visualstudio.com/docs/copilot/chat/chat-modes) with MCP tool boundaries
- Encapsulate tech stack knowledge and guidelines per mode
- Define the most appropriate [LLM model](https://code.visualstudio.com/docs/copilot/chat/chat-modes#_chat-mode-file-example) for your chat mode like `Claude Sonnet 4`
- Configure secure [MCP tool access](https://code.visualstudio.com/docs/copilot/chat/chat-modes#_chat-mode-file-example) to prevent cross-domain security breaches

> 💡 **Security Through MCP Tool Boundaries**: Each chat mode receives only the specific MCP tools needed for their domain - preventing dangerous access escalation and cross-contamination. Like professional licensing, a planning mode can't execute destructive commands, and a frontend mode can't access backend databases.

### 🔧 Tools & Files:
```
.github/
└── chatmodes/
    ├── architect.chatmode.md             # Planning specialist - designs, cannot execute
    ├── frontend-engineer.chatmode.md     # UI specialist - builds interfaces, no backend access
    ├── backend-engineer.chatmode.md      # API specialist - builds services, no UI modification
    └── technical-writer.chatmode.md      # Documentation specialist - writes docs, cannot run code
```

### Example: MCP Tool Boundary Implementation
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
- **Architect mode**: Research tools only - **cannot execute destructive commands or modify production code**
- **Frontend Engineer mode**: UI development tools only - **cannot access databases or backend services** 
- **Backend Engineer mode**: API and database tools only - **cannot modify user interfaces or frontend assets**
- **Technical Writer mode**: Documentation tools only - **cannot run code, deploy, or access sensitive systems**

*Like real-world professional licenses, each mode operates within its area of competence and cannot overstep into dangerous territory.*

**⚠️ Checkpoint:** Each mode has clear boundaries and tool restrictions

## C. Reusable Prompt Library
**✅ Quick Actions:**
- Create [`.prompt.md` files](https://code.visualstudio.com/docs/copilot/copilot-customization#_prompt-files-experimental) for recurring tasks
- Build in mandatory human validation points
- Design for multi-task delegation patterns

> 💡 **Markdown Prompt Engineering**: Prompt files are context-efficient templates that combine semantic structure, tool delegation, and validation checkpoints for statistical repeatability.

### 🔧 Tools & Files:
```
.github/prompts/
├── code-review.prompt.md           # With validation checkpoints
├── feature-spec.prompt.md          # Spec-first methodology
└── async-implementation.prompt.md  # GitHub Coding Agent delegation
```

### Example: Advanced Prompt Engineering Pattern
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

## D. Specification Templates
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

## Quick Start Checklist

### Conceptual Foundation
1. **[ ]** Understand **Markdown Prompt Engineering** principles (semantic structure + precision + tools)
2. **[ ]** Grasp **Context Engineering** fundamentals (buffer optimization + session strategy)

### Implementation Steps
3. **[ ]** Create [`.github/copilot-instructions.md`](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilot-instructionsmd-file) with basic project guidelines (Context Engineering: global rules)
4. **[ ]** Set up domain-specific [`.instructions.md` files](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-instructionsmd-files) with `applyTo` patterns (Context Engineering: selective loading)
5. **[ ]** Configure [chat modes](https://code.visualstudio.com/docs/copilot/copilot-customization#_custom-chat-modes) for your tech stack domains (Context Engineering: domain boundaries)
6. **[ ]** Create first [`.prompt.md` file](https://code.visualstudio.com/docs/copilot/copilot-customization#_prompt-files-experimental) with validation checkpoints (Markdown Prompt Engineering: deterministic templates)
7. **[ ]** Build your first `.spec.md` template for feature specifications (Agent Primitive: deterministic planning-to-implementation bridge)
8. **[ ]** Practice spec-first workflow: plan first, implement second (Context Engineering: session splitting)

## What's Next?

**Foundation Complete?** Advance to [Workflow Orchestration](../workflows/) to see these primitives in action with complete OAuth implementation example.

**Want to understand the theory better?** Return to [Core Concepts](../concepts/) for deeper theoretical understanding.

**Ready for team implementation?** Jump to [Team Adoption](../team-adoption/) for scaling strategies.

*You now have the foundation tools for consistent, reliable AI interactions. The next step is learning to orchestrate them into complete workflows.*

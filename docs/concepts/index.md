---
layout: docs
title: "Concepts"
display_title: "Core Concepts"
permalink: /docs/concepts/
nav_order: 2
---

Most developers start with AI by throwing simple prompts at GitHub Copilot and hoping for the best. This approach works for simple tasks but breaks down when you need reliable, repeatable results for complex development work.

**The PROSE Framework** transforms this ad-hoc experimentation into systematic engineering practices:

| | Component | What It Means |
|---|-----------|---------------|
| **P** | **Prompts** | Structured natural language that guides AI behavior |
| **R** | **Reliability** | Deterministic outcomes through context engineering |
| **O** | **Orchestration** | Multi-agent delegation and task decomposition |
| **S** | **Skills** | Capability packages that onboard agents into projects |
| **E** | **Engineering** | A new discipline—systematic AI-native development |

Let's explore each component in depth.

---

## P — Prompts: Markdown Prompt Engineering

**The Foundation:** Transform natural language into structured, repeatable instructions using Markdown's semantic power.

**Why This Works:** Markdown's structure (headers, lists, links) naturally guides AI reasoning, making outputs more predictable and consistent.

### Key Techniques

- **Context Loading**: `[Review existing patterns](./src/patterns/)` — Links become context injection points that pull in relevant information from files or websites
- **Structured Thinking**: Headers and bullets create clear reasoning pathways for the AI to follow
- **Role Activation**: "You are an expert [role]" — Triggers specialized knowledge domains and focuses responses
- **Tool Integration**: *Use MCP tool `tool-name`* — Connects to deterministic code execution from MCP servers
- **Precision Language**: Eliminate ambiguity through specific, unambiguous instructions
- **Validation Gates**: "Stop and get user approval" — Human oversight at critical decision points

### Quick Win Example

Instead of: `Find and fix the bug`, use:

```markdown
You are an expert debugger, specialized in debugging complex programming issues. 

You are particularly great at debugging this project, which architecture and quirks can be consulted in the [architecture document](./docs/architecture.md). 

Follow these steps:

1. Review the [error logs](./logs/error.log) and identify the root cause. 

2. Use the `azmcp-monitor-log-query` MCP tool to retrieve infrastructure logs from Azure.  

3. Once you find the root cause, think about 3 potential solutions with trade-offs

4. Present your root cause analysis and suggested solutions with trade-offs to the user and seek validation before proceeding with fixes - do not change any files.
```

Once you've mastered structured prompting, you'll quickly realize that manually crafting perfect prompts doesn't guarantee consistent results. This is where Reliability comes in.

---

## R — Reliability: The Goal Everything Serves

**The Outcome:** Reliability isn't a technique you apply—it's the result of applying all other PROSE components systematically.

Why do AI interactions fail? Three root causes:

1. **Ambiguous prompts** → AI interprets differently each time
2. **Context overload** → AI loses focus in noise
3. **No validation** → Errors compound silently

The PROSE Framework addresses each through specific mechanisms:

### How Each Component Delivers Reliability

| Problem | PROSE Solution | Mechanism |
|---------|----------------|-----------|
| Ambiguous prompts | **P**rompts | Markdown Prompt Engineering with precision language |
| Context overload | **E**ngineering | Strategic context management, progressive disclosure |
| AI Complexity | **S**kills | OSS and Private packaged agent capabilities benefiting from added validation and maintenance |
| Inconsistent execution | **O**rchestration | Splitting tasks into smaller chunks, coordinating agent flows and subagents |

**The key insight:** You don't "do reliability" as a separate step. You achieve reliability by mastering Prompts, Orchestration, Skills, and Engineering together.

---

## O — Orchestration: Multi-Agent Coordination

**The Coordination Layer:** Orchestration is how you coordinate multiple agents, decompose complex tasks, and delegate work—whether to local IDE agents or async GitHub Coding Agents.

### Agentic Workflows

**Agentic Workflows** are implemented as `.prompt.md` and `.agent.md` files that coordinate multiple primitives into unified processes:

```markdown
# Feature Implementation Workflow

## Phase 1: Planning
1. Review the [requirements spec](./specs/feature.spec.md)
2. Analyze existing [architecture patterns](./docs/architecture.md)
3. Present implementation plan and **seek user approval before proceeding**

## Phase 2: Implementation  
4. Generate code following [coding standards](./.github/instructions/code.instructions.md) and using one `runSubagent` per task
5. Create unit tests with minimum 80% coverage
6. **Checkpoint: Run tests and report results**

## Phase 3: Integration
7. Update [memory file](./.memory.md) with decisions made
8. Create pull request with summary
```

### Key Characteristics

- **Task Decomposition**: Break complex work into phases with clear handoffs
- **Execution Flexibility**: Same workflow works locally or delegated to async agents
- **Self-Improving**: Include learning mechanisms that update primitives based on outcomes
- **Validation Checkpoints**: Human approval gates at critical decision points

### Delegation Patterns

| Pattern | Use Case | How It Works |
|---------|----------|--------------|
| **Local Orchestration** | Interactive development | Run `.prompt.md` in IDE, human approves at gates |
| **Async Delegation** | Background tasks | Assign to GitHub Coding Agent, review PR when complete |
| **Multi-Agent Split** | Complex features | Different agents handle planning, implementation, testing |

Orchestration coordinates the work. But where do the reusable components come from? That's Skills.

---

## S — Skills: Agent Primitives & Packages

**The Building Blocks:** Skills are auto-discoverable, executable capability packages that *onboard* agents into projects—just like you onboard developers.

When a new developer joins your team, you don't explain everything from scratch. You point them to documentation, coding standards, and established patterns. **Skills do the same for AI agents**: they package the knowledge, guardrails, and workflows that make an agent productive in your specific context.

### What Skills Contain

**[Agent Skills](https://agentskills.io)** package primitives and any other resource into distributable units:

| Primitive | Purpose | File Pattern |
|-----------|---------|-------------|
| **Instructions** | Coding standards, guardrails | `.instructions.md` |
| **Agents** | Role-based personas with tool boundaries | `.agent.md` |
| **Workflows** | Reusable multi-step processes | `.prompt.md` |
| **Specifications** | Implementation blueprints | `.spec.md` |
| **Context** | Reference knowledge for tasks | `.context.md` |

Skills can also include scripts, templates, data files, examples—anything an agent might need.

### How Skills Work

1. **Discovery**: Each Skill has a `SKILL.md` that describes when it's relevant
2. **Auto-Summoning**: Agents scan available Skills and load only what matches the current task
3. **Execution**: The Skill's primitives guide the agent's behavior automatically

**No explicit `/command` needed.** When you ask an agent to "build a form," it automatically discovers and loads your `form-builder` Skill if installed.

### Key Properties

- **Auto-Discovery**: Agents find and load Skills based on task relevance
- **Composable**: Skills can depend on other Skills, creating capability stacks
- **Portable**: Same Skill works across Copilot, Claude, Cursor, and all major coding agents

> **VSCode Native**: VSCode supports Skills plus `.instructions.md`, `.prompt.md`, and `.agent.md` natively.

Skills give you the building blocks. But how do you manage the finite attention of the AI? That's Engineering.

---

## E — Engineering: Context Engineering

**The Discipline:** Context Engineering is the art of managing LLM attention—a finite, precious resource that determines whether your agent succeeds or fails.

> *"Context is the new RAM. Manage it or waste it."*

### The Attention Problem

LLMs have **finite memory** (context windows) and **limited attention**. When you overload them with irrelevant information:

- They lose focus on what matters
- They forget instructions given earlier
- They hallucinate to fill gaps
- They make inconsistent decisions

**Context Engineering** is the systematic practice of controlling what agents see, when they see it, and ensuring they focus only on what's relevant to the current task.

### Core Principles

| Principle | What It Means | Technique |
|-----------|---------------|-----------|  
| **Load only what's needed** | Don't dump everything into context | Progressive disclosure via markdown links |
| **Flush when stale** | Start fresh sessions for new phases | Session splitting (plan → implement → test) |
| **Scope to the task** | Different files need different rules | `applyTo` patterns in `.instructions.md` |
| **Hierarchical inheritance** | Local context overrides global | Nested `AGENTS.md` files |

### The AGENTS.md Standard

The **[AGENTS.md standard](https://agents.md)** emerged as the universal solution for modular agent instructions, adopted by 20,000+ open-source projects:

```
project/
├── AGENTS.md                    # Root: project-wide principles
├── frontend/
│   ├── AGENTS.md               # Frontend-specific context
│   └── Button.tsx              # Inherits: root + frontend
└── backend/
    ├── AGENTS.md               # Backend-specific context
    └── auth.ts                 # Inherits: root + backend
```

Agents walk up the directory tree and load the closest AGENTS.md file—domain-specific context without global pollution. 

### Key Techniques

- **Progressive Context Disclosure**: Use markdown links like `[detailed requirements](./specs/auth.md)` so agents fetch context only when needed
- **Session Splitting**: Fresh context for each development phase. Planning session → implementation session → testing session
- **Modular Instructions**: Author `.instructions.md` files with `applyTo` patterns for precision loading
- **Memory Files**: Use `.memory.md` to persist decisions across sessions without bloating active context
- **Context Helpers**: Use `.context.md` files as reference documents agents can consult on-demand

### The Payoff

- **Universal Portability**: Same context works across Copilot, Cursor, Claude, Codex
- **Automatic Optimization**: Agents load only what's relevant to the current file
- **Compound Intelligence**: Each primitive becomes a knowledge asset that improves with use

---

## Key Takeaways

1. **P — Prompts**: Markdown Prompt Engineering provides the structural foundation for predictable AI interactions
2. **R — Reliability**: The outcome all other components serve—achieved through systematic application of PROSE
3. **O — Orchestration**: Coordinate agents, decompose tasks, and delegate work through Agentic Workflows
4. **S — Skills**: Auto-discoverable packages that onboard agents into projects—like onboarding developers
5. **E — Engineering**: Context Engineering manages LLM attention—load only what's needed, flush when stale

**Ready for hands-on implementation?** Continue to [Getting Started](../getting-started/) to build your first Agent Primitives and culminate with your first Agentic Workflow.

**Want to understand the tooling ecosystem?** Jump to [Tooling](../tooling/) to learn about Agent CLI Runtimes, context compilation, and agent package management.

**Want to see complete workflow execution strategies?** Jump to [Agent Delegation](../agent-delegation/) for local and async orchestration patterns.

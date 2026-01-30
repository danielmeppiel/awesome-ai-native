---
name: prose-architect
description: Design PROSE-compliant AI-native code in Markdown. Use when (1) Writing prompts, instructions, or agent definitions (2) Designing multi-primitive AI systems from requirements (3) Decomposing mega-prompts into composable primitives (4) Auditing prompts/instructions for reliability issues. PROSE = Progressive Disclosure, Reduced Scope, Orchestrated Composition, Scoped Boundaries, Explicit Hierarchy
---

# PROSE Architect

Design AI-native Markdown artifacts that are reliable, scalable, and composable.

## Quick Compliance Check

Before writing, verify the artifact will satisfy:

| Constraint | Question |
|------------|----------|
| **P** Progressive Disclosure | Does context load just-in-time via links, not all upfront? |
| **R** Reduced Scope | Is scope sized for one concern? Can phases get fresh context? |
| **O** Orchestrated Composition | Are you composing small primitives, not building a mega-prompt? |
| **S** Scoped Boundaries | Are tools, knowledge scope, and approval gates explicit? |
| **E** Explicit Hierarchy | Do local rules inherit/override global rules appropriately? |

For constraint details: [constraints.md](references/constraints.md)

## Workflow: Single Prompt/Instruction

1. **Define boundaries first** — What can the agent do? What requires approval?
2. **Identify context needs** — What files/knowledge are required? Link them, don't inline.
3. **Structure into phases** — Break into steps. Add checkpoints where decisions need validation.
4. **Add validation gates** — "Present plan and seek approval before proceeding"
5. **Size appropriately** — One concern per artifact. If too large, decompose.

### Prompt Structure Pattern

```markdown
You are [role with domain focus].

## Context
Consult [relevant file](./path/to/file.md) for [specific purpose].

## Steps
1. [First phase with clear deliverable]
2. [Second phase]
3. **Checkpoint:** Present [output] and seek user approval before proceeding.
4. [Execution phase after approval]

## Boundaries
- CAN: [explicit capabilities]
- CANNOT: [explicit restrictions]
- APPROVAL REQUIRED: [what needs human sign-off]
```

## Workflow: Multi-Primitive System

When designing a system with multiple coordinated primitives:

1. **Decompose the behavior** — What distinct concerns exist?
2. **Map to primitive types** — See [primitives.md](references/primitives.md)
3. **Design the hierarchy** — What's project-wide vs. domain-specific?
4. **Plan composition** — How do primitives chain together?
5. **Define handoff points** — Where does one primitive's scope end?

### System Architecture Pattern

```
project/
├── AGENTS.md                      # Project-wide principles
├── .github/
│   ├── instructions/
│   │   ├── frontend.instructions.md   # applyTo: "**/*.tsx"
│   │   └── backend.instructions.md    # applyTo: "**/*.py"
│   ├── prompts/
│   │   └── feature-workflow.prompt.md # Orchestrates the flow
│   └── chatmodes/
│       └── architect.chatmode.md      # Planning, no execution tools
└── domain/
    └── AGENTS.md                  # Domain-specific rules (inherits root)
```

## Primitive Selection

| Need | Primitive | Key Property |
|------|-----------|--------------|
| Persistent rules | `.instructions.md` | `applyTo` pattern scoping |
| Reusable workflow | `.prompt.md` | Invokable task template |
| Bounded persona | `.agent.md` | Tool restrictions + role |
| Distributable capability | `SKILL.md` | Auto-discovery, portable |
| Reference knowledge | `.context.md` | On-demand loading |
| Session memory | `.memory.md` | Persists across sessions |

Full guide: [primitives.md](references/primitives.md)

## Anti-Pattern Detection

When reviewing existing artifacts, watch for:

| Symptom | Violation | Fix |
|---------|-----------|-----|
| 500+ line prompt | Orchestrated Composition | Decompose into primitives |
| All docs loaded upfront | Progressive Disclosure | Use links for just-in-time loading |
| No validation gates | Scoped Boundaries | Add checkpoints before destructive actions |
| Same rules everywhere | Explicit Hierarchy | Use `applyTo` patterns + nested AGENTS.md |
| "Do everything" agent | Reduced Scope | Split into phased workflow or multiple agents |

## Key Mechanisms

**Progressive Disclosure:**
```markdown
Consult the [architecture](./docs/arch.md) for system context.
```
Agent loads only when needed.

**Validation Gates:**
```markdown
**STOP:** Present implementation plan and seek approval before writing code.
```

**Scoped Boundaries (in .agent.md frontmatter):**
```yaml
tools: ['file_read', 'file_write', 'run_tests']
# Note: no deployment tools
```

**Explicit Hierarchy:**
```markdown
# Root AGENTS.md
All code must have tests.

# backend/AGENTS.md  
Use pytest. Coverage minimum 80%.
```

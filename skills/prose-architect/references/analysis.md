# Brownfield Analysis

Heuristics for making existing projects AI-native. Analyze before architecting.

## Context Awareness

**Critical:** Before deep analysis, assess your context capacity.

### Self-Assessment Questions

1. **How much context have I consumed?** — If approaching limits, delegate to subagents
2. **How large is this codebase?** — >50 files or >3 top-level directories = spawn explorers
3. **Am I loading content or structure?** — Prefer structure (file trees) over content (file contents)
4. **Can I summarize instead of quote?** — Summaries preserve context; raw content bloats it

### Context-Preserving Techniques

| Situation | Technique |
|-----------|-----------|
| Large codebase | Spawn `explore` subagents per domain |
| Deep file analysis needed | Ask subagent to summarize, don't read yourself |
| Multiple domains | Analyze one at a time, synthesize findings |
| Unclear structure | Start with file tree + key files (README, package.json, AGENTS.md) |

### When to Spawn Subagents

```
IF (directory has >20 files) OR (analysis requires reading >5 files):
  → Spawn explore agent with specific question
  → Receive summary, not raw content
  
IF (project has >3 distinct domains):
  → Analyze domains sequentially, not all at once
  → Synthesize at the end
```

---

## Quick Scan Protocol

**Goal:** Understand project shape without consuming context.

### Phase 1: Structure (Always Do This First)

```bash
# What you're looking for:
- File tree (top 2 levels)
- Package manifest (package.json, requirements.txt, go.mod, Cargo.toml)
- README.md (project purpose)
- Existing AGENTS.md or .github/agents/ (already AI-native?)
```

### Phase 2: Signals

| Signal | Indicates | Primitive Recommendation |
|--------|-----------|-------------------------|
| Monorepo structure (`apps/`, `packages/`, `services/`) | Multiple domains | Nested AGENTS.md per domain |
| Multiple languages | Polyglot project | Language-specific instructions with `applyTo` |
| Existing CI/CD (`.github/workflows/`) | Automation exists | Reference in AGENTS.md for agent awareness |
| Test directories | Testing culture exists | Include test requirements in instructions |
| No structure | Flat project | Start with root AGENTS.md + one domain instruction |

### Phase 3: Complexity Assessment

| Metric | Low | Medium | High |
|--------|-----|--------|------|
| Top-level directories | 1-3 | 4-7 | 8+ |
| Total files (estimate) | <50 | 50-200 | 200+ |
| Languages | 1 | 2-3 | 4+ |
| Distinct domains | 1 | 2-3 | 4+ |

**Recommendation by complexity:**

- **Low:** Pattern 1 (Single Agent) or Pattern 2 (Agent + Prompts)
- **Medium:** Pattern 3 (Multi-Agent) or Pattern 4 (Full Stack, minimal)
- **High:** Pattern 4 (Full Stack) with phased rollout

---

## Domain Identification

### Common Domain Patterns

| Directory Pattern | Likely Domain | Instruction Scope |
|-------------------|---------------|-------------------|
| `src/components/`, `apps/web/`, `frontend/` | Frontend | `applyTo: "**/*.{tsx,jsx,css}"` |
| `src/api/`, `services/`, `backend/` | Backend | `applyTo: "**/*.{py,go,java}"` |
| `infrastructure/`, `terraform/`, `pulumi/` | Infrastructure | `applyTo: "**/*.{tf,yaml}"` |
| `packages/`, `libs/`, `shared/` | Shared libraries | `applyTo: "packages/**"` |
| `tests/`, `__tests__/`, `spec/` | Testing | Usually covered by domain instructions |
| `docs/`, `documentation/` | Documentation | `applyTo: "docs/**/*.md"` |

### Monorepo Patterns

**Turborepo/Nx style:**
```
apps/           → Each app gets AGENTS.md
packages/       → Shared package rules
```

**Service-oriented:**
```
services/
├── api/        → Backend API rules
├── worker/     → Background job rules
└── gateway/    → API gateway rules
```

**Recommendation:** Create AGENTS.md at each domain root. Let Explicit Hierarchy handle inheritance.

---

## Existing AI Configuration Detection

### Check for Existing Primitives

| File/Pattern | Meaning | Action |
|--------------|---------|--------|
| `AGENTS.md` | Already AI-native | Audit and enhance, don't replace |
| `.github/copilot-instructions.md` | Has Copilot instructions | Migrate to structured primitives |
| `.cursorrules` | Cursor-specific rules | Migrate to portable primitives |
| `.github/agents/` | Has custom agents | Audit for PROSE compliance |
| `.github/chatmodes/` | Legacy chat modes | Migrate to `.agent.md` |

### Migration Priority

1. **Preserve existing AGENTS.md** — It's already the standard
2. **Consolidate tool-specific rules** — `.cursorrules`, `.copilot-instructions.md` → proper primitives
3. **Add structure incrementally** — Don't over-engineer on first pass

---

## Phased Rollout for Large Projects

**Don't try to make everything AI-native at once.**

### Phase 1: Foundation (Day 1)
- Create root `AGENTS.md` with project principles
- Create one instruction file for the most active domain
- Create one agent for the most common task

### Phase 2: Expansion (Week 1)
- Add instructions for remaining domains
- Add prompts for common workflows
- Create nested `AGENTS.md` for complex domains

### Phase 3: Optimization (Ongoing)
- Add skills for reusable capabilities
- Refine based on agent failures
- Add `.context.md` and `.memory.md` as needed

---

## Red Flags

When analyzing a brownfield project, watch for:

| Red Flag | Problem | Mitigation |
|----------|---------|------------|
| No tests | Agents can't verify changes | Add test requirements to instructions |
| No documentation | Agents lack context | Create `.context.md` with key knowledge |
| Inconsistent structure | Hard to scope instructions | Recommend restructuring before AI-native adoption |
| Secrets in code | Security risk | Add explicit prohibition in AGENTS.md |
| No CI/CD | No validation pipeline | Agents must run tests locally |

---

## Output Template

After analysis, provide structured recommendation:

```markdown
## Project Analysis: [Project Name]

### Structure
- Type: [Monorepo/Single app/Library]
- Languages: [List]
- Domains: [List with paths]
- Complexity: [Low/Medium/High]

### Existing AI Configuration
- [List any existing AGENTS.md, instructions, etc.]

### Recommended Pattern
[Pattern 1-5 from patterns.md]

### Proposed Primitive Structure
[File tree of recommended primitives]

### Phased Rollout
- Phase 1: [What to create first]
- Phase 2: [What to add next]
- Phase 3: [Future enhancements]

### Potential Challenges
- [List any red flags or concerns]
```

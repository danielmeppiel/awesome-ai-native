---
layout: docs
title: "Workflows"
display_title: "Workflow Orchestration: From Planning to Execution"
permalink: /docs/workflows/
nav_order: 4
---

Master complete workflows from planning to implementation through Agent Primitives orchestration, async delegation, and multi-agent coordination patterns.

## Primitives in Action: Complete Workflow

**Scenario:** Adding OAuth authentication to a Node.js API - from planning to developer-refined intelligence

### Step 1: Mode Selection & Automatic Context Assembly
```markdown
Developer: "@backend-dev I need to add OAuth authentication"
```

> **Note:** Currently, VSCode chat mode switching requires using the Command Palette (`Cmd/Ctrl+Shift+P` → "Chat: Switch Chat Mode"), keyboard shortcuts, or the chat view dropdown. The `@backend-dev` syntax represents ideal UX that we would like to find in future versions.

**What Happens Behind the Scenes:**
- `backend-dev.chatmode.md` activates with security-focused MCP tool boundaries
- Automatically triggers `security.instructions.md` via `applyTo: "auth/**"` pattern
- VSCode loads domain-specific guidance without polluting global context

### Step 2: Intelligent Context Loading via Markdown Links
**From `security.instructions.md`:**
```markdown
---
applyTo: "./auth/**"
---

## Context Loading
Before implementing authentication, review:
- [Previous security decisions](./auth.memory.md#auth-patterns)
- [API security standards](./api-sec.context.md#security-requirements)
- [Team authentication patterns](./team-auth.context.md#oauth-implementations)

## Security Requirements
- Use industry-standard OAuth 2.0 flow
- Implement proper token validation
- Use the MCP tool `security-scanner` to ensure your implementation is secure
```

**Intelligence Layer:** Markdown hyperlinks automatically pull in relevant project history and standards, creating contextually-aware responses.

### Step 3: Spec-First Planning with Template Structure
**Generated:** `features/auth/oauth-integration.spec.md`
```markdown
# Feature: OAuth 2.0 Authentication System

## Problem Statement
Users need secure third-party authentication via Google/GitHub OAuth providers.

## Approach  
Implement OAuth 2.0 authorization code flow with JWT token management.

## Implementation Requirements
### Core Components
- [ ] OAuth middleware (`src/middleware/oauth.ts`)
- [ ] Token service (`src/services/auth.ts`) 
- [ ] User profile sync (`src/services/user-sync.ts`)

### API Contracts
- `GET /auth/oauth/:provider` - Initiates OAuth flow
- `GET /auth/callback/:provider` - Handles OAuth callback
- `POST /auth/refresh` - Refreshes JWT tokens

### Context References
- Security patterns: [View previous implementations](./auth.memory.md#oauth-v2)
- API standards: [REST conventions](./api-sec.context.md#api-design)

### Validation Criteria
- [ ] Handles OAuth errors with proper redirects
- [ ] JWT tokens properly signed and validated
- [ ] User data synced securely on first login
- [ ] Unit tests >95% coverage
- [ ] Integration tests for all OAuth flows
```

### Step 4: Implementation via Validated Prompt Workflow
**Executed:** `.github/prompts/implement-from-spec.prompt.md`
```markdown
---
mode: agent
tools: ['file-search', 'semantic-search', 'test-runner']
description: 'Spec-to-implementation workflow with validation gates'
---
# Spec-to-Implementation Workflow

## Context Loading Phase
1. Load specification: [${input:specFile}]
2. Review API security patterns: [Security context](./api-sec.context.md#security)
3. Check similar implementations using [the authentication pattern memory](./auth.memory.md#oauth-v2)

## Implementation Phase  
Generate implementation following specification requirements:
- [ ] Core component files with proper interfaces
- [ ] Comprehensive error handling and logging
- [ ] Security-first validation at all boundaries
- [ ] Complete test coverage including edge cases

## Human Validation Gate
🚨 **STOP**: Present specific implementation plan with short code snippets before code generation.
Required approvals you must get from the user:
- [ ] Security architecture review
- [ ] API contract validation  
- [ ] Testing strategy confirmation

## Post-Implementation Learning
After completion, update your primitives based on outcomes:
- Propose to add successful patterns to [auth.memory.md](./auth.memory.md#oauth-v2)
- Suggest security instruction enhancements to the user for [security.instructions.md](./.github/instructions/security.instructions.md) based on discovered edge cases 
```

### Step 5: Developer-Driven Intelligence Refinement

**When Implementation Succeeds:**
- You update `auth.memory.md`: "OAuth flow with Google/GitHub providers - JWT refresh pattern worked well"
- You enhance `security.instructions.md`: "Always implement refresh token rotation for OAuth"
- You refine `implement-from-spec.prompt.md`: "Implement learnings after user validates proposals"

**When Implementation Fails:**
- You record in `auth.memory.md`: "OAuth PKCE flow required for mobile clients - add to future specs"
- You update `security.instructions.md`: "Validate OAuth provider configuration before implementation"
- You enhance `implement-from-spec.prompt.md`: "You must include unit tests to check security of the implementation, with at least 80%+ coverage, and ensure they pass"

### The Compound Intelligence Effect

**Traditional Approach:** Each OAuth implementation starts from scratch, same mistakes repeated.

**AI Native Approach:** Each OAuth implementation allows you to refine the system:
- **Memory**: You preserve successful patterns and failure lessons
- **Instructions**: You enhance based on real project outcomes  
- **Workflows**: You refine validation gates based on discovered edge cases
- **Context**: You accumulate domain expertise across projects

**Result:** The 10th OAuth implementation is dramatically better than the 1st, with the intelligence you've built into the primitives, extending beyond just your memory.


## A. Execution Path Selection
**✅ Quick Actions:**
- **Local IDE Agent:** Maintain maximum control over implementation process
- **Async Delegation:** Maximize productivity for well-specified, low-deviation-risk tasks with the [Coding Agent](https://docs.github.com/en/copilot/how-tos/agents/copilot-coding-agent)
- **Local IDE Monitoring:** Delegate for speed while preserving oversight and learning

> 💡 **Control vs. Productivity Framework**: Choose execution paths based on your desire for control, specification maturity, and tolerance for agent deviation. More control = local implementation. Higher productivity = async delegation to [Coding Agent](https://docs.github.com/en/copilot/how-tos/agents/copilot-coding-agent).

### 🔧 Control-Based Decision Matrix:
```
Control Preference → Recommended Path:
├── High Control Needed → Local IDE Agent (Learn, iterate, guide)
├── Productivity Focus → Async Delegation (Delegate & monitor)  
└── Balanced Approach → Hybrid (Delegate with active oversight)
```

### Quick Decision Matrix: Choose Your Path

| Situation | Local IDE Agent | Async Delegation | Hybrid Monitoring |
|-----------|:---------------:|:----------------:|:-----------------:|
| **First time doing this task** | ✅ | ❌ | ✅ |
| **Well-established pattern** | ❌ | ✅ | ❌ |
| **High-risk/critical feature** | ✅ | ❌ | ✅ |
| **Need speed/parallel work** | ❌ | ✅ | ❌ |
| **Want to learn & understand** | ✅ | ❌ | ✅ |
| **Proven instructions/specs** | ❌ | ✅ | ✅ |
| **Low tolerance for mistakes** | ✅ | ❌ | ✅ |


**⚠️ Checkpoint:** Path selection aligns with control preferences and specification maturity

**📊 Success Metric:** Optimal balance between productivity and quality control

## B. Async Delegation Workflows

### B.1. Single Agent Delegation
**✅ Quick Actions:**
- **VSCode Native**: Use [`#copilotCodingAgent`](https://github.blog/changelog/2025-07-14-start-and-track-github-copilot-coding-agent-sessions-from-visual-studio-code/) in Ask chat mode for direct delegation. You need the [GitHub Pull Requests VSCode extension](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github) installed.
- **GitHub MCP Server**: Leverage `create_issue` and `assign_copilot_to_issue` [GitHub MCP Server tools](https://github.com/github/github-mcp-server?tab=readme-ov-file#tools) from any MCP host application
- **GitHub Web/Mobile**: Direct task assignment via [Agents control plane](https://github.com/copilot/agents)

**🔧 Implementation Pattern:**
```markdown
## Workflow: Single Feature Delegation

1. **Spec Approval** → Validate `.spec.md` with human reviewer
2. **Entry Point Selection**:
   - VSCode: "#copilotCodingAgent implement the OAuth feature per specification"
   - MCP: Use `create_issue` and `assign_copilot_to_issue` tool with spec reference
   - GitHub: the human needs to create task via Agents page with spec attachment
3. **Handoff Confirmation** → Confirm with user and proceed
```

### B.2. Parallel Multi-Agent Delegation (Spec-to-Issues Pattern)
**✅ Quick Actions:**
- **Spec Decomposition:** Break complex specifications into non-overlapping component issues
- **Issue Generation:** Use GitHub MCP Server `create_issue` tool for systematic issue creation
- **Parallel Assignment:** Delegate multiple issues to separate GitHub Coding Agents simultaneously with `assign_copilot_to_issue` GitHub MCP tool

> 💡 **Parallel Orchestration**: Large specifications can be decomposed into independent, parallel workstreams while maintaining architectural coherence through shared context references.

**🔧 Implementation Pattern:**
```markdown
## Workflow: Spec-to-Multiple-Issues Delegation

### Phase 1: Specification Decomposition
1. **Component Analysis** → Identify independent, non-overlapping components
2. **Dependency Mapping** → Define integration points and sequence constraints
3. **Context Distribution** → Ensure each component references shared architecture decisions
4. **Implementation dependencies** → Ensure issues have an implementation order based on mutual dependencies by creating sub-issue hierarchies

### Phase 2: Parallel Issue Generation
Use GitHub MCP Server tools:
- `create_issue(title: "OAuth Middleware Component", body: spec_section_1)`
- `create_issue(title: "Token Service Component", body: spec_section_2)`  
- `create_issue(title: "User Sync Service Component", body: spec_section_3)`

### Phase 3: Parallel Agent Assignment
- `assign_copilot_to_issue(issue_1)` → Agent A works on middleware
- `assign_copilot_to_issue(issue_2)` → Agent B works on token service
- `assign_copilot_to_issue(issue_3)` → Agent C works on user sync

### Phase 4: Coordinated Integration
- **Progress Monitoring** → Track all agents via GitHub Agents control plane
- **Integration Testing** → Validate component interactions
- **Conflict Resolution** → Address any overlapping changes
```

### Example: OAuth System Decomposition
```markdown
# Parent Spec: OAuth 2.0 Authentication System

## Component Breakdown for Parallel Delegation:

### Issue 1: OAuth Middleware (`oauth-middleware`)
**Scope:** Request interception, provider routing, error handling
**Dependencies:** None (independent component)
**Agent Focus:** Middleware patterns, HTTP handling

### Issue 2: Token Service (`token-service`)  
**Scope:** JWT generation, validation, refresh logic
**Dependencies:** None (independent component)
**Agent Focus:** Cryptographic operations, token lifecycle

### Issue 3: User Profile Sync (`user-sync-service`)
**Scope:** OAuth callback handling, user data synchronization
**Dependencies:** Token Service (for user identification)
**Agent Focus:** Data transformation, persistence patterns

### Integration Context References:
- Architecture patterns: [Auth system design](./auth.memory.md#oauth-architecture)
- API conventions: [REST standards](./api-sec.context.md#api-design)
- Security requirements: [OAuth security checklist](./security.instructions.md#oauth)
```

**⚠️ Checkpoint:** Each component is independently implementable with clear integration contracts
**📊 Success Metric:** Parallel agents complete without scope conflicts or integration failures


## C. Progress Monitoring & Async Integration

### C.1. Multi-Channel Progress Tracking
**✅ Quick Actions:**
- **VSCode Integration:** Monitor async tasks via GitHub Pull Request extension "Copilot on My Behalf" section
- **GitHub Control Plane:** Centralized agent status tracking via Agents page

**🔧 Monitoring Capabilities:**
```
Progress Visibility Across Channels:
├── VSCode GitHub PR Extension:
│   ├── Real-time agent status indicators
│   ├── Draft PR previews and progress logs
│   └── Direct session viewing capabilities
└── GitHub Agents Page:
    ├── Multi-agent orchestration dashboard  
    ├── Task status across all repositories
    └── Agent performance metrics
```

### C.2. Async Agent Quality Gates
**✅ Quick Actions:**
1. **Draft PR Review:** Systematic review of async agent outputs before merging
2. **Integration Testing:** Validate component interactions from parallel async work
3. **Context Synchronization:** Update local knowledge with async agent discoveries

> 💡 **Quality Control Strategy**: Treat async agent outputs as high-quality drafts requiring human validation, not finished implementations—maintaining quality standards while leveraging automation speed.

**🔧 Quality Control Workflow:**
```markdown
## Async Agent Output Integration Process

### Phase 1: Draft PR Analysis
1. **Code Review** → Systematic review of async agent implementation
2. **Architecture Alignment** → Validate adherence to original specification
3. **Security Assessment** → Verify security best practices and patterns
4. **Test Coverage Validation** → Ensure comprehensive test implementation

### Phase 2: Integration Validation  
1. **Component Interface Testing** → Validate contracts between parallel components
2. **End-to-End Testing** → Verify complete feature functionality
3. **Performance Assessment** → Check for performance regressions
4. **Documentation Review** → Ensure adequate documentation coverage

### Phase 3: Knowledge Integration
1. **Memory Updates** → Record successful patterns in `.memory.md` files
2. **Instruction Enhancement** → Improve `.instructions.md` based on discoveries
3. **Template Refinement** → Update `.spec.md` templates with learned patterns
```

### Example: OAuth Integration Quality Gates
```markdown
## Async Agent Output Review: OAuth Components

### Component 1: OAuth Middleware (Agent A)
- [x] Code adheres to middleware patterns
- [x] Error handling comprehensive
- [x] Security validations implemented
- [x] Unit tests >90% coverage
- [ ] **Issue**: Missing CSRF protection → Local fix required

### Component 2: Token Service (Agent B)  
- [x] JWT operations secure
- [x] Refresh logic implemented
- [x] Comprehensive error handling
- [x] Integration tests complete
- [x] **Excellent**: Discovered improved token rotation pattern

### Component 3: User Sync Service (Agent C)
- [x] OAuth callback handling robust
- [x] User data transformation secure
- [x] Database operations optimized
- [ ] **Issue**: Race condition in concurrent requests → Local fix required

### Integration Actions:
1. **Local Fixes**: Address CSRF and race condition issues
2. **Knowledge Capture**: Document token rotation improvement in `auth.memory.md`
3. **Process Enhancement**: Add CSRF and concurrency checks to OAuth spec template
```

**⚠️ Checkpoint:** All async outputs meet quality standards before integration
**📊 Success Metric:** Zero production issues from async agent implementations

## D. Advanced: Hybrid Context Strategies

*Building on Basic Delegation for Complex Multi-Component Workflows*

**✅ Quick Actions:**
- **Session Boundaries:** Separate planning, delegation, and integration phases
- **Context Handoff:** Preserve knowledge across sync/async execution contexts
- **Memory Preservation:** Update `.memory.md` files with async agent outcomes

> 💡 **Hybrid Context Strategy**: Maintain cognitive clarity by treating async delegation as context-preserved handoffs rather than context loss, enabling seamless continuation of local work.

### Example: Context-Optimized Hybrid Session
```markdown
## Session 1: Planning & Delegation Setup
### Context Loading
- Review [project requirements](./requirements.md)
- Load [existing auth patterns](./auth.memory.md)
- Generate OAuth specification with component breakdown

### Delegation Handoff
- Create 3 parallel issues via GitHub MCP Server
- Assign GitHub Coding Agents to each component
- Preserve delegation context in [delegation.memory.md](./delegation.memory.md#oauth-parallel)

## Session 2: Local Development (Concurrent)
### Fresh Context for Local Work
- Continue on frontend components (independent of OAuth backend)
- Monitor async agent progress via VSCode GitHub PR extension
- Address any integration questions from async agents

## Session 3: Integration & Learning (Post-Async Completion)
### Context Assembly
- Review async agent outputs from draft PRs
- Load integration context from [delegation.memory.md](./delegation.memory.md#oauth-parallel)
- Perform integration testing and conflict resolution

### Knowledge Accumulation
- Update [auth.memory.md](./auth.memory.md) with successful patterns
- Enhance [security.instructions.md](./.github/instructions/security.instructions.md) based on discoveries
- Refine delegation patterns for future complex features
```

**⚠️ Checkpoint:** Context preservation enables seamless hybrid sync/async workflows
**📊 Success Metric:** No cognitive overhead when switching between local and async work contexts

## Key Takeaways

1. **Complete Workflows** combine Agent Primitives into systematic, repeatable processes
2. **Execution Path Selection** balances control vs. productivity based on your specific needs
3. **Async Delegation** enables parallel work while maintaining quality through validation gates
4. **Hybrid Context Strategies** preserve knowledge across sync/async execution boundaries
5. **Intelligence Refinement** creates compound learning that improves over time

**Ready to scale across teams?** Continue to [Team Adoption](../team-adoption/) for organizational implementation.

**Need implementation templates?** Check out the [Examples](../examples/) for ready-to-use primitives.

*You now have complete workflow orchestration patterns. The next step is scaling these techniques across your entire organization.*

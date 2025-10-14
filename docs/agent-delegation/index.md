---
layout: docs
title: "Agent Delegation"
display_title: "Agent Delegation"
permalink: /docs/agent-delegation/
nav_order: 4
---

With your **Agentic Workflows** built and ready, you now face a critical decision: how to execute them. The strategies you choose—from local control to sophisticated async orchestration—fundamentally shape both your development speed and learning outcomes.

This guide covers the complete spectrum of execution approaches, from maintaining tight control in your local IDE to delegating complex workflows to multiple async agents working in parallel. Each strategy has optimal use cases, and mastering the decision framework ensures you choose the right approach for each situation.

## Execution Strategy Overview

**Agentic Workflows** can be executed through three primary strategies, each offering different balances of control, speed, and learning:

1. **Local IDE Execution** - Direct workflow execution in your development environment for maximum control and learning
2. **Async Agent Delegation** - Hand off complete workflows to GitHub Coding Agents for parallel productivity
3. **Hybrid Orchestration** - Strategic combination of local control and async delegation with context preservation

The key insight is that the **same Agentic Workflow** can be executed through different strategies based on your current needs, workflow maturity, and tolerance for agent deviation.

## Agentic Workflow Execution Example

To demonstrate the execution strategies, let's use a complete **Agentic Workflow** for implementing OAuth authentication. This workflow orchestrates all your Agent Primitives into a systematic process that can be executed through any of the strategies below.

**Example Workflow:** `implement-oauth-feature.prompt.md`

### Workflow Components in Action:
1. **Mode Activation** → Triggers `backend-dev.chatmode.md` with security-focused MCP tool boundaries  
2. **Context Loading** → Loads `[auth patterns](./auth.memory.md)` and `[security standards](./security.context.md)`
3. **Specification Generation** → Uses `oauth-feature.spec.md` template with validation criteria
4. **Implementation Execution** → Guided by `security.instructions.md` applied via `applyTo: "auth/**"` pattern
5. **Learning Integration** → Updates `.memory.md` with successful patterns and discovered edge cases

**Key Insight:** This same workflow produces consistent results whether executed locally for learning or delegated async for speed. The execution strategy becomes a separate decision from the workflow design.

Now let's examine how to choose and execute the optimal strategy for your specific situation.

## A. Execution Strategy Selection

Once you've built your Agentic Workflow, you need to decide how to execute it. This choice between local control and async delegation fundamentally shapes both your development speed and learning outcomes.

**✅ Quick Actions:**
- **Local IDE Execution:** Maintain maximum control over implementation process for learning and complex tasks
- **Async Agent Delegation:** Maximize productivity for well-specified, low-deviation-risk tasks with the [GitHub Coding Agent](https://docs.github.com/en/copilot/how-tos/agents/copilot-coding-agent)
- **Hybrid Orchestration:** Combine local control with async delegation while preserving context and oversight

> 💡 **Control vs. Productivity Framework**: Choose execution paths based on your desire for control, workflow maturity, and tolerance for agent deviation. More control = local execution. Higher productivity = async delegation.

### 🔧 Strategic Decision Matrix:
```
Control Preference → Recommended Strategy:
├── High Control Needed → Local IDE Execution (Learn, iterate, guide)
├── Productivity Focus → Async Agent Delegation (Delegate & monitor)  
└── Balanced Approach → Hybrid Orchestration (Delegate with active oversight)
```

### Quick Decision Guide: Choose Your Execution Strategy

| Situation | Local IDE | Async Delegation | Hybrid Orchestration |
|-----------|:---------:|:----------------:|:-------------------:|
| **First time with this workflow** | ✅ | ❌ | ✅ |
| **Well-established workflow** | ❌ | ✅ | ❌ |
| **High-risk/critical feature** | ✅ | ❌ | ✅ |
| **Need speed/parallel work** | ❌ | ✅ | ✅ |
| **Want to learn & understand** | ✅ | ❌ | ✅ |
| **Low tolerance for mistakes** | ✅ | ❌ | ✅ |

**⚠️ Checkpoint:** Strategy selection aligns with control preferences and maturity of your agent primitives

**📊 Success Metric:** Optimal balance between productivity and quality control

The execution strategy you choose determines not just the speed of development, but also how much you learn from each implementation and how much oversight you maintain throughout the process.

## B. Local IDE Execution

For maximum control and learning, execute your Agentic Workflows directly in your development environment. This strategy is optimal when you're working with new patterns, complex requirements, or want to deeply understand the implementation process.

**✅ Quick Actions:**
- **Direct Prompt Execution:** Use `/workflow-name` in VSCode chat to execute your `.prompt.md` files
- **Step-by-Step Control:** Manually progress through each workflow phase with full oversight
- **Real-Time Learning:** Observe and guide the AI through complex decision points

> 💡 **Learning Optimization**: Local execution preserves maximum context for understanding both successful patterns and failure modes, making it ideal for building expertise and refining workflows.

### 🔧 Implementation Pattern:
```markdown
## Local IDE Agentic Workflow Execution

1. **Workflow Selection** → Choose the `<workflow-name>.prompt.md` workflow file to execute
2. **Context Preparation** → Ensure relevant files and specifications are ready
3. **Execution Control** → Use `/workflow-name` in VSCode chat to trigger the workflow
4. **Interactive Guidance** → Provide input at validation gates and decision points
5. **Learning Capture** → Document insights and refine workflow based on outcomes
```

### Example: Local OAuth Implementation
Using `implement-oauth-feature.prompt.md` workflow:

```markdown
Developer in VSCode Chat:
> /implement-oauth-feature ./specs/oauth-integration.spec.md

AI Response:
> Loading workflow: implement-oauth-feature.prompt.md
> 
> ## Context Loading Phase ✅
> - Loaded specification: oauth-integration.spec.md
> - Reviewed auth patterns: 3 previous implementations found
> - Security standards: OAuth 2.0 + JWT validation requirements loaded
> 
> ## Human Validation Gate 🚨
> Architecture review required before proceeding:
> 
> **Proposed Implementation:**
> 1. OAuth middleware with PKCE flow
> 2. JWT service with refresh token rotation  
> 3. User sync service with conflict resolution
> 
> **Security considerations:**
> - CSRF protection via state parameter
> - Token storage in httpOnly cookies
> - Rate limiting on auth endpoints
> 
> Approve this architecture? [Yes/No/Modify]

Developer:
> Yes, but add rate limiting to 5 attempts per minute

AI Response:
> ✅ Architecture approved with rate limiting enhancement
> 
> Proceeding with implementation...
> [Generated secure OAuth implementation with enhanced rate limiting]
> 
> ## Learning Integration Phase
> 🎯 New pattern discovered: Enhanced rate limiting for auth endpoints
> 
> Should I update security.instructions.md with this pattern? [Yes/No]
```

**Benefits of Local Execution:**
- **Full Control**: Guide every decision and validate each step
- **Deep Learning**: Understand the reasoning behind implementation choices  
- **Immediate Refinement**: Adjust workflows in real-time based on outcomes
- **Context Preservation**: Maintain complete development context throughout the process

**⚠️ Checkpoint:** Local execution maximizes learning and control at the cost of speed

**📊 Success Metric:** High-quality implementations with deep understanding and workflow refinement

## C. Async Agent Delegation

When speed and parallel productivity are priorities, delegate your complete Agentic Workflows to GitHub Coding Agents. This strategy works best with mature workflows, clear specifications, and established patterns where the implementation path is well-understood.

Your Agentic Workflows can be executed through various async delegation patterns, from single-agent execution to sophisticated parallel orchestration.

### C.1. Single Agent Delegation
**✅ Quick Actions:**
- **VSCode Native**: Use [`#copilotCodingAgent`](https://github.blog/changelog/2025-07-14-start-and-track-github-copilot-coding-agent-sessions-from-visual-studio-code/) in Ask chat mode for direct delegation. You need the [GitHub Pull Requests VSCode extension](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github) installed.
- **GitHub MCP Server**: Leverage `create_issue` and `assign_copilot_to_issue` [GitHub MCP Server tools](https://github.com/github/github-mcp-server?tab=readme-ov-file#tools) from any MCP host application
- **GitHub Web/Mobile**: Direct task assignment via [Agents control plane](https://github.com/copilot/agents)

**🔧 Implementation Pattern:**
```markdown
## Single Agent Workflow Delegation

1. **Spec Approval** → Validate `.spec.md` with human reviewer
2. **Entry Point Selection**:
   - VSCode: "#copilotCodingAgent implement the OAuth feature per specification"
   - MCP: Use `create_issue` and `assign_copilot_to_issue` tool with spec reference
   - GitHub: the human needs to create task via Agents page with spec attachment
3. **Handoff Confirmation** → Confirm with user and proceed
```

### C.2. Parallel Multi-Agent Delegation (Spec-to-Issues Pattern)
**✅ Quick Actions:**
- **Spec Decomposition:** Break complex specifications into non-overlapping component issues
- **Issue Generation:** Use GitHub MCP Server `create_issue` tool for systematic issue creation
- **Parallel Assignment:** Delegate multiple issues to separate GitHub Coding Agents simultaneously with `assign_copilot_to_issue` GitHub MCP tool

> 💡 **Parallel Orchestration**: Large specifications can be decomposed into independent, parallel workstreams while maintaining architectural coherence through shared context references.

**🔧 Implementation Pattern:**
```markdown
## Agentic Workflow: Spec-to-Multiple-Issues Delegation

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

Async delegation creates new challenges around quality control and learning integration. While agents work independently, you need systematic approaches to validate their outputs and incorporate their discoveries back into your evolving Agent Primitives.

## D. Progress Monitoring & Async Integration

Once your agents are working asynchronously, maintaining visibility and control becomes crucial. This section covers the essential practices for maintaining oversight and learning from async agent execution. 

### D.1. Multi-Channel Progress Tracking
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

### D.2. Async Agent Quality Gates
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

## E. Hybrid Orchestration Strategies

The most sophisticated approach combines local control with async delegation through strategic context management. This hybrid strategy preserves the benefits of both execution approaches while minimizing their respective downsides when executing complex Agentic Workflows.

*Building on Basic Delegation for Complex Multi-Component Workflows*

**✅ Quick Actions:**
- **Session Boundaries:** Separate planning, delegation, and integration phases
- **Context Handoff:** Preserve workflow knowledge across sync/async execution strategies  
- **Memory Preservation:** Update `.memory.md` files with async agent outcomes

> 💡 **Hybrid Context Strategy**: Maintain cognitive clarity by treating async delegation as context-preserved handoffs rather than context loss, enabling seamless continuation of local work while agents execute workflows in parallel.

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

**⚠️ Checkpoint:** Context preservation enables seamless hybrid sync/async Agentic Workflow execution

**📊 Success Metric:** No cognitive overhead when switching between local and async work contexts

## Key Takeaways

1. **Execution Strategy Selection** balances control vs. productivity based on workflow maturity and specific needs
2. **Local IDE Execution** maximizes learning and control for complex or unfamiliar Agentic Workflows
3. **Async Agent Delegation** enables parallel execution and productivity for proven workflows with clear specifications
4. **Hybrid Orchestration** combines the benefits of both approaches through strategic context preservation
6. **Intelligence Refinement** creates compound learning that improves Agent Primitives over time

**Ready to scale to teams?** Continue to [Team & Enterprise Scale](../team-adoption/) to bridge from individual mastery to team coordination through spec-driven workflows and enterprise governance.

**Need implementation templates?** Check out the [Examples](../../examples/) for ready-to-use primitives.

*You now have complete agentic workflow patterns and delegation strategies. The next step is scaling these techniques across your entire organization.*

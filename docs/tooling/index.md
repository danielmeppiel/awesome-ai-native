---
layout: docs
title: "Tooling"
display_title: "Tooling: Scaling Agent Primitives"
permalink: /docs/tooling/
nav_order: 3
---

You've mastered the [three-layer framework](../concepts/) and understand that your Agent Primitives are **executable software written in natural language**. Now comes the natural next question: how do these markdown files scale beyond your individual development workflow into production-grade infrastructure?

The answer mirrors every programming ecosystem's evolution. Just as JavaScript grew from browser scripts to need Node.js runtimes, package managers, and deployment tooling, your Agent Primitives need similar infrastructure to reach their full potential.

## Natural Language as Code

Your Agent Primitives exhibit all the characteristics of professional software: modularity, reusability, dependencies, versioning, and continuous evolution. This isn't just a metaphor - these `.prompt.md` and `.instructions.md` files represent a genuine new form of software development that deserves proper tooling infrastructure.

Consider what happens as your Agent Primitives mature:

- **Modularity**: Separate concerns across different primitive files that work together
- **Reusability**: Same primitives work reliably across projects and contexts  
- **Dependencies**: MCP servers, external tools, and context requirements that must be managed
- **Evolution**: Continuous refinement and versioning as your workflows improve
- **Distribution**: Teams want to share proven primitives like they share code libraries

This recognition transforms how we think about AI development tooling. Your natural language programs need the same infrastructure support as any other software.

## Agent CLI Runtimes

Most developers create and run Agent Primitives directly in VS Code with GitHub Copilot - and that's perfect for interactive development, debugging, and daily workflow refinement. But just as JavaScript eventually needed Node.js to break free from browser constraints, your natural language programs need **Agent CLI Runtimes** for automated and production scenarios.

The emerging ecosystem includes different vendor implementations of the same core functionality: **OpenAI Codex CLI**, **Anthropic Claude Code**, **Google Gemini CLI**, and future vendor runtimes as the ecosystem matures. Each provides command-line execution of your Agent Primitives with access to their respective model capabilities.

### Inner Loop vs Outer Loop

The key insight is understanding when each environment serves you best:

- **Inner Loop (VS Code + GitHub Copilot)**: Interactive development, testing, and workflow refinement
- **Outer Loop (Agent CLI Runtimes)**: Reproducible execution, CI/CD integration, and production deployment

Agent CLI Runtimes transform your Agent Primitives from IDE-bound files into **autonomously executable workflows** that run consistently across any environment. They provide command-line execution, CI/CD integration, environment consistency, and native support for MCP servers - bridging your development work to production reality.

## Runtime Management

While VS Code + GitHub Copilot handles individual development perfectly, teams need additional infrastructure for **sharing, versioning, and productizing** their Agent Primitives. Managing multiple CLI environments becomes complex quickly - different installation procedures, configuration requirements, and compatibility matrices.

[Agent Package Manager](https://github.com/danielmeppiel/apm) solves this by providing unified runtime management and agent package distribution. Instead of manually installing and configuring each vendor CLI, APM handles the complexity while preserving your existing VS Code workflow.

Here's how runtime management works in practice:

```bash
# Install APM once
curl -sSL https://raw.githubusercontent.com/danielmeppiel/apm/main/install.sh | sh

# Optional: setup your GitHub PAT to use GitHub Copilot CLI
export GITHUB_COPILOT_PAT=your_token_here

# APM manages runtime installation for you
apm runtime setup copilot        # Installs GitHub Copilot CLI (Recommended)
apm runtime setup codex          # Installs OpenAI Codex CLIs

# Check what's available
apm runtime list                 # Shows installed runtimes
apm runtime status               # Shows which runtime will be used

# Install MCP dependencies (like npm install)
# Note: this feature is under development
apm install

# Compile Instructions files to Agents.md files
apm compile

# Run workflows against your chosen runtime
# This will trigger 'copilot --log-level all --log-dir copilot-logs --allow-all-tools -p  security-review.prompt.md' command 
# Check the example apm.yml file a bit below in this guide
apm run copilot-sec-review --param pr_id=123 
```

The key benefits become immediately apparent: your daily development stays exactly the same in VS Code, APM installs and configures runtimes automatically, your workflows run regardless of which runtime is installed, and the same `apm run` command works consistently across all runtimes.

**✅ Checkpoint:** Runtime complexity is abstracted away while preserving development workflow flexibility

## Context Compilation & Optimization

Your modular `.instructions.md` files work great in VSCode, but they're locked to that one environment. To work across all coding agents (Cursor, Claude Desktop, etc.), you need the universal `AGENTS.md` standard. And when pulling in primitives from multiple packages, they need to merge intelligently without context pollution.

**Compilation solves both:** transforms VSCode-native instructions into portable `AGENTS.md` files while optimizing how contexts from dependencies and local primitives combine. This is what enables **spec-driven team coordination** from [Team & Enterprise Scale](../team-adoption/).

[APM's compiler](https://github.com/danielmeppiel/apm) analyzes your `applyTo` patterns, maps your directory structure, and generates the optimal `AGENTS.md` hierarchy that guarantees complete coverage with minimal redundancy:

```bash
# 1. Author modular primitives as usual
.apm/instructions/
├── security.instructions.md      # applyTo: "**/auth/**"
├── react.instructions.md         # applyTo: "**/*.{tsx,jsx}"
└── api-design.instructions.md    # applyTo: "backend/api/**"

# 2. Run compilation
apm compile

# 3. Optimal AGENTS.md hierarchy generated automatically
├── AGENTS.md                     # Global context (minimal)
├── frontend/AGENTS.md           # React patterns
└── backend/
    ├── AGENTS.md                # Backend patterns
    └── auth/AGENTS.md           # Security + backend
```

**Key benefits:**
- **Portability**: Works across all coding agents supporting AGENTS.md standard
- **Efficiency**: Reduction in context per file vs manual approaches
- **Coverage**: Mathematical guarantee every file gets needed instructions
- **Maintenance**: Modify primitives, recompile — `AGENTS.md` updates automatically
- **Team Coordination**: Changes to team standards instantly propagate through compilation

```bash
$ apm compile --verbose

Generated 5 AGENTS.md files --- Context efficiency: 46.7%

Placement Distribution
├─ .                      Constitution and 5 instructions from 4 sources
├─ tests                  2 instructions from 3 sources
├─ docs                   1 instructions from 2 sources
├─ backend/api            2 instructions from 4 sources
└─ scripts/deployment     1 instructions from 1 source
```

For small projects (5-10 instruction files), manual `AGENTS.md` organization works fine—see [Getting Started](../getting-started/). As you scale beyond that or start using dependencies, compilation becomes essential. See [APM's compilation docs](https://github.com/danielmeppiel/apm/blob/main/docs/compilation.md) for technical details.

**✅ Checkpoint:** Compilation creates portable, optimized context that scales across agents and projects

## Distribution and Packaging

Once your Agent Primitives prove valuable, you'll naturally want to **share them with your team** and eventually **deploy them in production**. This is where the parallels to traditional software development become most apparent - you need package management, dependency resolution, version control, and distribution mechanisms.

The challenge emerges quickly: you've built powerful Agent Primitives, your team wants to use them, but distributing markdown files and ensuring consistent MCP dependencies across different environments becomes unwieldy. You need the equivalent of npm for natural language programs.

[APM](https://github.com/danielmeppiel/apm) provides npm-style package management for natural language programs—create distributable packages with dependencies, versioning, and composition. This is the foundation for **agent onboarding** and **enterprise governance** from [Team & Enterprise Scale](../team-adoption/).

### Package Management in Practice

```bash
# Create an APM package
apm init security-review-workflow

# Write .apm/instructions/*.instructions.md files

# Develop and test your agentic workflow locally
cd security-review-workflow 
apm compile && apm install
apm run copilot-sec-review --param pr_id=123

# Publish the APM package to GitHub: 
git tag v1.0.0 && git push --tags
```

APM projects have an `apm.yml` configuration file that serves as the `package.json` equivalent for Agent Primitives, defining scripts, dependencies, and input parameters:

```yaml
# Team members can install and use your primitives
# apm.yml in your project root (like package.json)
name: security-review-workflow
version: 1.2.0
description: Comprehensive security review process with GitHub integration
scripts:
  copilot-sec-review: "copilot --log-level all --log-dir copilot-logs --allow-all-tools -p  security-review.prompt.md"
  codex-sec-review: "codex security-review.prompt.md"
  codex-debug: "RUST_LOG=debug codex security-review.prompt.md"
  
dependencies:
  apm:
    - company/compliance-rules
    - company/design-guidelines
  mcp:
    - github/github-mcp-server
```

Upon context compilation, multiple APM packages can contribute to the same `applyTo` patterns without conflicts. When `company/compliance-rules`, `company/design-guidelines`, and your local project all target `**/auth/**`, compilation merges all three contexts with source attribution—layered, composable context building on shared foundations.

**Real example:** [corporate-website](https://github.com/danielmeppiel/corporate-website) uses `compliance-rules` + `design-guidelines` as dependencies. After `apm install && apm compile`, compliance patterns automatically apply to data handling code, design standards to frontend components, both compose with local context—zero conflicts, complete coverage.

**Enterprise governance pattern:** When your compliance team updates `company/compliance-rules` with new data retention policies, every team across the organization runs `apm install && apm compile`. Every agent, every project, instantly compliant. This is **deterministic agent onboarding at scale**—policies become enforceable primitives, not training materials.

The benefits compound quickly: distribute tested workflows and instructions as versioned packages with dependencies, automatically resolve and install required MCP servers, track workflow evolution and maintain compatibility across updates, build on shared primitive libraries from the community, ensure consistent execution across different team members' setups, and enable instant enterprise-wide policy updates for governance.

**✅ Checkpoint:** Your Agent Primitives are now packaged as distributable software with managed dependencies

## Production Deployment

The final piece of the tooling ecosystem enables **Continuous AI** - automated execution of packaged Agent Primitives in production environments. Your carefully developed workflows can now run automatically in CI/CD pipelines with the same reliability as traditional software deployments.

Building on the `security-review-workflow` package example above, here's how the same APM project deploys to production with multi-runtime flexibility.

```yaml
# .github/workflows/security-review.yml
name: AI Security Review Pipeline
on: 
  pull_request:
    types: [opened, synchronize]

jobs:
  security-analysis:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        script: [codex-sec-review, copilot-sec-review, codex-debug]  # Maps to apm.yml scripts
    permissions:
      models: read
      pull-requests: write
      contents: read
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Run Security Review (${{ matrix.script }})
      uses: danielmeppiel/action-apm-cli@v1
      with:
        script: ${{ matrix.script }}
        parameters: |
          {
            "pr_id": "${{ github.event.number }}"
          }
      env:
        GITHUB_COPILOT_PAT: ${{ secrets.GITHUB_COPILOT_PAT }}
      
```

**Key Connection**: The `matrix.script` values (`codex-sec-review`, `copilot-sec-review`, `codex-debug`) correspond exactly to the scripts defined in the `apm.yml` configuration above. [APM](https://github.com/danielmeppiel/apm) automatically installs the MCP dependencies (`ghcr.io/github/github-mcp-server`, `security-scanner-mcp`) and passes the input parameters (`pr_id`) to your security-review.prompt.md workflow.

This creates production-ready AI workflows with runtime flexibility, parallel execution capabilities, consistent deployment across environments, and automated quality processes integrated into standard CI/CD pipelines.

**✅ Checkpoint:** Your Agent Primitives now run automatically in production with the same reliability as traditional software

## Ecosystem Evolution

This tooling progression follows the same predictable pattern as every successful programming ecosystem. Understanding this pattern helps you see where AI Native Development is heading and how to position your work strategically.

The evolution happens in four stages:

1. **Raw Code** → Agent Primitives (.prompt.md, .instructions.md files)
2. **Runtime Environments** → Agent CLI Runtimes (Codex CLI, Claude Code, etc.)
3. **Package Management** → [APM](https://github.com/danielmeppiel/apm) (distribution and orchestration layer)
4. **Thriving Ecosystem** → Shared libraries, tools, and community packages

Just as npm enabled JavaScript's explosive growth by solving the package distribution problem, [APM](https://github.com/danielmeppiel/apm) enables the Agent Primitive ecosystem to flourish by providing the missing infrastructure layer that makes sharing and scaling natural language programs practical.

## Key Takeaways

1. **Natural Language as Code** - Your Agent Primitives are genuine software that deserves proper tooling infrastructure
2. **Agent CLI Runtimes** enable execution beyond VS Code, particularly for CI/CD and production scenarios  
3. **Runtime Management** through APM simplifies portability in multi-vendor Agentic Coding environments while preserving VS Code workflow
4. **Context Compilation** transforms modular `.instructions.md` into portable, optimized `AGENTS.md` hierarchies
5. **Package Management** enables npm-style distribution with dependencies, versioning, and composition
6. **Production Deployment** makes Agent Primitives first-class citizens in modern software delivery

**Ready to execute workflows?** With production-grade infrastructure in place, continue to [Agent Delegation](../agent-delegation/) to master execution strategies—from local IDE control to sophisticated async orchestration that leverages everything you just learned.

**Want to see advanced execution patterns?** Jump to [Agent Delegation](../agent-delegation/) for comprehensive orchestration strategies that leverage this tooling foundation for both local and async agent coordination.

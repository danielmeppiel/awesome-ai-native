---
layout: docs
title: "Tooling"
display_title: "Tooling: Scaling Agent Primitives"
permalink: /docs/tooling/
nav_order: 3
---

You've mastered the [three-layer framework](../concepts/index.md) and understand that your Agent Primitives are **executable software written in natural language**. Now comes the natural next question: how do these markdown files scale beyond your individual development workflow?

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

[APM CLI](https://github.com/danielmeppiel/apm-cli) solves this by providing unified runtime management and package distribution. Instead of manually installing and configuring each vendor CLI, APM handles the complexity while preserving your existing VS Code workflow.

Here's how runtime management works in practice:

```bash
# Install APM CLI once
curl -sSL https://raw.githubusercontent.com/danielmeppiel/apm-cli/main/install.sh | sh

# Optional: setup your GitHub PAT with read-only Models permissions for free inferencing with GitHub Models https://github.com/settings/personal-access-tokens/new
export GITHUB_TOKEN=your_token_here

# APM manages runtime installation for you
apm runtime setup codex          # Installs OpenAI Codex CLI
apm runtime setup llm            # Installs Simon Willison's LLM

# Check what's available
apm runtime list                 # Shows installed runtimes
apm runtime status               # Shows which runtime will be used

# Install MCP dependencies (like npm install)
# Note: this feature is under development
apm install

# Compile Agent Primitive files to Agents.md files
apm compile

# Run workflows against your chosen runtime
# This will trigger 'codex security-review.prompt.md' command 
# Check the example apm.yml file a bit below in this guide
apm run codex-sec-review --param pr_id=123 
```

The key benefits become immediately apparent: your daily development stays exactly the same in VS Code, APM installs and configures runtimes automatically, your workflows run regardless of which runtime is installed, and the same `apm run` command works consistently across all runtimes.

**✅ Checkpoint:** Runtime complexity is abstracted away while preserving development workflow flexibility

## Distribution and Packaging

Once your Agent Primitives prove valuable, you'll naturally want to **share them with your team** and eventually **deploy them in production**. This is where the parallels to traditional software development become most apparent - you need package management, dependency resolution, version control, and distribution mechanisms.

The challenge emerges quickly: you've built powerful Agent Primitives in VS Code, your team wants to use them, but distributing markdown files and ensuring consistent MCP dependencies across different environments becomes unwieldy. You need the equivalent of npm for natural language programs.

[APM CLI](https://github.com/danielmeppiel/apm-cli) provides this missing layer. It doesn't replace your VS Code workflow - it **extends** it by creating distributable packages of Agent Primitives complete with dependencies, configuration, and runtime compatibility that teams can share like npm packages.

### Package Management in Practice

```bash
# Initialize new APM project (like npm init)
apm init security-review-workflow

# Develop and test your workflow locally
cd security-review-workflow 
apm compile && apm install
apm run codex-sec-review --param pr_id=123

# Package for distribution (future: apm publish)
# Share apm.yml and Agent Primitive files with team
# Team members can install and use your primitives
git clone your-workflow-repo
cd your-workflow-repo && apm compile && apm install
apm run codex-sec-review --param pr_id=456  
```

The benefits compound quickly: distribute tested workflows as versioned packages with dependencies, automatically resolve and install required MCP servers, track workflow evolution and maintain compatibility across updates, build on shared primitive libraries from the community, and ensure consistent execution across different team members' setups.

### Project Configuration

Create your `apm.yml` configuration file that serves as the package.json equivalent for Agent Primitives, defining scripts, dependencies, and input parameters:

```yaml
# apm.yml - Project configuration (like package.json)
name: security-review-workflow
version: 1.2.0
description: Comprehensive security review process with GitHub integration

scripts:
  codex-sec-review: "codex security-review.prompt.md"
  llm-sec-review: "llm security-review.prompt.md"
  codex-debug: "RUST_LOG=debug codex security-review.prompt.md"
  
dependencies:
  mcp:
    - ghcr.io/github/github-mcp-server
    - registry.npmjs.org/security-scanner-mcp
```

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
        script: [codex-sec-review, llm-sec-review, codex-debug]  # Maps to apm.yml scripts
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
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**Key Connection**: The `matrix.script` values (`codex-sec-review`, `llm-sec-review`, `codex-debug`) correspond exactly to the scripts defined in the `apm.yml` configuration above. [APM CLI](https://github.com/danielmeppiel/apm-cli) automatically installs the MCP dependencies (`ghcr.io/github/github-mcp-server`, `security-scanner-mcp`) and passes the input parameters (`pr_id`) to your security-review.prompt.md workflow.

This creates production-ready AI workflows with runtime flexibility, parallel execution capabilities, consistent deployment across environments, and automated quality processes integrated into standard CI/CD pipelines.

**✅ Checkpoint:** Your Agent Primitives now run automatically in production with the same reliability as traditional software

## Ecosystem Evolution

This tooling progression follows the same predictable pattern as every successful programming ecosystem. Understanding this pattern helps you see where AI Native Development is heading and how to position your work strategically.

The evolution happens in four stages:

1. **Raw Code** → Agent Primitives (.prompt.md, .instructions.md files)
2. **Runtime Environments** → Agent CLI Runtimes (Codex CLI, Claude Code, etc.)
3. **Package Management** → [APM CLI](https://github.com/danielmeppiel/apm-cli) (distribution and orchestration layer)
4. **Thriving Ecosystem** → Shared libraries, tools, and community packages

Just as npm enabled JavaScript's explosive growth by solving the package distribution problem, [APM CLI](https://github.com/danielmeppiel/apm-cli) enables the Agent Primitive ecosystem to flourish by providing the missing infrastructure layer that makes sharing and scaling natural language programs practical.

## Key Takeaways

1. **Agent Primitives are Software**: Your `.prompt.md` and `.instructions.md` files represent executable natural language programs that deserve professional tooling infrastructure
2. **Runtime Diversity Enables Scale**: Agent CLI Runtimes (Codex CLI, Claude Code, Gemini CLI) provide the execution environments that bridge development to production
3. **Package Management is Critical**: [APM CLI](https://github.com/danielmeppiel/apm-cli) provides the npm-equivalent layer that makes Agent Primitives truly portable and shareable
4. **Production Ready Today**: This tooling stack enables automated AI workflows in CI/CD pipelines with enterprise-grade reliability
5. **Ecosystem Growth Pattern**: Package management infrastructure creates the foundation for thriving ecosystems of shared workflows, tools, and community libraries

The transformation is profound: what started as individual markdown files in your editor becomes a systematic software development practice with proper tooling, distribution, and production deployment capabilities.


**Ready to build your first Agent Primitives?** Continue to [Getting Started](../getting-started/) to implement the foundational workflows that this tooling infrastructure supports.

**Want to see advanced execution patterns?** Jump to [Agent Delegation](../agent-delegation/) for comprehensive orchestration strategies that leverage this tooling foundation for both local and async agent coordination.

# PROSE

### Build agentic primitives for GitHub Copilot.

Skills, Custom Agents, Instructions, and Hooks — designed with proven architectural patterns, bundled into plugins, and shipped on marketplaces. Hands-on. Copilot-native. Practitioner-tested.

**[Start building →](https://danielmeppiel.github.io/awesome-ai-native/docs/getting-started/)** &nbsp;·&nbsp; **[Read the Specification →](https://danielmeppiel.github.io/agentic-sdlc-handbook/handbook/ch12-the-prose-specification.html)**

---

> **The book teaches the discipline. This site shows you how to ship it in Copilot.**
>
> [*The Agentic SDLC Handbook*](https://danielmeppiel.github.io/agentic-sdlc-handbook/) is the in-depth reference for PROSE — the seven primitive types, the load lifecycle, the architectural patterns, the methodology. This site is the practitioner's playbook: how to author Skills, Custom Agents, Instructions, and Hooks for Copilot, bundle them as plugins, and distribute them. Theory there. Practice here.

---

## PROSE — the five constraints

| | Constraint | Principle | Induced Property |
|---|------------|-----------|------------------|
| **P** | **Progressive Disclosure** | Context arrives just-in-time, not just-in-case | Efficient context utilization |
| **R** | **Reduced Scope** | Match task size to context capacity | Manageable complexity |
| **O** | **Orchestrated Composition** | Simple things compose; complex things collapse | Flexibility, reusability |
| **S** | **Safety Boundaries** | Autonomy within guardrails | Reliability, security |
| **E** | **Explicit Hierarchy** | Specificity increases as scope narrows | Modularity, inheritance |

---

## 🔌 Install the PROSE Skill

Use PROSE directly in Claude Code or GitHub Copilot CLI:

```bash
# Add the marketplace
/plugin marketplace add danielmeppiel/awesome-ai-native

# Install the skill
/plugin install prose-architect@prose
```

Once installed, the skill auto-activates when you:
- Ask to build an AI-native app from requirements
- Want to make a legacy project AI-native
- Need to design agent workflows or primitives

---

## 🚀 Quick Access

### 📚 **[Complete Guide →](https://danielmeppiel.github.io/awesome-ai-native)**
Access the full AI Native Development guide with improved navigation and structure

### 🧠 **[The Practice →](https://danielmeppiel.github.io/awesome-ai-native/docs/concepts/)**  
Three disciplines that implement PROSE: Prompt Engineering, Agent Primitives, Context Engineering

### 🎯 **[PROSE Specification →](https://danielmeppiel.github.io/awesome-ai-native/docs/prose/)**  
The architectural style definition—constraints, grounding principles, and derivation

### 🛠️ **[Getting Started →](https://danielmeppiel.github.io/awesome-ai-native/docs/getting-started/)**
Build your first Agent Primitives and see immediate results

### ⚙️ **[Agent Delegation →](https://danielmeppiel.github.io/awesome-ai-native/docs/agent-delegation/)**
Master advanced patterns and async delegation workflows

### 👥 **[Team Adoption →](https://danielmeppiel.github.io/awesome-ai-native/docs/team-adoption/)**
Scale AI Native Development across your organization

### 📚 **[Reference Guide →](https://danielmeppiel.github.io/awesome-ai-native/docs/reference/)**
Checklists, progression guides, and documentation links

---

## ⚡ What This Guide Delivers

Your AI interactions are **inconsistent and unreliable**:
- Sometimes Copilot generates brilliant code, other times it's completely off-target
- You waste time re-prompting and re-explaining the same context repeatedly  
- Different requests for similar tasks produce wildly different quality results
- Team members get different AI outputs for the same problems
- You can't predict or control what the AI will focus on

**Sound familiar?** You're experiencing the chaos of unstructured AI interaction.

## The Solution: AI Native Development

**Systematic approach to transform unreliable AI chats into consistent, professional workflows:**

- **Core Technique**: Use structured Markdown to guide AI reasoning (like coding standards for prompts)
- **Agent Primitives**: Build reusable AI configurations that improve over time  
- **Context Engineering**: Optimize AI memory and performance for complex projects
- **Async Delegation**: Scale through GitHub Coding Agents and multi-agent coordination
- **Team Intelligence**: Share successful AI patterns across your organization

### 🧠 Core Mental Model

Each PROSE constraint addresses a specific failure mode:

| Constraint | Failure Mode | Solution |
|------------|--------------|----------|
| **P**rogressive Disclosure | Context overload dilutes attention | Load context just-in-time |
| **R**educed Scope | Scope creep degrades quality | Right-size tasks to context capacity |
| **O**rchestrated Composition | Monolithic prompts collapse | Compose from small primitives |
| **S**coped Boundaries | Unbounded autonomy is unsafe | Define tools, knowledge, approval |
| **E**xplicit Hierarchy | Flat guidance pollutes context | Layer guidance global to local |

---

## 🎯 The Paradigm Shift

*Traditional approach: "Tell the AI what to do"*  
**PROSE approach: "Engineer the context and structure for optimal cognitive performance"**

**Ready to transform your AI development workflow?** Visit the [complete guide](https://danielmeppiel.github.io/awesome-ai-native) to choose your learning path and start building more reliable, consistent AI interactions today.

---

## 📖 Repository Structure

This repository contains the source for the GitHub Pages site:

```
awesome-ai-native/
├── docs/                    # Main guide sections
│   ├── concepts/           # Engineering principles  
│   ├── getting-started/    # Foundation setup
│   ├── workflows/          # Advanced orchestration
│   ├── team-adoption/      # Scaling strategies
│   └── reference/          # Quick lookups
├── _examples/              # Ready-to-use templates
│   ├── instructions/       # Domain-specific guidance
│   ├── chatmodes/         # Role-based AI specialists  
│   ├── prompts/           # Workflow templates
│   └── specifications/    # Implementation blueprints
├── index.md               # Site homepage
└── _config.yml           # Jekyll configuration
```

---

## 🤝 Contributing

We welcome contributions that advance AI Native Development research and practice! Whether you're sharing experimental results, contributing Agent Primitives, or improving documentation—your expertise helps push the boundaries of AI-assisted programming.

**[📖 Read the Contributing Guide →](CONTRIBUTING.md)**

This project is licensed under **CC BY-NC-SA 4.0**, enabling free educational use while supporting sustainable commercial development. Contributors retain copyright to their work and are credited in all derivative applications.

---

## 📄 License

This work is licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](LICENSE).

- ✅ **Free for education, research, and non-commercial use**
- ✅ **Attribution required**  
- ✅ **Derivatives must use same license**
- ❌ **Commercial use requires permission**

For commercial licensing inquiries (corporate training, book publishing, etc.), please contact [@danielmeppiel](https://github.com/danielmeppiel).

---

> 🌟 **Community Resources:** Explore the [Awesome GitHub Copilot](https://github.com/github/awesome-copilot) repository for hundreds of community-contributed instructions, prompts, and chat modes across all major languages and frameworks.



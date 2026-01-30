---
layout: home
title: PROSE - AI-Native Development
permalink: /
---

<div class="hero-section">
  <h1>PROSE</h1>
  <p class="tagline">An architectural style for AI-native development</p>
  
  <div class="prose-acronym">
    <div class="prose-letter">
      <span class="letter">P</span>
      <span class="meaning">rogressive Disclosure</span>
    </div>
    <div class="prose-letter">
      <span class="letter">R</span>
      <span class="meaning">educed Scope</span>
    </div>
    <div class="prose-letter">
      <span class="letter">O</span>
      <span class="meaning">rchestrated Composition</span>
    </div>
    <div class="prose-letter">
      <span class="letter">S</span>
      <span class="meaning">coped Boundaries</span>
    </div>
    <div class="prose-letter">
      <span class="letter">E</span>
      <span class="meaning">xplicit Hierarchy</span>
    </div>
  </div>
</div>

## Learning Path

<div class="learning-paths">
  <a href="docs/prose/" class="path-card">
    <div class="path-title">PROSE Specification</div>
    <div class="path-description">The architectural style for AI-native development—constraints that induce reliability</div>
    <div class="path-meta">10-15 minutes • Theory & Foundation</div>
    <div class="path-link">Learn more</div>
  </a>

  <a href="docs/concepts/" class="path-card">
    <div class="path-title">Core Concepts</div>
    <div class="path-description">The three-layer framework: Prompt Engineering, Agent Primitives, and Context Engineering</div>
    <div class="path-meta">15-20 minutes • Practitioner's Guide</div>
    <div class="path-link">Learn more</div>
  </a>

  <a href="docs/getting-started/" class="path-card">
    <div class="path-title">Getting Started</div>
    <div class="path-description">Set up your first PROSE-compliant project in under 10 minutes</div>
    <div class="path-meta">15-20 minutes • Hands-on Implementation</div>
    <div class="path-link">Learn more</div>
  </a>

  <a href="docs/tooling/" class="path-card">
    <div class="path-title">Tooling</div>
    <div class="path-description">Discover tools, IDE extensions, and CLI utilities for PROSE compliant agents</div>
    <div class="path-meta">12-15 minutes • Infrastructure & Scaling</div>
    <div class="path-link">Learn more</div>
  </a>

  <a href="docs/agent-delegation/" class="path-card">
    <div class="path-title">Agent Delegation</div>
    <div class="path-description">Learn patterns for effective human-AI collaboration and task delegation</div>
    <div class="path-meta">20-25 minutes • Advanced Patterns</div>
    <div class="path-link">Learn more</div>
  </a>

  <a href="docs/team-adoption/" class="path-card">
    <div class="path-title">Team Implementation</div>
    <div class="path-description">Scale PROSE practices across teams and organizations</div>
    <div class="path-meta">15-20 minutes • Team & Leadership</div>
    <div class="path-link">Learn more</div>
  </a>

  <a href="docs/reference/" class="path-card">
    <div class="path-title">Quick Reference</div>
    <div class="path-description">Checklists, guides, and documentation for ongoing reference</div>
    <div class="path-meta">5-10 minutes • Quick Lookups</div>
    <div class="path-link">Learn more</div>
  </a>
</div>

## The Five Constraints

PROSE defines five architectural constraints that guide AI-native development:

| Constraint | Core Idea |
|------------|-----------|
| **Progressive Disclosure** | Load context just-in-time, not just-in-case |
| **Reduced Scope** | Right-size tasks to context capacity |
| **Orchestrated Composition** | Compose simple primitives; complex things collapse |
| **Scoped Boundaries** | Autonomy within guardrails |
| **Explicit Hierarchy** | Layer guidance from global to local |

These constraints emerge from three grounding principles:

1. **Context is finite and fragile** — AI models have limited context windows that degrade with noise
2. **Context must be explicit** — Implicit knowledge doesn't exist for AI; make everything discoverable
3. **Output is probabilistic** — AI produces likely outputs, not guaranteed ones; design for verification

<a href="/docs/prose/" class="cta-button">Read the full PROSE specification →</a>

## Maturity Model

Assess and evolve your AI-native development practices:

<div class="maturity-model">
  <div class="maturity-level level-0">
    <span class="level-number">0</span>
    <div class="level-content">
      <h4>Ad-hoc</h4>
      <p>No structured approach. AI assistance is reactive and inconsistent.</p>
    </div>
  </div>
  
  <div class="maturity-level level-1">
    <span class="level-number">1</span>
    <div class="level-content">
      <h4>Structured</h4>
      <p>Basic primitives in place. Instructions and prompts are documented.</p>
    </div>
  </div>
  
  <div class="maturity-level level-2">
    <span class="level-number">2</span>
    <div class="level-content">
      <h4>Composed</h4>
      <p>Primitives are modular and reusable. Context is managed intentionally.</p>
    </div>
  </div>
  
  <div class="maturity-level level-3">
    <span class="level-number">3</span>
    <div class="level-content">
      <h4>Orchestrated</h4>
      <p>Workflows chain primitives. AI agents operate within defined boundaries.</p>
    </div>
  </div>
  
  <div class="maturity-level level-4">
    <span class="level-number">4</span>
    <div class="level-content">
      <h4>Distributed</h4>
      <p>Cross-repo sharing. Organization-wide standards with local adaptation.</p>
    </div>
  </div>
</div>

## Contributing

PROSE is an open specification shaped by the community. Whether you're refining constraints, sharing patterns, or building tooling—your contributions matter.

<div class="cta-buttons">
  <a href="docs/concepts/" class="btn-primary">Read the Guide →</a>
  <a href="https://github.com/danielmeppiel/awesome-ai-native/blob/main/CONTRIBUTING.md" class="github-btn"><span class="github-text">Contribute →</span></a>
</div>
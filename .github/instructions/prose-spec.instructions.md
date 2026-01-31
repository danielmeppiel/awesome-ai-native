---
applyTo: "**/prose/**/*.md, **/PROSE*.md"
description: "Guidelines for editing PROSE specification documents"
---

# PROSE Specification Editing Guidelines

When editing PROSE specification documents, follow these rules to maintain consistency and rigor.

## Reference

All constraint definitions live in: [PROSE Spec](../../docs/prose/index.md)

## Rules

1. **Constraint Consistency** - New content must align with existing PROSE constraints (Progressive Disclosure, Reduced Scope, Orchestrated Composition, Safety Boundaries, Explicit Hierarchy)

2. **Example Updates** - When adding or modifying concepts, provide concrete examples that demonstrate the principle

3. **Academic Tone** - PROSE specs are reference documents; maintain a rigorous, precise writing style

4. **Link Don't Duplicate** - Reference existing definitions rather than restating them

5. **Version Awareness** - Note which PROSE version (e.g., v0.1) a change applies to

## Validation

Before committing changes:
- [ ] New content does not contradict existing constraints
- [ ] Cross-references are valid and up-to-date
- [ ] Examples compile/work if code is included
- [ ] Changes are noted in changelog if breaking

## Anti-patterns

- Adding constraints without clear rationale
- Duplicating definitions across documents
- Breaking backward compatibility without migration path
- Over-engineering simple concepts

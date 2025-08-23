---
title: "Frontend Development Instructions"
category: instructions
layout: page
---

# Frontend Development Instructions

## File Configuration
Create your `.github/instructions/frontend.instructions.md` file:

```yaml
---
applyTo: "**/*.{jsx,tsx,css,scss,html}"
description: "Frontend development guidelines with React and TypeScript focus"
---
```

## Context Loading
Before starting frontend development, review:
- [Design system documentation](../docs/design-system.md)
- [Component library patterns](../src/components/README.md) 
- [Accessibility guidelines](../docs/accessibility.md)

## Core Requirements

### React Component Standards
- Use functional components with TypeScript
- Implement proper prop validation with TypeScript interfaces
- Follow component composition patterns over inheritance
- Use React hooks for state management and side effects

### Code Structure
Generate components with:
- [ ] TypeScript interfaces for all props
- [ ] JSDoc comments for component purpose and usage
- [ ] Accessibility attributes (ARIA labels, roles)
- [ ] Error boundaries for complex components
- [ ] Unit tests in `__tests__/` directory

### Styling Guidelines
- Use CSS Modules or styled-components for component styling
- Follow mobile-first responsive design principles
- Implement dark/light theme support through CSS custom properties
- Ensure WCAG 2.1 AA compliance for color contrast and navigation

### Performance Optimization
- Implement lazy loading for route-based code splitting
- Use React.memo() for expensive component re-renders
- Optimize images with next/image or similar optimization tools
- Minimize bundle size through tree shaking and dead code elimination

## Validation Checkpoints
Before submitting frontend code:
- [ ] Components render correctly across target browsers
- [ ] Responsive design works on mobile, tablet, and desktop
- [ ] Accessibility tested with screen reader
- [ ] Performance metrics meet project benchmarks
- [ ] Unit tests achieve >90% coverage

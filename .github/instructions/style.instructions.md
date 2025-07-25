---
applyTo: "**/*.scss, **/*.css"
---

# GitHub Primer-Inspired Design System

Follow these principles when working with styles to maintain elegant, professional design:

## Color Palette
- Use muted colors over bright, flashy ones
- Primary: `#0969da` (GitHub blue) instead of bright blues
- Text: `#24292f` (primary), `#656d76` (secondary), `#8c959f` (muted)
- Backgrounds: `#ffffff`, `#f6f8fa`, `#f1f3f4` (subtle grays)
- Borders: `#d0d7de`, `#d8dee4`, `#e1e4e8` (GitHub's signature grays)

## Design Philosophy
- **Subtlety over Flash**: Avoid gradients, bright colors, and dramatic effects
- **Clean Interactions**: Use gentle hover effects (border changes, subtle shadows)
- **Professional Typography**: No gradient text, colorful headings, or flashy treatments
- **Minimal Shadows**: Use `rgba(27, 31, 35, 0.04)` for subtle depth
- **Consistent Borders**: 1px borders with GitHub's signature colors

## Component Guidelines
- **Cards**: 8px border radius, subtle shadows, gentle hover effects
- **Headers**: Clean backgrounds, avoid gradients
- **Code**: Muted backgrounds (`#f1f3f4`), no bright accent colors
- **Buttons**: GitHub's blue with subtle hover states
- **Lists**: Proper indentation (`padding-left: 24px`), consistent spacing
- **Spacing**: Maintain clean spacing without excessive padding

## List Styling Rules
- Use `padding-left: 24px` for proper bullet indentation
- Set `margin-bottom: 8px` for list items
- Handle nested lists with `padding-left: 20px`
- Fix first/last element spacing in containers with `:first-child` and `:last-child`

## Content Card Usage
- Only use `.content-card` for functional groupings (grids, problem/solution sections)
- Remove unnecessary card wrappers around regular content
- Cards should enhance content structure, not add visual noise
- Use colored left borders (`border-left: 4px solid`) for semantic distinctions

## Anti-Patterns to Avoid
- Bright primary colors (`#2563eb`, `#7c3aed`)
- Transform animations (`translateY`, dramatic scaling)
- Gradient backgrounds and text effects
- Heavy shadows and dramatic hover effects
- Flashy color combinations

Keep it clean, professional, and GitHub-like.

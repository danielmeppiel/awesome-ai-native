---
applyTo: "**/*.scss, **/*.css"
---

# GitHub Primer-Inspired Design System

Follow these principles when working with styles to maintain elegant, professional design.

**Reference**: Study the official [GitHub Primer Product UI](https://primer.style/product/) for current design patterns and component examples.

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
- **Cards**: 12px border radius, subtle shadows, gentle hover effects
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

## Professional Card Design Meta-Learnings

### 🎯 Implementation Guidelines
When creating card layouts:
1. **Study Primer first**: Reference https://primer.style/product/ for current patterns
2. **Content over decoration**: Focus on clear information hierarchy
3. **Professional tone**: Remove emojis, use descriptive titles
4. **Subtle interactions**: Gentle hover states, no dramatic effects
5. **Consistent spacing**: 24px gaps, proper internal padding
6. **Typography hierarchy**: Clear but not heavy font weights

## Primer-Compliant Comparison Layouts

### ✅ River-Style Comparisons
For before/after or paradigm shift content, use side-by-side layouts inspired by Primer Brand's River component:

**Structure:**
- Grid layout with proper spacing (32px gaps)
- Each section in subtle card containers (12px radius, light borders)
- Semantic left border colors (red for problems, green for solutions)
- Central divider with clean arrow indicator
- Mobile-responsive stacking

**Typography:**
- Headers: 1.125rem, 600 weight
- Subtitles in secondary color
- Clean bullet points with custom styling
- Result sections in subtle background boxes

### ❌ Heavy Card Anti-Patterns
- Don't wrap regular content sections in `.content-card`
- Avoid colored left borders on general content
- Don't use cards for simple text comparisons
- Avoid heavy visual treatments for flowing content

## Enhanced Code Styling

Following Primer Brand theming patterns:

**Inline Code:**
```scss
code {
  background: #f6f8fa;
  color: #24292f;
  border: 1px solid #d8dee4;
  border-radius: 6px;
  padding: 2px 6px;
  font-family: 'SFMono-Regular', 'Consolas', monospace;
}
```

**Code Blocks:**
```scss
pre {
  background: #f6f8fa;
  border: 1px solid #d8dee4;
  border-radius: 8px;
  padding: 16px;
}
```

These follow GitHub's native code styling with proper contrast and subtle borders.

### ❌ Anti-Patterns for Cards
- Emoji icons or decorative elements in card titles
- Button-style "Call to Action" links with background colors
- Heavy borders or dramatic color changes on hover
- Excessive font weights (700+) for titles
- Dense padding or cramped spacing
- Flashy or attention-grabbing visual elements

## Meta-Design Philosophy
When visual elements feel heavy or inelegant, replace structural divisions (borders, lines) with spatial relationships and subtle background changes. Study GitHub Primer's approach to visual hierarchy: they achieve separation through intelligent spacing, gentle hover states, and minimal visual noise. Instead of adding visual elements, remove them and let whitespace, subtle opacity changes, and consistent spacing patterns create the structure.

## Anti-Patterns to Avoid
- Bright primary colors (`#2563eb`, `#7c3aed`)
- Transform animations (`translateY`, dramatic scaling)
- Gradient backgrounds and text effects
- Heavy shadows and dramatic hover effects
- Flashy color combinations
- Thick border separators in navigation (use spacing instead)

Keep it clean, professional, and GitHub-like.

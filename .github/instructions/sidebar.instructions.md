---
applyTo: "_layouts/docs.html"
description: "Documentation sidebar navigation principles and consistency guidelines"
---

# Documentation Sidebar Navigation Guidelines

## Core Principles

### 1. Content-First Navigation
- **ALWAYS** verify actual page content before updating sidebar links
- **NEVER** use placeholder or assumed section names
- Use `grep_search` with regex `^## |^# ` to identify all major headings
- Match sidebar anchors exactly to the auto-generated heading IDs in the markdown

### 2. Comprehensive Section Coverage
- Include ALL major `## ` level sections from each documentation page
- Don't omit important sections like "Key Takeaways", "Success Metrics", "Implementation Roadmap"
- Maintain logical reading order that matches the page structure
- Include both primary content sections AND concluding sections

### 3. Link Styling Isolation
- Sidebar navigation links MUST be excluded from general content link styling
- Use specific exclusions in CSS selectors: `:not(.nav-main-link):not(.nav-sub-link):not(.edit-link)`
- Prevent "90s style" blue underlined links in navigation by maintaining styling boundaries
- Navigation should have clean, professional GitHub Primer styling without content link interference

## Implementation Rules

### Anchor ID Verification Process
1. **Search for headings**: Use `grep_search` with pattern `^## ` on target markdown file
2. **Verify anchor format**: Markdown headings auto-convert to lowercase, spaces become hyphens, special chars become hyphens
3. **Test actual links**: Ensure anchors work with the Jekyll markdown processor
4. **Include emoji prefixes**: Many sections use emoji prefixes like `🚀`, `🎯`, `📈` - include the full anchor

### Section Prioritization
**Always Include These Common Sections:**
- Main lettered sections (A., B., C., D.)
- Quick Start Checklist / Implementation steps
- Key Takeaways (crucial for user understanding)
- Success Metrics (important for team adoption)
- Implementation Roadmap (essential for planning)
- What's Next / Next Steps (guides user journey)

### CSS Styling Requirements
**Navigation Link Exclusions:**
```scss
// CORRECT: Exclude navigation from content link styling
.page-content a:not(.path-link):not(.nav-main-link):not(.nav-sub-link):not(.edit-link) {
  color: var(--primary-color);
  text-decoration: underline;
}

// WRONG: Don't let navigation inherit content link styles
.page-content a:not(.path-link) {
  // This affects sidebar navigation
}
```

**Navigation Specific Styling:**
- Use `var(--text-primary)` for main navigation links
- Use `var(--text-secondary)` for sub-navigation links
- Maintain hover states with `var(--bg-secondary)` background
- No underlines on navigation elements - clean, button-like appearance

## Quality Assurance Checklist

### Before Updating Sidebar Navigation:
- [ ] **Content Audit**: Read through entire target page to identify ALL major sections
- [ ] **Anchor Verification**: Test that anchor links actually work with Jekyll's markdown processing
- [ ] **Completeness Check**: Ensure no important sections are omitted (especially concluding sections)
- [ ] **Styling Isolation**: Verify navigation links don't inherit unwanted content styling
- [ ] **User Experience**: Navigation should provide comprehensive page overview and easy jumping between sections

### Common Mistakes to Avoid:
- ❌ **Assumption-based navigation**: Don't guess what sections exist
- ❌ **Incomplete coverage**: Don't omit "less important" sections like Key Takeaways
- ❌ **Styling conflicts**: Don't let sidebar inherit content link styling (blue underlines)
- ❌ **Broken anchors**: Don't use anchors that don't match Jekyll's auto-generation
- ❌ **Inconsistent patterns**: Maintain same level of detail across all documentation sections

## Testing Approach

### Verification Steps:
1. **Visual Check**: Sidebar should have clean, professional appearance without blue underlines
2. **Functional Check**: All sidebar links should jump to correct page sections
3. **Completeness Check**: Compare sidebar to actual page content - should cover all major sections
4. **Consistency Check**: All documentation pages should have similar levels of sidebar detail

### Success Criteria:
- Navigation provides comprehensive page overview
- All links work correctly and jump to intended sections
- Clean, professional styling consistent with GitHub Primer design system
- No unwanted styling inheritance from content link rules
- Users can easily navigate through entire documentation structure

## Maintenance Guidelines

- **When adding new documentation pages**: Follow same comprehensive approach to sidebar creation
- **When updating existing pages**: Always verify sidebar still matches actual content structure
- **When modifying CSS**: Ensure navigation styling isolation is maintained
- **When reviewing changes**: Check that all major sections are represented in navigation

Remember: The sidebar is a crucial UX element that helps users understand and navigate complex documentation. Invest the time to make it comprehensive and accurate rather than rushed or incomplete.

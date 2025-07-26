---
applyTo: "**/*.md"
---

# Markdown Content Guidelines

Keep content clean, structured, and professional. Avoid visual clutter.

## Content Card Usage

### ✅ Use Content Cards For:
- **Problem/Solution sections**: With colored left borders for semantic distinction
  ```html
  <div class="content-card" style="border-left: 4px solid #ef4444;" markdown="1">
  ### ❌ Problem Section
  </div>
  
  <div class="content-card" style="border-left: 4px solid #10b981;" markdown="1">
  ### ✅ Solution Section
  </div>
  ```
- **Grid layouts**: Learning paths, feature cards, structured collections
- **Special callouts**: When the card adds functional value

### ❌ Don't Use Content Cards For:
- Regular text sections
- Basic headings and paragraphs
- Generic content that doesn't need visual grouping
- Lists and standard markdown content

## Content Structure

### Lists
- Use proper markdown list syntax
- Maintain consistent indentation
- Keep list items concise and scannable

### Headings
- Use semantic heading hierarchy (h1 → h2 → h3)
- First heading should not have excessive top margin
- Keep headings descriptive and actionable

### Sections
- Use `---` for section breaks when needed
- Group related content logically
- Avoid unnecessary visual separators

## Writing Style
- **Be concise**: Remove unnecessary words
- **Be actionable**: Tell users what to do
- **Be scannable**: Use lists, headings, and short paragraphs
- **Be consistent**: Follow established patterns
- **Use flowing prose**: Prefer narrative paragraphs over excessive bullets, bolds, and formatting. Bullet points are important but should be used sparingly to highlight key points, not as a primary content structure.
- **Create bridges**: Connect concepts with transitional paragraphs that show progression
- **Write conversationally**: Sound like an experienced practitioner, not a specification document

## Anti-Patterns
- Wrapping every section in content cards
- Excessive visual decorations
- Inconsistent heading structures
- Walls of text without breaks

## Sidebar Maintenance
When adding or modifying content structure in documentation:

**For existing pages** - adding/modifying top-level sections (`## ` headers):
- **MUST** update the corresponding sidebar navigation in `_layouts/docs.html`
- Add new sections to the appropriate `nav-subsection` list
- Ensure anchor links match the auto-generated heading IDs

**For new pages** - creating new `index.md` files:
- **MUST** add a new navigation section to `_layouts/docs.html`
- Create complete `nav-subsection` with all major headings from the new page
- Follow the established pattern with proper icons, URLs, and expand/collapse functionality

Follow the comprehensive guidelines in `sidebar.instructions.md` for both scenarios.

Keep it simple, functional, and user-focused.

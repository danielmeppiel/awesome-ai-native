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

## Anti-Patterns
- Wrapping every section in content cards
- Excessive visual decorations
- Inconsistent heading structures
- Walls of text without breaks

Keep it simple, functional, and user-focused.

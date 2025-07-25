---
title: "Code Review Prompt Template"
category: prompts
layout: page
---

# Systematic Code Review Workflow

## File Configuration
```yaml
---
mode: agent
model: gpt-4
tools: ['codebase', 'search', 'problems', 'changes']
description: 'Comprehensive code review with security, performance, and maintainability focus'
---
```

# Code Review Workflow

## Context Loading Phase
1. Review [coding standards](../../docs/coding-standards.md) for this project
2. Load [security guidelines](../../docs/security-guidelines.md) for vulnerability assessment
3. Check [performance benchmarks](../../docs/performance-requirements.md) for optimization opportunities

## Review Categories

### 1. Code Quality Assessment
Evaluate the code for:
- [ ] Adherence to project coding standards and style guide
- [ ] Proper error handling and edge case coverage
- [ ] Code readability and maintainability
- [ ] Appropriate use of design patterns and architectural principles

### 2. Security Analysis  
Check for common vulnerabilities:
- [ ] Input validation and sanitization
- [ ] SQL injection and XSS prevention
- [ ] Authentication and authorization implementation
- [ ] Sensitive data handling and encryption

### 3. Performance Review
Assess performance implications:
- [ ] Algorithm efficiency and complexity analysis
- [ ] Database query optimization opportunities
- [ ] Memory usage and potential leaks
- [ ] Caching strategies and implementation

### 4. Testing Coverage
Validate testing approach:
- [ ] Unit test coverage for critical paths
- [ ] Integration test scenarios
- [ ] Error condition testing
- [ ] Performance and load testing considerations

## Human Validation Gate
🚨 **STOP**: Present review findings summary before detailed analysis.
Required from user:
- [ ] Confirmation of review scope and priorities
- [ ] Agreement on critical vs. minor issue classification
- [ ] Approval to proceed with detailed recommendations

## Review Output Structure
Provide findings in this format:

### Critical Issues (Must Fix)
- **Issue**: [Description]
- **Risk**: [Security/Performance/Maintainability impact]
- **Solution**: [Specific remediation steps]
- **Code Location**: [File and line references]

### Recommendations (Should Fix)
- **Improvement**: [Description] 
- **Benefit**: [Expected improvement]
- **Implementation**: [Suggested approach]

### Observations (Consider)
- **Pattern**: [Code pattern observed]
- **Alternative**: [Potential improvement]
- **Trade-off**: [Costs and benefits]

## Post-Review Actions
After completing review:
- Update [review patterns](../../docs/review-patterns.md) with new findings
- Add discovered anti-patterns to [code guidelines](../../docs/anti-patterns.md)
- Schedule follow-up review if critical issues found

---
title: "API Endpoint Specification Template"
category: specifications
layout: page
---

# API Endpoint Specification Template

Use this template for creating implementation-ready API endpoint specifications.

```markdown
# API Endpoint: [Endpoint Name]

## Problem Statement
[Describe the business need this endpoint addresses]

## Endpoint Details
- **Method**: [GET|POST|PUT|PATCH|DELETE]
- **Path**: `/api/v1/[resource-path]`
- **Authentication**: [Required|Optional|None]
- **Rate Limiting**: [requests/minute]

## Request Specification

### Path Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| id | string | Yes | Unique resource identifier |

### Query Parameters  
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| limit | integer | No | 20 | Number of results to return |
| offset | integer | No | 0 | Number of results to skip |

### Request Body
```json
{
  "field1": "string (required)",
  "field2": "integer (optional)",
  "nested": {
    "field3": "boolean (required)"
  }
}
```

## Response Specification

### Success Response (200)
```json
{
  "success": true,
  "data": {
    "id": "string",
    "field1": "string",
    "created_at": "2024-01-01T00:00:00Z"
  },
  "meta": {
    "total": 100,
    "limit": 20,
    "offset": 0
  }
}
```

### Error Responses
- **400 Bad Request**: Invalid request parameters
- **401 Unauthorized**: Authentication required
- **403 Forbidden**: Insufficient permissions
- **404 Not Found**: Resource not found
- **429 Too Many Requests**: Rate limit exceeded
- **500 Internal Server Error**: Server error

## Implementation Requirements

### Core Logic
- [ ] Input validation for all parameters
- [ ] Business logic implementation
- [ ] Data persistence/retrieval
- [ ] Response formatting

### Security Requirements
- [ ] Authentication verification
- [ ] Authorization checks
- [ ] Input sanitization
- [ ] Rate limiting implementation

### Performance Requirements
- [ ] Response time < 200ms for typical requests
- [ ] Database query optimization
- [ ] Caching strategy implementation
- [ ] Connection pooling

### Testing Requirements
- [ ] Unit tests for business logic (>90% coverage)
- [ ] Integration tests for full endpoint flow
- [ ] Security testing for common vulnerabilities
- [ ] Performance testing under load

## Context References
- API standards: [REST conventions](../../docs/api-standards.md)
- Security patterns: [Authentication flows](../../docs/auth-patterns.md)
- Database schemas: [Data models](../../docs/database-schema.md)

## Validation Criteria
- [ ] All request/response schemas validated
- [ ] Error handling covers all edge cases
- [ ] Security requirements implemented and tested
- [ ] Performance benchmarks met
- [ ] Documentation updated

## Implementation Notes
[Any additional context, constraints, or implementation details]

## Handoff Checklist
- [ ] Technical design reviewed and approved
- [ ] Database changes planned and documented
- [ ] Security review completed
- [ ] Performance requirements validated
- [ ] Ready for implementation assignment
```

## Usage Instructions

1. **Copy this template** for each new API endpoint
2. **Fill in all sections** with specific requirements
3. **Review with team** before implementation begins
4. **Use as reference** during development and testing
5. **Update based on implementation discoveries**

This template ensures consistent, implementation-ready API specifications that reduce ambiguity and improve development velocity.

# Contract: {Feature Name} - API Contract

> Backend API Specification

---

## Metadata

| Item | Content |
|-----|------|
| Feature ID | {feature-id} |
| Feature Name | {Feature Name} |
| Backend Owner | @{username} |
| Created Date | {YYYY-MM-DD} |
| Status | ⚪ Draft / 🔵 Review / ✅ Approved |
| Version | 1.0.0 |
| Spec Reference | [spec.md](./spec.md) |

---

## Related Documents

| Type | Document | Status |
|------|----------|:------:|
| PRD | [{Feature Name}.md](../../prd/ph{X}/{feature-name}.md) | ✅ |
| Feature Spec | [spec.md](./spec.md) | ✅ |
| Acceptance | [acceptance.md](./acceptance.md) | 🔵 |

---

## Open Items

| Item | Owner | Status |
|------|-------|:------:|
| Confirm authentication method (JWT / Session) | @Backend | 🔵 |
| Rate Limiting specific values | @Backend | 🔵 |
| {Item to confirm} | @{owner} | 🔵 |

---

## 1. Overview

This document defines the API contract for {Feature Name}.

{Feature description}

---

## 2. Data Schema

### 2.1 Enums

#### {EnumName}

{Enum description}

| Value | Description |
|-------|-------------|
| `value1` | {Description} |
| `value2` | {Description} |

---

### 2.2 Entities

#### {EntityName}

{Entity description}

| Field | Type | Required | Description | Default | Example |
|-------|------|:--------:|-------------|---------|---------|
| id | string | ✓ | Unique identifier | - | `"entity_abc123"` |
| name | string | ✓ | Name | - | `"Example Name"` |
| status | {EnumName} | ✓ | Status | `"active"` | `"active"` |
| createdAt | datetime | ✓ | Created time | - | `"2026-01-22T10:30:00Z"` |
| updatedAt | datetime | ✓ | Updated time | - | `"2026-01-22T10:30:00Z"` |

**Example:**
```json
{
  "id": "entity_abc123",
  "name": "Example Name",
  "status": "active",
  "createdAt": "2026-01-22T10:30:00Z",
  "updatedAt": "2026-01-22T10:30:00Z"
}
```

---

## 3. API Endpoints

### 3.1 {API Name}

{API description}

**Endpoint**
```
GET /api/v1/{resource}
```

**Authentication**
- Required: ✓ / -
- Type: Bearer Token

**Request**

| Param | Location | Type | Required | Description | Example |
|-------|----------|------|:--------:|-------------|---------|
| Authorization | header | string | ✓ | Bearer {token} | `"Bearer eyJ..."` |
| {param} | query | string | - | {Description} | `"value"` |

**Response - Success (200)**

```json
{
  "success": true,
  "data": {
    "items": [],
    "pagination": {
      "hasMore": false,
      "nextCursor": null
    }
  }
}
```

**Response - Errors**

| HTTP | Code | Description | Frontend Handling |
|------|------|-------------|-------------------|
| 400 | `INVALID_REQUEST` | Invalid request format | Show error message |
| 401 | `UNAUTHORIZED` | Unauthorized or invalid token | Redirect to login |
| 404 | `NOT_FOUND` | Resource not found | Show "Not found" |
| 429 | `RATE_LIMITED` | Too many requests | Delay and retry |
| 500 | `INTERNAL_ERROR` | Server error | Show "System error" |

**Performance**

| Metric | Target |
|--------|--------|
| P50 | < 100ms |
| P95 | < 200ms |
| P99 | < 500ms |

---

### 3.2 {Another API}

...

---

## 4. Error Codes

### 4.1 Error Response Format

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable error message",
    "details": {}
  }
}
```

### 4.2 Error Code List

| Code | HTTP | Description | Frontend Handling |
|------|------|-------------|-------------------|
| `UNAUTHORIZED` | 401 | Unauthorized or invalid token | Clear local token, redirect to login |
| `FORBIDDEN` | 403 | No permission for this action | Show "No permission" |
| `NOT_FOUND` | 404 | Resource not found | Show "Not found" |
| `VALIDATION_ERROR` | 400 | Request validation failed | Show specific field errors |
| `RATE_LIMITED` | 429 | Too many requests | Show "Please try again later", delay retry |
| `INTERNAL_ERROR` | 500 | Internal server error | Show "System error" |

---

## 5. Security Considerations

| Item | Description |
|-----|------|
| Authentication | All APIs require valid Bearer Token |
| Authorization | Users can only access their own data |
| Rate Limiting | Max {N} requests per minute per user |
| Input Validation | Strictly validate all input parameters |

---

## 6. Implementation Notes

### 6.1 Frontend Implementation Notes

{Frontend implementation notes}

### 6.2 Offline Handling

| Operation | Handling |
|-----|---------|
| Read data | Use local cache |
| Modify data | Store locally + mark for sync |
| Connection restored | Background sync pending items |

---

## 7. Out of Scope

The following items are not covered in this contract:

| Item | Reason | Related Document |
|-----|------|---------|
| {Item} | {Reason} | {Related document or TBD} |

---

## Changelog

| Version | Date | Changes | Author |
|-----|------|---------|------|
| 1.0.0 | {date} | Initial version | @{backend} |

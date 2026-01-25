# Delta Spec: Product Search - Add Search History

> Sprint Change Specification

---

## Metadata

| Item | Content |
|-----|------|
| Sprint | Sprint-2 |
| Type | 🔄 Change |
| Owner | @pd-sarah |
| Status | ✅ Done |
| Base → Target | 1.0.0 → 1.1.0 |

---

## Change Summary

**Goal**: Add search history feature so users can quickly re-search previous queries.

| Type | Count | Description |
|:---:|:----:|------|
| [NEW] | 3 | Search history dropdown, history API, clear history button |
| [MODIFIED] | 2 | Search input component, search result page layout |
| [REMOVED] | 0 | - |

---

## Open Items

| # | Item | Owner | Status |
|:-:|------|-------|:----:|
| 1 | ~~Max history items to store~~ | @pm-david | ✅ Resolved: 20 items |
| 2 | ~~Store on device or server~~ | @backend-tom | ✅ Resolved: Server-side |

---

## Detailed Changes

### [NEW] Search History Dropdown

**Description**: Display user's recent search queries below the search input.

**Specifications**:

| Item | Specification |
|------|---------------|
| Trigger | Focus on search input |
| Max items | 20 most recent |
| Item display | Query text + search time |
| Actions | Click to search, swipe to delete |

**UI Layout**:

```
┌─────────────────────────────┐
│   ┌─────────────────────┐   │
│   │ 🔍 Search...        │   │
│   └─────────────────────┘   │
│   ┌─────────────────────┐   │
│   │ Recent Searches     │   │
│   ├─────────────────────┤   │
│   │ 🕐 iPhone 15    [×] │   │
│   │ 🕐 MacBook Pro  [×] │   │
│   │ 🕐 AirPods      [×] │   │
│   ├─────────────────────┤   │
│   │ Clear All History   │   │
│   └─────────────────────┘   │
└─────────────────────────────┘
```

### [NEW] Search History API

**Endpoint**: `GET /api/search/history`

| Field | Type | Description |
|-------|------|-------------|
| items | array | List of search history |
| items[].query | string | Search query text |
| items[].timestamp | datetime | Search time |
| items[].resultCount | number | Number of results found |

**Endpoint**: `DELETE /api/search/history`

| Field | Type | Description |
|-------|------|-------------|
| query | string? | Specific query to delete (optional) |
| all | boolean? | Delete all history |

### [NEW] Clear History Button

**Location**: Bottom of history dropdown

**Behavior**:
1. Show confirmation dialog
2. Call DELETE /api/search/history?all=true
3. Close dropdown
4. Show success toast

### [MODIFIED] Search Input Component

| Before | After |
|--------|-------|
| Simple text input | Text input with history dropdown on focus |
| No dropdown | Shows history dropdown when focused and empty |
| - | Hide dropdown when typing |

**Reason**: Need to integrate history feature with existing search input.

### [MODIFIED] Search Result Page Layout

| Before | After |
|--------|-------|
| Results only | Results + "Save to history" indicator |
| No feedback | Show checkmark when query saved |

**Reason**: Provide feedback that search query was saved to history.

---

## Impact Analysis

| Document | Section | Change Type |
|------|------|:--------:|
| spec.md | Search Input Component | [MODIFIED] |
| spec.md | Page States | [MODIFIED] |
| spec.md | Add History Dropdown section | [NEW] |
| contract.md | Add /api/search/history | [NEW] |
| acceptance.md | TC-010 ~ TC-015 | [NEW] |

---

## Pre-merge Checklist

- [x] All open items resolved
- [x] contract.md updated
- [x] acceptance.md updated
- [x] No critical bugs

---

## Changelog

| Date | Change | Author |
|-----|------|------|
| 2024-02-01 | Initial version | @pd-sarah |
| 2024-02-03 | Resolved open items | @pd-sarah |
| 2024-02-10 | Ready for merge | @pd-sarah |

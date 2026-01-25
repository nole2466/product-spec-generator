# Example: Delta Spec - Add Search History

This example demonstrates how to write a Delta Spec for modifying an existing feature.

## Scenario

The product search feature (see `examples/product-search/`) is already in production. In Sprint-2, we need to add a "Search History" feature.

## File Structure

```
delta-spec/
├── README.md                 # You are here
└── delta-search-history.md   # Delta Spec example
```

## Key Concepts

### What is a Delta Spec?

A Delta Spec documents **changes** to an existing feature during a Sprint, rather than writing a complete new spec. It uses markers to indicate what's being changed:

| Marker | Description |
|:---:|------|
| `[NEW]` | New addition |
| `[MODIFIED]` | Change to existing item (must show Before/After) |
| `[REMOVED]` | Removed item |

### When to Use Delta Spec

| Scenario | Use |
|----------|-----|
| New feature (no existing spec) | `spec.md` |
| Modify existing feature | `delta.md` |
| Bug fix | `delta.md` |

### Sprint Workflow

```
Product Backlog     →     Sprint Backlog     →     Source of Truth
(PRD)                     (delta.md)              (spec.md)
```

## Learning Points

### 1. Change Summary

Always start with a clear summary of what's changing:

```markdown
| Type | Count | Description |
|:---:|:----:|------|
| [NEW] | 3 | Search history feature |
| [MODIFIED] | 2 | Search input, result page |
| [REMOVED] | 0 | - |
```

### 2. Before/After for Modifications

When modifying existing items, always show what's changing:

```markdown
| Before | After |
|--------|-------|
| Search input only | Search input + history dropdown |
```

### 3. Impact Analysis

List all documents that need updating:

```markdown
| Document | Section | Change Type |
|------|------|:--------:|
| spec.md | Search Input | [MODIFIED] |
| contract.md | /api/search/history | [NEW] |
| acceptance.md | TC-010~012 | [NEW] |
```

### 4. Pre-merge Checklist

Before merging to Source of Truth:

- [ ] All open items resolved
- [ ] contract.md updated
- [ ] acceptance.md updated
- [ ] No critical bugs

## Related Files

- [Delta Spec Example](./delta-search-history.md)
- [Product Search Example](../product-search/)
- [Delta Template (Chinese)](../../templates/delta.md)
- [Delta Template (English)](../../templates/en/delta.md)

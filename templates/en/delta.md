# Delta Spec: {Feature Name}

> Sprint Change Specification

---

## Metadata

| Item | Content |
|-----|------|
| Sprint | Sprint-{X} |
| Type | 🆕 New / 🔄 Change / 🐛 Fix |
| Owner | @{username} |
| Status | ⚪ Draft / 🔵 Review / ✅ Done |
| Base → Target | 1.0.0 → 1.1.0 |

---

## Change Summary

**Goal**: {One sentence describing what this change aims to achieve}

| Type | Count | Description |
|:---:|:----:|------|
| [NEW] | {n} | {Brief description} |
| [MODIFIED] | {n} | {Brief description} |
| [REMOVED] | {n} | {Brief description} |

---

## Open Items

| # | Item | Owner | Status |
|:-:|------|-------|:----:|
| 1 | {Item to confirm} | @{who} | 🔵 |

---

## Detailed Changes

### [NEW] {New Item Name}

{Describe what is being added}

### [MODIFIED] {Modified Item Name}

| Before | After |
|--------|-------|
| {Original} | {Modified} |

**Reason**: {Explain why this change is needed}

### [REMOVED] {Removed Item Name}

**Reason**: {Explain why this is being removed}

---

## Impact Analysis

| Document | Section | Change Type |
|------|------|:--------:|
| spec.md | {Section} | [MODIFIED] |
| contract.md | {endpoint} | [NEW] |
| acceptance.md | TC-XXX | [MODIFIED] |

---

## Pre-merge Checklist

- [ ] All open items resolved
- [ ] contract.md updated
- [ ] acceptance.md updated
- [ ] No critical bugs

---

## Changelog

| Date | Change | Author |
|-----|------|------|
| {date} | Initial version | @pd |

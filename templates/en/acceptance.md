# Acceptance: {Feature Name}

> Acceptance Criteria Document

---

## Metadata

| Item | Content |
|-----|------|
| Feature ID | {feature-id} |
| Feature Name | {Feature Name} |
| QA Owner | @{username} |
| Created Date | {YYYY-MM-DD} |
| Status | ⚪ Draft / 🔵 Review / ✅ Approved |
| Version | 1.0.0 |
| Spec Reference | [spec.md](./spec.md) |

---

## Related Documents

| Type | Document | Status |
|------|----------|:------:|
| PRD | [{Feature Name}.md](../../prd/ph{X}/{feature-name}.md) | ✅ |
| Spec | [spec.md](./spec.md) | ✅ |
| Contract | [contract.md](./contract.md) | ✅ |

---

## Open Items

| # | Type | Item | Owner | Status | Note |
|:-:|:---:|------|-------|:----:|------|
| 1 | Pending | Test accounts | @QA | 🔵 | - |
| 2 | Dependency | Test environment | @Backend | 🔵 | - |

---

## 1. Test Scope

### 1.1 In Scope

- {Test item 1}
- {Test item 2}

### 1.2 Out of Scope

- {Excluded item 1}
- {Excluded item 2}

---

## 2. Test Environment

| Item | Specification |
|-----|------|
| Environment | Staging |
| API Version | v1 |
| Test Data | Test accounts |

### Test Accounts

| Account | Password | Role | Purpose |
|-----|------|------|------|
| test@example.com | ******* | Regular user | Basic function testing |
| admin@example.com | ******* | Admin | Permission testing |

---

## 3. Test Coverage Matrix

| Test Item | TC ID | Flow | UI State | API | Error Handling | Result |
|---------|-------|:--------:|:--------:|:---:|:--------:|:----:|
| {Item 1} | TC-FL-001 | ✅ | ✅ | ✅ | ✅ | ⬜ |
| {Item 2} | TC-FL-002 | ✅ | ✅ | ✅ | ✅ | ⬜ |
| {UI State} | TC-UI-001 | - | ✅ | - | - | ⬜ |
| {Error} | TC-ERR-001 | - | ✅ | - | ✅ | ⬜ |

---

## 4. Functional Flow Tests

### TC-FL-001: {Test Case Name}

| Item | Content |
|-----|------|
| **Preconditions** | {Conditions} |
| **Test Steps** | See below |
| **Expected Result** | {Result} |
| **Priority** | P0 |

**Test Steps**:
1. {Step 1}
2. {Step 2}
3. {Step 3}

**Expected Results**:
- {Expected result 1}
- {Expected result 2}

---

### TC-FL-002: {Test Case Name}

| Item | Content |
|-----|------|
| **Preconditions** | {Conditions} |
| **Test Steps** | See below |
| **Expected Result** | {Result} |
| **Priority** | P0 |

**Test Steps**:
1. {Step 1}
2. {Step 2}

**Expected Results**:
- {Expected result}

---

## 5. UI State Tests

### TC-UI-001: Loading State Display

| Item | Content |
|-----|------|
| **Preconditions** | Enter page |
| **Test Steps** | See below |
| **Expected Result** | Show loading animation |
| **Priority** | P0 |

**Test Steps**:
1. Enter page
2. Observe loading state

**Expected Results**:
- Shows loading animation or skeleton

---

### TC-UI-002: Empty State Display

| Item | Content |
|-----|------|
| **Preconditions** | No data |
| **Test Steps** | See below |
| **Expected Result** | Show empty state screen |
| **Priority** | P0 |

---

### TC-UI-003: Error State Display

| Item | Content |
|-----|------|
| **Preconditions** | API returns error |
| **Test Steps** | See below |
| **Expected Result** | Show error message + retry button |
| **Priority** | P0 |

---

## 6. API Tests

### TC-API-001: API Success Response

| Item | Content |
|-----|------|
| **Preconditions** | User logged in |
| **Test Steps** | See below |
| **Expected Result** | API returns 200, data correct |
| **Priority** | P0 |

---

## 7. Error Handling Tests

### TC-ERR-001: Network Offline

| Item | Content |
|-----|------|
| **Preconditions** | Normal usage |
| **Test Steps** | Disable network connection |
| **Expected Result** | Show "Network connection failed" |
| **Priority** | P0 |

---

### TC-ERR-002: API Timeout

| Item | Content |
|-----|------|
| **Preconditions** | Mock API delay |
| **Test Steps** | Trigger API request |
| **Expected Result** | Show "Request timeout" |
| **Priority** | P1 |

---

### TC-ERR-003: Server Error

| Item | Content |
|-----|------|
| **Preconditions** | Mock 500 error |
| **Test Steps** | Trigger API request |
| **Expected Result** | Show "Server error, please try again later" |
| **Priority** | P0 |

---

## 8. Boundary Condition Tests

### TC-EDGE-001: Input Validation

| # | Field | Test Value | Expected Result |
|:-:|-----|-------|---------|
| 1 | {Field} | Empty | Show error "{Field} is required" |
| 2 | {Field} | Exceeds limit | Show error "Maximum X characters" |
| 3 | {Field} | Special characters | Handle normally |
| 4 | {Field} | XSS attack | Filter and sanitize, no script execution |

---

## 9. Compatibility Tests

### 9.1 Browsers (Web)

| Browser | Version | Test Result |
|-------|------|:--------:|
| Chrome | Latest 2 versions | ⬜ |
| Safari | Latest 2 versions | ⬜ |
| Firefox | Latest 2 versions | ⬜ |
| Edge | Latest 2 versions | ⬜ |

### 9.2 Devices (App)

| Platform | Version | Test Device | Test Result |
|-----|------|---------|:--------:|
| iOS | 15.0+ | iPhone 12 | ⬜ |
| iOS | 15.0+ | iPhone 14 | ⬜ |
| Android | API 26+ | Pixel 6 | ⬜ |
| Android | API 26+ | Samsung S22 | ⬜ |

---

## 10. Performance Tests

| # | Item | Standard | Test Result |
|:-:|-----|------|:--------:|
| 1 | Initial load | < 2 seconds | ⬜ |
| 2 | API response | < 500ms | ⬜ |
| 3 | Animation smoothness | 60fps | ⬜ |
| 4 | Memory usage | No memory leak | ⬜ |

---

## 11. Test Case Summary

| Type | TC ID Range | Count | P0 | P1 | P2 |
|-----|-----------|:----:|:--:|:--:|:--:|
| Functional Flow | TC-FL-XXX | {n} | {n} | {n} | {n} |
| UI State | TC-UI-XXX | {n} | {n} | {n} | {n} |
| API Tests | TC-API-XXX | {n} | {n} | {n} | {n} |
| Error Handling | TC-ERR-XXX | {n} | {n} | {n} | {n} |
| Boundary | TC-EDGE-XXX | {n} | {n} | {n} | {n} |
| Performance | TC-PERF-XXX | {n} | {n} | {n} | {n} |
| **Total** | - | **{n}** | **{n}** | **{n}** | **{n}** |

---

## 12. Acceptance Criteria

### 12.1 Release Criteria

- [ ] All P0 test cases pass
- [ ] 95%+ P1 test cases pass
- [ ] No known Critical / Major bugs
- [ ] Performance meets standards

### 12.2 Bug Severity

| Severity | Definition | Action |
|:----:|------|---------|
| 🔴 Critical | System crash, data loss | Block release, fix immediately |
| 🟠 Major | Main feature unusable | Block release, fix with priority |
| 🟡 Minor | Secondary feature issue | Don't block, fix in next release |
| 🟢 Trivial | UI glitch, typo | Don't block, schedule fix |

---

## Changelog

| Version | Date | Changes | Author |
|-----|------|---------|------|
| 1.0.0 | {date} | Initial version | @{qa} |

# Contract: {功能名稱} - API Contract

> Backend API Specification

---

## Metadata

| 項目 | 內容 |
|-----|------|
| Feature ID | {feature-id} |
| Feature Name | {功能名稱} |
| Backend Owner | @{username} |
| Created Date | {YYYY-MM-DD} |
| Status | Draft / Review / Approved |
| Version | 1.0.0 |
| Spec Reference | [規格.md](./規格.md) |

---

## Related Documents

| Type | Document | Status |
|------|----------|:------:|
| PRD | [{功能名稱}.md](../../產品需求文件/ph{X}/{功能名稱}.md) | ✅ |
| Feature Spec | [規格.md](./規格.md) | ✅ |
| Acceptance | [驗收.md](./驗收.md) | 🔵 Pending |

---

## Outstanding Items

| Item | Owner | Status |
|------|-------|:------:|
| 確認認證機制（JWT / Session） | @Backend | 🔵 |
| Rate Limiting 具體數值確認 | @Backend | 🔵 |
| {待確認項目} | @{owner} | 🔵 |

---

## 1. Overview

本文件定義 {功能名稱} 相關的 API 合約。

{功能說明}

---

## 2. Data Schema

### 2.1 Enums

#### {EnumName}

{Enum 說明}

| Value | Description |
|-------|-------------|
| `value1` | {說明} |
| `value2` | {說明} |

---

### 2.2 Entities

#### {EntityName}

{Entity 說明}

| Field | Type | Required | Description | Default | Example |
|-------|------|:--------:|-------------|---------|---------|
| id | string | ✓ | 唯一識別碼 | - | `"entity_abc123"` |
| name | string | ✓ | 名稱 | - | `"範例名稱"` |
| status | {EnumName} | ✓ | 狀態 | `"active"` | `"active"` |
| createdAt | datetime | ✓ | 建立時間 | - | `"2026-01-22T10:30:00Z"` |
| updatedAt | datetime | ✓ | 更新時間 | - | `"2026-01-22T10:30:00Z"` |

**Example:**
```json
{
  "id": "entity_abc123",
  "name": "範例名稱",
  "status": "active",
  "createdAt": "2026-01-22T10:30:00Z",
  "updatedAt": "2026-01-22T10:30:00Z"
}
```

---

## 3. API Endpoints

### 3.1 {API 名稱}

{API 說明}

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
| {param} | query | string | - | {說明} | `"value"` |

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
| 400 | `INVALID_REQUEST` | 請求格式錯誤 | 顯示錯誤訊息 |
| 401 | `UNAUTHORIZED` | 未授權或 Token 無效 | 導向登入頁 |
| 404 | `NOT_FOUND` | 資源不存在 | 顯示「找不到」 |
| 429 | `RATE_LIMITED` | 請求過於頻繁 | 延遲重試 |
| 500 | `INTERNAL_ERROR` | 伺服器錯誤 | 顯示「系統錯誤」 |

**Performance**

| Metric | Target |
|--------|--------|
| P50 | < 100ms |
| P95 | < 200ms |
| P99 | < 500ms |

---

### 3.2 {另一個 API}

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
| `UNAUTHORIZED` | 401 | 未授權或 Token 無效 | 清除本地 Token，導向登入頁 |
| `FORBIDDEN` | 403 | 無權限執行此操作 | 顯示「無權限」 |
| `NOT_FOUND` | 404 | 資源不存在 | 顯示「找不到」 |
| `VALIDATION_ERROR` | 400 | 請求參數驗證失敗 | 顯示具體欄位錯誤 |
| `RATE_LIMITED` | 429 | 請求過於頻繁 | 顯示「請稍後再試」，延遲重試 |
| `INTERNAL_ERROR` | 500 | 伺服器內部錯誤 | 顯示「系統錯誤」 |

---

## 5. Security Considerations

| 項目 | 說明 |
|-----|------|
| 認證 | 所有 API 需要有效的 Bearer Token |
| 授權 | 用戶只能存取自己的資料 |
| Rate Limiting | 單一用戶每分鐘最多 {N} 次請求 |
| 資料驗證 | 嚴格驗證所有輸入參數 |

---

## 6. Implementation Notes

### 6.1 前端實作建議

{前端實作相關說明}

### 6.2 離線處理

| 操作 | 處理方式 |
|-----|---------|
| 讀取資料 | 使用本地快取 |
| 變更資料 | 儲存本地 + 標記待同步 |
| 連線恢復 | 背景同步待同步項目 |

---

## 7. Out of Scope

以下項目不在本合約範圍內：

| 項目 | 原因 | 相關文件 |
|-----|------|---------|
| {項目} | {原因} | {相關文件或待定} |

---

## Changelog

| 版本 | 日期 | 變更內容 | 作者 |
|-----|------|---------|------|
| 1.0.0 | {date} | 初版 | @{backend} |

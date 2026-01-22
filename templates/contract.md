# Contract: {功能名稱}

> API 契約文件

---

## Metadata

| 項目 | 內容 |
|-----|------|
| 功能 ID | {FE-XXX} |
| 功能名稱 | {名稱} |
| Spec | [spec.md](./spec.md) |
| 負責 Backend | @{username} |
| 建立日期 | {YYYY-MM-DD} |
| 狀態 | Draft / Review / Approved |

---

## 1. API 總覽

| Method | Endpoint | 說明 |
|:------:|----------|------|
| GET | `/api/v1/{resource}` | 取得列表 |
| GET | `/api/v1/{resource}/:id` | 取得單筆 |
| POST | `/api/v1/{resource}` | 新增 |
| PUT | `/api/v1/{resource}/:id` | 更新 |
| DELETE | `/api/v1/{resource}/:id` | 刪除 |

---

## 2. API 詳細規格

### 2.1 取得列表

```
GET /api/v1/{resource}
```

#### Request

**Headers**
| Header | 必填 | 說明 |
|--------|:----:|------|
| Authorization | ✅ | Bearer {token} |

**Query Parameters**
| 參數 | 類型 | 必填 | 說明 | 範例 |
|-----|------|:----:|------|------|
| page | integer | | 頁碼，預設 1 | `1` |
| limit | integer | | 每頁筆數，預設 20，最大 100 | `20` |
| sort | string | | 排序欄位 | `createdAt` |
| order | string | | 排序方向：asc / desc | `desc` |
| q | string | | 搜尋關鍵字 | `keyword` |

#### Response

**成功 (200)**
```json
{
  "success": true,
  "data": {
    "items": [
      {
        "id": "string",
        "name": "string",
        "createdAt": "2024-01-01T00:00:00Z",
        "updatedAt": "2024-01-01T00:00:00Z"
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 20,
      "total": 100,
      "totalPages": 5
    }
  }
}
```

**錯誤**
| 狀態碼 | 錯誤碼 | 說明 |
|:------:|-------|------|
| 401 | UNAUTHORIZED | 未授權 |
| 403 | FORBIDDEN | 無權限 |

---

### 2.2 取得單筆

```
GET /api/v1/{resource}/:id
```

#### Request

**Path Parameters**
| 參數 | 類型 | 必填 | 說明 |
|-----|------|:----:|------|
| id | string | ✅ | 資源 ID |

#### Response

**成功 (200)**
```json
{
  "success": true,
  "data": {
    "id": "string",
    "name": "string",
    "description": "string",
    "createdAt": "2024-01-01T00:00:00Z",
    "updatedAt": "2024-01-01T00:00:00Z"
  }
}
```

**錯誤**
| 狀態碼 | 錯誤碼 | 說明 |
|:------:|-------|------|
| 404 | NOT_FOUND | 資源不存在 |

---

### 2.3 新增

```
POST /api/v1/{resource}
```

#### Request

**Body**
```json
{
  "name": "string",       // 必填，1-100 字元
  "description": "string" // 選填，最多 500 字元
}
```

**欄位驗證**
| 欄位 | 規則 |
|-----|------|
| name | 必填，1-100 字元 |
| description | 選填，最多 500 字元 |

#### Response

**成功 (201)**
```json
{
  "success": true,
  "data": {
    "id": "string",
    "name": "string",
    "description": "string",
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

**錯誤**
| 狀態碼 | 錯誤碼 | 說明 |
|:------:|-------|------|
| 400 | VALIDATION_ERROR | 驗證失敗 |
| 409 | DUPLICATE | 名稱重複 |

---

### 2.4 更新

```
PUT /api/v1/{resource}/:id
```

#### Request

**Body**
```json
{
  "name": "string",
  "description": "string"
}
```

#### Response

**成功 (200)**
```json
{
  "success": true,
  "data": {
    "id": "string",
    "name": "string",
    "description": "string",
    "updatedAt": "2024-01-01T00:00:00Z"
  }
}
```

---

### 2.5 刪除

```
DELETE /api/v1/{resource}/:id
```

#### Response

**成功 (200)**
```json
{
  "success": true,
  "data": {
    "id": "string",
    "deletedAt": "2024-01-01T00:00:00Z"
  }
}
```

---

## 3. 資料結構

### 3.1 Entity

```typescript
interface Entity {
  id: string;           // UUID
  name: string;         // 名稱
  description?: string; // 描述
  status: Status;       // 狀態
  createdAt: string;    // ISO 8601
  updatedAt: string;    // ISO 8601
  createdBy: string;    // 建立者 ID
  updatedBy: string;    // 更新者 ID
}

enum Status {
  ACTIVE = 'active',
  INACTIVE = 'inactive',
  DELETED = 'deleted'
}
```

### 3.2 Pagination

```typescript
interface Pagination {
  page: number;       // 目前頁碼
  limit: number;      // 每頁筆數
  total: number;      // 總筆數
  totalPages: number; // 總頁數
}
```

### 3.3 Error Response

```typescript
interface ErrorResponse {
  success: false;
  error: {
    code: string;      // 錯誤碼
    message: string;   // 錯誤訊息
    details?: object;  // 詳細資訊（驗證錯誤時）
  }
}
```

---

## 4. 錯誤碼定義

| 錯誤碼 | HTTP 狀態碼 | 說明 |
|-------|:----------:|------|
| UNAUTHORIZED | 401 | 未授權，請先登入 |
| FORBIDDEN | 403 | 無權限執行此操作 |
| NOT_FOUND | 404 | 資源不存在 |
| VALIDATION_ERROR | 400 | 請求參數驗證失敗 |
| DUPLICATE | 409 | 資源已存在 |
| INTERNAL_ERROR | 500 | 伺服器內部錯誤 |

---

## 5. 非功能需求

### 5.1 效能需求

| API | 回應時間 | 備註 |
|-----|---------|------|
| GET 列表 | < 500ms | p95 |
| GET 單筆 | < 200ms | p95 |
| POST/PUT | < 500ms | p95 |
| DELETE | < 200ms | p95 |

### 5.2 限流

| 類型 | 限制 |
|-----|------|
| 每用戶 | 100 req/min |
| 全域 | 1000 req/min |

---

## 6. 第三方串接

引用 `knowledge/integrations/` 中的相關服務：

| 服務 | 用途 | 文件 |
|-----|------|------|
| {服務名稱} | {用途} | [連結](../../knowledge/integrations/xxx.md) |

---

## 7. 相關文件

- [PRD](./prd.md)
- [Spec](./spec.md)
- [驗收標準](./acceptance.md)

---

## 變更紀錄

| 日期 | 版本 | 變更內容 | 作者 |
|-----|------|---------|------|
| {日期} | 1.0 | 初版 | @{username} |

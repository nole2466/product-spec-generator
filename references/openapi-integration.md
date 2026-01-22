# OpenAPI 整合指南

> 將 contract.md 轉換為 OpenAPI，實現自動化 Mock 和文件產生

---

## 為什麼要整合 OpenAPI？

| 好處 | 說明 |
|-----|------|
| **自動 Mock** | 前端不用等後端，可以先開發 |
| **API 文件** | 自動產生 Swagger UI |
| **型別產生** | 自動產生 TypeScript 型別 |
| **測試輔助** | 自動產生 API 測試案例 |

---

## contract.md → OpenAPI 對應表

| contract.md | OpenAPI 3.0 | 說明 |
|-------------|-------------|------|
| Data Schema | `components.schemas` | 資料結構定義 |
| API Endpoints | `paths` | API 路徑和方法 |
| Request | `requestBody` / `parameters` | 請求參數 |
| Response | `responses` | 回應格式 |
| Error Codes | `components.responses` | 錯誤回應 |

---

## 轉換範例

### contract.md 格式

```markdown
## Data Schema

### Stock（股票）

| 欄位 | 型別 | 必填 | 說明 | 範例 |
|-----|------|:----:|------|------|
| id | string | ✓ | 唯一識別碼 | "stock_2330" |
| symbol | string | ✓ | 股票代號 | "2330" |
| name | string | ✓ | 股票名稱 | "台積電" |
| price | number | ✓ | 現價 | 580.00 |

## API Endpoints

### 搜尋股票

GET /api/v1/stocks/search

**Request**

| 參數 | 位置 | 型別 | 必填 | 說明 |
|-----|------|------|:----:|------|
| q | query | string | ✓ | 搜尋關鍵字 |
| limit | query | number | - | 回傳筆數 |

**Response - 成功 (200)**

{
  "success": true,
  "data": {
    "items": [Stock]
  }
}
```

### 對應的 OpenAPI 3.0

```yaml
openapi: 3.0.0
info:
  title: Stock API
  version: 1.0.0

components:
  schemas:
    Stock:
      type: object
      required:
        - id
        - symbol
        - name
        - price
      properties:
        id:
          type: string
          example: "stock_2330"
        symbol:
          type: string
          example: "2330"
        name:
          type: string
          example: "台積電"
        price:
          type: number
          example: 580.00

    SearchResponse:
      type: object
      properties:
        success:
          type: boolean
        data:
          type: object
          properties:
            items:
              type: array
              items:
                $ref: '#/components/schemas/Stock'

paths:
  /api/v1/stocks/search:
    get:
      summary: 搜尋股票
      parameters:
        - name: q
          in: query
          required: true
          schema:
            type: string
          description: 搜尋關鍵字
        - name: limit
          in: query
          required: false
          schema:
            type: number
          description: 回傳筆數
      responses:
        '200':
          description: 成功
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/SearchResponse'
```

---

## Mock Server 方案

### 方案 1: Prism（推薦）

基於 OpenAPI 自動產生 Mock Server。

**安裝**：
```bash
npm install -g @stoplight/prism-cli
```

**使用**：
```bash
# 啟動 Mock Server
prism mock openapi.yaml

# Mock Server 運行在 http://localhost:4010
```

**特點**：
- 自動根據 schema 產生假資料
- 支援動態回應
- 可驗證請求格式

---

### 方案 2: MSW（Mock Service Worker）

在瀏覽器端攔截請求，適合前端開發和測試。

**安裝**：
```bash
npm install msw --save-dev
```

**使用**：
```typescript
// mocks/handlers.ts
import { rest } from 'msw'

export const handlers = [
  rest.get('/api/v1/stocks/search', (req, res, ctx) => {
    const q = req.url.searchParams.get('q')
    
    return res(
      ctx.json({
        success: true,
        data: {
          items: [
            { id: 'stock_2330', symbol: '2330', name: '台積電', price: 580 }
          ]
        }
      })
    )
  })
]
```

**特點**：
- 不需要啟動額外服務
- 可在測試中使用
- 支援請求攔截和驗證

---

### 方案 3: JSON Server

快速建立 REST API，適合快速原型。

**安裝**：
```bash
npm install -g json-server
```

**使用**：
```json
// db.json
{
  "stocks": [
    { "id": "stock_2330", "symbol": "2330", "name": "台積電", "price": 580 }
  ]
}
```

```bash
json-server --watch db.json --port 3001
```

**特點**：
- 超快速設置
- 支援 CRUD 操作
- 適合簡單場景

---

## 方案選擇指南

| 情境 | 推薦方案 |
|-----|---------|
| 前端獨立開發 | Prism |
| 前端單元測試 | MSW |
| E2E 測試 | Prism / MSW |
| 快速原型 | JSON Server |
| 複雜業務邏輯 | 自建 Mock Server |

---

## 型別產生

### TypeScript 型別

使用 `openapi-typescript` 從 OpenAPI 產生 TypeScript 型別。

**安裝**：
```bash
npm install openapi-typescript --save-dev
```

**使用**：
```bash
npx openapi-typescript openapi.yaml -o src/types/api.d.ts
```

**產生結果**：
```typescript
// src/types/api.d.ts
export interface Stock {
  id: string
  symbol: string
  name: string
  price: number
}

export interface SearchResponse {
  success: boolean
  data: {
    items: Stock[]
  }
}
```

---

## 工作流程整合

### 建議流程

```
1. Backend 撰寫 contract.md
       ↓
2. 轉換為 openapi.yaml（手動或 AI 輔助）
       ↓
3. 提交到 Git
       ↓
4. CI 自動產生：
   - Mock Server
   - TypeScript 型別
   - API 文件
       ↓
5. Frontend 使用 Mock 開發
       ↓
6. Backend 實作 API
       ↓
7. 切換到真實 API
```

### 檔案結構

```
specs/
└── search-stock/
    ├── spec.md
    ├── design.md
    ├── contract.md
    ├── contract.openapi.yaml  # OpenAPI 格式
    └── acceptance.md
```

---

## AI 協作指南

### 讓 AI 幫你轉換 OpenAPI

**Prompt 範本**：

```
請將以下 contract.md 轉換為 OpenAPI 3.0 格式：

{contract.md 內容}

要求：
1. 使用 YAML 格式
2. 包含所有 Data Schema
3. 包含所有 API Endpoints
4. 包含錯誤回應
5. 加入適當的 example
```

### 讓 AI 幫你產生 Mock Handler

**Prompt 範本**：

```
請根據以下 OpenAPI，產生 MSW handler：

{openapi.yaml 內容}

要求：
1. 使用 TypeScript
2. 每個 API 都要有 handler
3. 回傳符合 schema 的假資料
4. 包含錯誤情境的 handler
```

---

## 常見問題

### Q: contract.md 和 openapi.yaml 哪個是 Source of Truth？

**A**: contract.md 是 Source of Truth。openapi.yaml 是從 contract.md 產生的，當 contract.md 變更時，需要同步更新 openapi.yaml。

### Q: 需要手動維護兩份文件嗎？

**A**: 建議用 AI 輔助轉換，減少手動維護成本。未來可以開發自動轉換工具。

### Q: Mock 資料和真實資料不一致怎麼辦？

**A**: 
1. Mock 資料應該符合 schema 定義
2. 使用 Prism 可以自動驗證
3. 定期比對 Mock 和真實 API 回應

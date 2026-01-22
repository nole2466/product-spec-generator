# Contract: 商品搜尋

> API 契約文件

---

## Metadata

| 項目 | 內容 |
|-----|------|
| 功能 ID | FE-001 |
| 功能名稱 | 商品搜尋 |
| Spec | [spec.md](./spec.md) |
| 負責 Backend | @backend-tom |
| 建立日期 | 2024-01-23 |
| 狀態 | Approved |

---

## 1. API 總覽

| Method | Endpoint | 說明 |
|:------:|----------|------|
| GET | `/api/v1/search` | 搜尋商品 |
| GET | `/api/v1/search/suggestions` | 搜尋建議 |
| GET | `/api/v1/search/filters` | 取得篩選選項 |

---

## 2. API 詳細規格

### 2.1 搜尋商品

```
GET /api/v1/search
```

#### Request

**Headers**
| Header | 必填 | 說明 |
|--------|:----:|------|
| Authorization | | Bearer {token}（登入用戶） |

**Query Parameters**
| 參數 | 類型 | 必填 | 說明 | 範例 |
|-----|------|:----:|------|------|
| q | string | ✅ | 搜尋關鍵字（1-50 字元） | `iPhone` |
| page | integer | | 頁碼，預設 1 | `1` |
| limit | integer | | 每頁筆數，預設 20，最大 100 | `20` |
| sort | string | | 排序方式 | `relevance` |
| category | string | | 分類 ID（可多個，逗號分隔） | `cat1,cat2` |
| minPrice | number | | 最低價格 | `100` |
| maxPrice | number | | 最高價格 | `5000` |
| minRating | number | | 最低評價（1-5） | `4` |

**排序選項**
| 值 | 說明 |
|---|------|
| `relevance` | 相關度（預設） |
| `price_asc` | 價格低到高 |
| `price_desc` | 價格高到低 |
| `sales` | 銷量 |
| `newest` | 最新 |

#### Response

**成功 (200)**
```json
{
  "success": true,
  "data": {
    "items": [
      {
        "id": "prod_123",
        "name": "iPhone 15 Pro 256GB",
        "description": "Apple 最新旗艦手機",
        "imageUrl": "https://cdn.example.com/products/iphone15.jpg",
        "price": 36900,
        "originalPrice": 39900,
        "rating": 4.8,
        "ratingCount": 1234,
        "sales": 5678,
        "categoryId": "cat_phone",
        "categoryName": "手機",
        "inStock": true,
        "tags": ["熱銷", "限時優惠"]
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 20,
      "total": 128,
      "totalPages": 7
    },
    "filters": {
      "categories": [
        {"id": "cat_phone", "name": "手機", "count": 45},
        {"id": "cat_case", "name": "手機殼", "count": 83}
      ],
      "priceRange": {
        "min": 99,
        "max": 49900
      }
    }
  }
}
```

**錯誤**
| 狀態碼 | 錯誤碼 | 說明 |
|:------:|-------|------|
| 400 | INVALID_QUERY | 搜尋關鍵字無效 |
| 400 | INVALID_PARAMS | 參數格式錯誤 |

---

### 2.2 搜尋建議

```
GET /api/v1/search/suggestions
```

#### Request

**Query Parameters**
| 參數 | 類型 | 必填 | 說明 | 範例 |
|-----|------|:----:|------|------|
| q | string | ✅ | 輸入文字（至少 1 字元） | `iPh` |
| limit | integer | | 建議數量，預設 10，最大 20 | `10` |

#### Response

**成功 (200)**
```json
{
  "success": true,
  "data": {
    "suggestions": [
      {
        "type": "keyword",
        "text": "iPhone 15",
        "highlight": "<em>iPh</em>one 15"
      },
      {
        "type": "keyword",
        "text": "iPhone 15 Pro",
        "highlight": "<em>iPh</em>one 15 Pro"
      },
      {
        "type": "category",
        "text": "iPhone 手機殼",
        "highlight": "<em>iPh</em>one 手機殼",
        "categoryId": "cat_case"
      }
    ]
  }
}
```

**建議類型**
| type | 說明 |
|------|------|
| `keyword` | 熱門搜尋關鍵字 |
| `category` | 分類名稱 |
| `brand` | 品牌名稱 |

---

### 2.3 取得篩選選項

```
GET /api/v1/search/filters
```

#### Request

**Query Parameters**
| 參數 | 類型 | 必填 | 說明 | 範例 |
|-----|------|:----:|------|------|
| q | string | ✅ | 搜尋關鍵字 | `iPhone` |

#### Response

**成功 (200)**
```json
{
  "success": true,
  "data": {
    "categories": [
      {"id": "cat_phone", "name": "手機", "count": 45},
      {"id": "cat_case", "name": "手機殼", "count": 83},
      {"id": "cat_charger", "name": "充電器", "count": 32}
    ],
    "priceRanges": [
      {"min": 0, "max": 500, "label": "$500 以下", "count": 45},
      {"min": 500, "max": 1000, "label": "$500-$1000", "count": 38},
      {"min": 1000, "max": 5000, "label": "$1000-$5000", "count": 67},
      {"min": 5000, "max": null, "label": "$5000 以上", "count": 23}
    ],
    "ratings": [
      {"min": 4, "label": "4 星以上", "count": 98},
      {"min": 3, "label": "3 星以上", "count": 115}
    ]
  }
}
```

---

## 3. 資料結構

### 3.1 Product

```typescript
interface Product {
  id: string;              // 商品 ID
  name: string;            // 商品名稱
  description: string;     // 商品描述
  imageUrl: string;        // 商品圖片 URL
  price: number;           // 售價
  originalPrice?: number;  // 原價（有折扣時顯示）
  rating: number;          // 評價（1-5）
  ratingCount: number;     // 評價數量
  sales: number;           // 銷量
  categoryId: string;      // 分類 ID
  categoryName: string;    // 分類名稱
  inStock: boolean;        // 是否有庫存
  tags?: string[];         // 標籤
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

### 3.3 Suggestion

```typescript
interface Suggestion {
  type: 'keyword' | 'category' | 'brand';
  text: string;           // 建議文字
  highlight: string;      // 高亮 HTML
  categoryId?: string;    // 分類 ID（type 為 category 時）
}
```

### 3.4 Error Response

```typescript
interface ErrorResponse {
  success: false;
  error: {
    code: string;
    message: string;
    details?: object;
  }
}
```

---

## 4. 錯誤碼定義

| 錯誤碼 | HTTP 狀態碼 | 說明 |
|-------|:----------:|------|
| INVALID_QUERY | 400 | 搜尋關鍵字無效（空白或超過 50 字元） |
| INVALID_PARAMS | 400 | 參數格式錯誤 |
| INTERNAL_ERROR | 500 | 伺服器內部錯誤 |

---

## 5. 非功能需求

### 5.1 效能需求

| API | 回應時間 | 備註 |
|-----|---------|------|
| 搜尋商品 | < 500ms | p95 |
| 搜尋建議 | < 200ms | p95 |
| 篩選選項 | < 300ms | p95 |

### 5.2 限流

| 類型 | 限制 |
|-----|------|
| 搜尋 API | 60 req/min per user |
| 建議 API | 120 req/min per user |

---

## 6. 實作備註

### 6.1 搜尋引擎

使用 Elasticsearch 實作，索引包含：
- 商品名稱（繁簡體分詞）
- 商品描述
- 品牌名稱
- 分類名稱

### 6.2 繁簡體轉換

搜尋時自動進行繁簡體轉換，確保「手機」和「手机」能搜到相同結果。

### 6.3 快取策略

| 項目 | 快取時間 |
|-----|---------|
| 搜尋建議 | 5 分鐘 |
| 篩選選項 | 10 分鐘 |
| 搜尋結果 | 不快取 |

---

## 7. 相關文件

- [PRD](./prd.md)
- [Spec](./spec.md)
- [驗收標準](./acceptance.md)

---

## 變更紀錄

| 日期 | 版本 | 變更內容 | 作者 |
|-----|------|---------|------|
| 2024-01-23 | 1.0 | 初版 | @backend-tom |

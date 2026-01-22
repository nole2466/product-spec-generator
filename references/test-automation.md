# 自動化測試指南

> 將 acceptance.md 轉換為自動化測試

---

## 測試框架選擇

| 框架 | 適用場景 | 特點 |
|-----|---------|------|
| **Cypress** | E2E 測試 | 易上手、豐富的 API |
| **Playwright** | E2E 測試 | 跨瀏覽器、速度快 |
| **Jest + RTL** | 元件測試 | React 生態系標準 |
| **Vitest** | 單元測試 | 快速、Vite 整合 |

---

## acceptance.md → 自動化測試

### 轉換對應表

| acceptance.md | 自動化測試 |
|---------------|-----------|
| 情境名稱 | `describe` 區塊 |
| 前置條件 | `beforeEach` |
| 測試步驟 | `it` 區塊 |
| 操作 | 測試動作 |
| 預期結果 | 斷言 |

---

## Cypress 範本

### 基本結構

```typescript
// cypress/e2e/search-stock.cy.ts

describe('搜尋股票', () => {
  beforeEach(() => {
    // 前置條件
    cy.login()
    cy.visit('/search')
  })

  describe('情境 1：正常搜尋 - 有結果', () => {
    it('輸入股票代號後顯示搜尋結果', () => {
      // 操作
      cy.get('[data-testid="search-input"]').type('2330')
      
      // 預期結果
      cy.get('[data-testid="search-loading"]').should('be.visible')
      cy.get('[data-testid="stock-list"]').should('be.visible')
      cy.contains('台積電').should('be.visible')
    })
  })

  describe('情境 2：邊界情境 - 無結果', () => {
    it('輸入不存在的關鍵字顯示空狀態', () => {
      cy.get('[data-testid="search-input"]').type('zzzzz')
      
      cy.get('[data-testid="empty-state"]').should('be.visible')
      cy.contains('無搜尋結果').should('be.visible')
    })
  })

  describe('情境 3：錯誤情境 - 網路錯誤', () => {
    it('網路錯誤時顯示錯誤訊息和重試按鈕', () => {
      // Mock 網路錯誤
      cy.intercept('GET', '/api/v1/stocks/search*', {
        statusCode: 500,
        body: { error: 'INTERNAL_ERROR' }
      })

      cy.get('[data-testid="search-input"]').type('2330')
      
      cy.get('[data-testid="error-state"]').should('be.visible')
      cy.get('[data-testid="retry-button"]').should('be.visible')
    })
  })
})
```

### 常用指令

```typescript
// 元素選取
cy.get('[data-testid="search-input"]')
cy.contains('台積電')
cy.get('.stock-card').first()

// 操作
cy.type('2330')
cy.click()
cy.clear()
cy.select('option')

// 斷言
cy.should('be.visible')
cy.should('not.exist')
cy.should('have.text', '台積電')
cy.should('have.length', 20)

// 等待
cy.wait('@searchApi')
cy.get('[data-testid="loading"]').should('not.exist')

// API Mock
cy.intercept('GET', '/api/v1/stocks/search*', { fixture: 'stocks.json' }).as('searchApi')
```

---

## Playwright 範本

### 基本結構

```typescript
// tests/search-stock.spec.ts

import { test, expect } from '@playwright/test'

test.describe('搜尋股票', () => {
  test.beforeEach(async ({ page }) => {
    // 前置條件
    await page.goto('/search')
  })

  test('情境 1：正常搜尋 - 有結果', async ({ page }) => {
    // 操作
    await page.getByTestId('search-input').fill('2330')
    
    // 預期結果
    await expect(page.getByTestId('search-loading')).toBeVisible()
    await expect(page.getByTestId('stock-list')).toBeVisible()
    await expect(page.getByText('台積電')).toBeVisible()
  })

  test('情境 2：邊界情境 - 無結果', async ({ page }) => {
    await page.getByTestId('search-input').fill('zzzzz')
    
    await expect(page.getByTestId('empty-state')).toBeVisible()
    await expect(page.getByText('無搜尋結果')).toBeVisible()
  })

  test('情境 3：錯誤情境 - 網路錯誤', async ({ page }) => {
    // Mock 網路錯誤
    await page.route('**/api/v1/stocks/search*', route => {
      route.fulfill({
        status: 500,
        body: JSON.stringify({ error: 'INTERNAL_ERROR' })
      })
    })

    await page.getByTestId('search-input').fill('2330')
    
    await expect(page.getByTestId('error-state')).toBeVisible()
    await expect(page.getByTestId('retry-button')).toBeVisible()
  })
})
```

### 常用指令

```typescript
// 元素選取
page.getByTestId('search-input')
page.getByText('台積電')
page.getByRole('button', { name: '搜尋' })
page.locator('.stock-card').first()

// 操作
await element.fill('2330')
await element.click()
await element.clear()

// 斷言
await expect(element).toBeVisible()
await expect(element).toHaveText('台積電')
await expect(element).toHaveCount(20)

// API Mock
await page.route('**/api/**', route => route.fulfill({ body: mockData }))
```

---

## MSW (Mock Service Worker) 範本

適合元件測試和整合測試。

```typescript
// mocks/handlers.ts

import { rest } from 'msw'

export const handlers = [
  // 成功情境
  rest.get('/api/v1/stocks/search', (req, res, ctx) => {
    const q = req.url.searchParams.get('q')
    
    if (q === 'zzzzz') {
      return res(ctx.json({ success: true, data: { items: [] } }))
    }
    
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
  }),

  // 錯誤情境
  rest.get('/api/v1/stocks/error', (req, res, ctx) => {
    return res(
      ctx.status(500),
      ctx.json({ error: 'INTERNAL_ERROR' })
    )
  })
]
```

```typescript
// tests/SearchPage.test.tsx

import { render, screen, waitFor } from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import { SearchPage } from './SearchPage'

describe('SearchPage', () => {
  it('搜尋成功顯示結果', async () => {
    render(<SearchPage />)
    
    await userEvent.type(screen.getByTestId('search-input'), '2330')
    
    await waitFor(() => {
      expect(screen.getByText('台積電')).toBeInTheDocument()
    })
  })
})
```

---

## data-testid 規範

為了讓測試穩定，建議使用 `data-testid` 而非 class 或 id。

### 命名規則

```
{component}-{element}-{state}
```

| 元件 | data-testid |
|-----|-------------|
| 搜尋輸入框 | `search-input` |
| 搜尋按鈕 | `search-button` |
| 載入中 | `search-loading` |
| 結果列表 | `stock-list` |
| 列表項目 | `stock-item-{id}` |
| 空狀態 | `empty-state` |
| 錯誤狀態 | `error-state` |
| 重試按鈕 | `retry-button` |

### 在 design.md 標註

```markdown
### 元件清單

| 元件 | Component Name | data-testid |
|-----|----------------|-------------|
| 搜尋框 | `SearchInput` | `search-input` |
| 結果列表 | `StockList` | `stock-list` |
| 空狀態 | `EmptyState` | `empty-state` |
```

---

## 測試覆蓋率建議

| 情境類型 | 建議覆蓋 |
|---------|---------|
| Happy Path | 100% |
| 邊界條件 | > 80% |
| 錯誤情境 | > 80% |
| Edge Case | > 50% |

---

## AI 協作指南

### 讓 AI 幫你產生測試

**Prompt 範本**：

```
請根據以下 acceptance.md，產生 Cypress 測試：

{acceptance.md 內容}

要求：
1. 使用 TypeScript
2. 每個情境一個 describe
3. 使用 data-testid 選取元素
4. 包含 API Mock
5. 包含適當的等待和斷言
```

### 讓 AI 幫你檢查測試覆蓋

**Prompt 範本**：

```
請比對以下 acceptance.md 和測試程式碼，檢查測試覆蓋：

acceptance.md:
{內容}

測試程式碼:
{程式碼}

請列出：
1. 已覆蓋的情境
2. 未覆蓋的情境
3. 建議補充的測試
```

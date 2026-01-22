# 無障礙規範指南

> 確保產品對所有用戶都可用，包括身心障礙者

---

## 為什麼需要無障礙？

| 原因 | 說明 |
|-----|------|
| **法規遵循** | 許多國家要求公共網站符合 WCAG 標準 |
| **擴大用戶群** | 全球約 15% 人口有某種形式的障礙 |
| **提升體驗** | 無障礙設計對所有用戶都有益 |
| **SEO 友善** | 語意化 HTML 有助於搜尋引擎理解 |

---

## WCAG 2.1 簡介

Web Content Accessibility Guidelines (WCAG) 分為三個等級：

| 等級 | 說明 | 建議 |
|:---:|------|------|
| A | 最低標準 | 必須達成 |
| AA | 中等標準 | 建議達成 |
| AAA | 最高標準 | 理想目標 |

**四大原則 (POUR)**：
- **Perceivable** 可感知：資訊可被感知
- **Operable** 可操作：介面可被操作
- **Understandable** 可理解：內容可被理解
- **Robust** 穩健性：相容各種輔助技術

---

## design.md 無障礙規格

### 色彩對比

在 design.md 標註色彩對比度：

```markdown
### 色彩規格

| 用途 | 前景色 | 背景色 | 對比度 | WCAG |
|-----|-------|-------|:------:|:----:|
| 正文 | #1C1C1E | #FFFFFF | 16.1:1 | AAA ✅ |
| 次要文字 | #8E8E93 | #FFFFFF | 3.5:1 | AA ⚠️ |
| 連結 | #007AFF | #FFFFFF | 4.5:1 | AA ✅ |
| 按鈕文字 | #FFFFFF | #007AFF | 4.5:1 | AA ✅ |

**對比度標準**：
- 正文：至少 4.5:1（AA）
- 大字（18px+）：至少 3:1（AA）
- 非文字元素：至少 3:1
```

### 觸控區域

```markdown
### 互動元素規格

| 元件 | 最小尺寸 | 間距 | 說明 |
|-----|---------|------|------|
| 按鈕 | 44x44px | 8px | iOS HIG 標準 |
| 連結 | 44x44px | 8px | 觸控區域，非視覺尺寸 |
| 列表項 | 44px 高 | - | 整行可點擊 |
| 核取方塊 | 44x44px | 8px | 含 label 區域 |
```

### 焦點狀態

```markdown
### 焦點狀態設計

每個互動元件都需要定義焦點狀態：

| 元件 | 焦點樣式 | 說明 |
|-----|---------|------|
| 按鈕 | 2px solid #007AFF, offset 2px | 外框 |
| 輸入框 | 2px solid #007AFF | 邊框變色 |
| 連結 | 2px solid #007AFF, offset 2px | 外框 |
| 卡片 | 2px solid #007AFF | 邊框 |

**原則**：
- 焦點必須可見
- 不能只靠顏色變化
- 焦點順序符合邏輯
```

---

## ARIA 標籤規範

### 常用 ARIA 屬性

| 屬性 | 用途 | 範例 |
|-----|------|------|
| `aria-label` | 提供標籤 | `<button aria-label="關閉">✕</button>` |
| `aria-labelledby` | 參考其他元素作為標籤 | `<div aria-labelledby="title">` |
| `aria-describedby` | 提供描述 | `<input aria-describedby="hint">` |
| `aria-hidden` | 對輔助技術隱藏 | `<span aria-hidden="true">👍</span>` |
| `aria-live` | 動態內容通知 | `<div aria-live="polite">` |
| `aria-expanded` | 展開狀態 | `<button aria-expanded="false">` |
| `aria-selected` | 選取狀態 | `<li aria-selected="true">` |
| `aria-disabled` | 禁用狀態 | `<button aria-disabled="true">` |

### 在 design.md 標註

```markdown
### 元件清單

| 元件 | Component | ARIA | 說明 |
|-----|-----------|------|------|
| 搜尋框 | `SearchInput` | `role="search"`, `aria-label="搜尋股票"` | |
| 清除按鈕 | `ClearButton` | `aria-label="清除搜尋"` | 只有圖示 |
| 結果列表 | `StockList` | `role="listbox"`, `aria-label="搜尋結果"` | |
| 結果項目 | `StockItem` | `role="option"`, `aria-selected` | |
| Loading | `LoadingSpinner` | `aria-label="載入中"`, `aria-live="polite"` | |
| 空狀態 | `EmptyState` | `role="status"`, `aria-live="polite"` | |
| 錯誤訊息 | `ErrorMessage` | `role="alert"`, `aria-live="assertive"` | |
```

---

## 鍵盤導航規範

### 基本要求

| 按鍵 | 行為 |
|-----|------|
| `Tab` | 移至下一個可聚焦元素 |
| `Shift + Tab` | 移至上一個可聚焦元素 |
| `Enter` / `Space` | 啟動按鈕或連結 |
| `Escape` | 關閉彈窗、取消操作 |
| `Arrow Keys` | 在列表、選單中移動 |

### 常見元件的鍵盤操作

**下拉選單**：
```
Tab → 聚焦選單按鈕
Enter/Space → 開啟選單
↓/↑ → 在選項間移動
Enter → 選取選項
Escape → 關閉選單
```

**Modal 彈窗**：
```
開啟時 → 焦點移至彈窗
Tab → 在彈窗內循環
Escape → 關閉彈窗
關閉後 → 焦點返回觸發元素
```

**搜尋結果列表**：
```
Tab → 聚焦搜尋框
輸入 → 顯示結果
↓ → 移至第一個結果
↓/↑ → 在結果間移動
Enter → 選取結果
Escape → 清除結果，返回搜尋框
```

### 在 design.md 標註

```markdown
## 鍵盤導航

### 搜尋頁鍵盤操作

| 情境 | 按鍵 | 行為 |
|-----|------|------|
| 搜尋框聚焦 | `↓` | 移至第一個搜尋結果 |
| 搜尋結果 | `↓` / `↑` | 在結果間移動 |
| 搜尋結果 | `Enter` | 進入股票詳情 |
| 搜尋結果 | `Escape` | 返回搜尋框 |
| 任意位置 | `Tab` | 依序移動焦點 |

### 焦點順序

```
1. 返回按鈕
2. 搜尋框
3. 清除按鈕（有文字時）
4. 搜尋結果列表
   4.1 結果項目 1
   4.2 結果項目 2
   ...
```
```

---

## 螢幕閱讀器支援

### 語意化 HTML

| 用途 | 推薦 | 避免 |
|-----|------|------|
| 標題 | `<h1>` ~ `<h6>` | `<div class="title">` |
| 導航 | `<nav>` | `<div class="nav">` |
| 主內容 | `<main>` | `<div class="main">` |
| 按鈕 | `<button>` | `<div onclick>` |
| 連結 | `<a href>` | `<span onclick>` |
| 列表 | `<ul>` / `<ol>` | `<div>` 套 `<div>` |

### 圖片替代文字

```markdown
### 圖片規格

| 圖片類型 | alt 處理 |
|---------|---------|
| 資訊圖片 | 描述圖片內容 |
| 裝飾圖片 | `alt=""` 或 `aria-hidden="true"` |
| 圖示按鈕 | 描述功能，非外觀 |
| Logo | 公司名稱 |

**範例**：
- ✅ `alt="台積電股價走勢圖，過去一週上漲 5%"`
- ✅ `alt=""` （純裝飾）
- ✅ `alt="關閉"` （關閉按鈕的 X 圖示）
- ❌ `alt="圖片"` 
- ❌ `alt="icon.png"`
```

---

## 驗收標準整合

### acceptance.md 無障礙測試項目

```markdown
## 無障礙驗收

### 鍵盤操作測試

| # | 操作 | 預期結果 | 通過 |
|:-:|------|---------|:----:|
| 1 | 只用 Tab 鍵瀏覽頁面 | 所有互動元素可聚焦 | ☐ |
| 2 | 焦點樣式 | 當前焦點位置清晰可見 | ☐ |
| 3 | Enter/Space 啟動按鈕 | 按鈕正常觸發 | ☐ |
| 4 | Escape 關閉彈窗 | 彈窗關閉，焦點返回 | ☐ |

### 螢幕閱讀器測試

| # | 測試項目 | 預期結果 | 通過 |
|:-:|---------|---------|:----:|
| 1 | 頁面標題 | 正確朗讀頁面標題 | ☐ |
| 2 | 表單標籤 | 輸入框有對應標籤 | ☐ |
| 3 | 圖片替代文字 | 資訊圖片有描述 | ☐ |
| 4 | 動態內容 | Loading/錯誤有通知 | ☐ |

### 視覺測試

| # | 測試項目 | 預期結果 | 通過 |
|:-:|---------|---------|:----:|
| 1 | 色彩對比 | 文字對比度 ≥ 4.5:1 | ☐ |
| 2 | 放大 200% | 內容不被截斷 | ☐ |
| 3 | 觸控區域 | ≥ 44x44px | ☐ |
```

---

## 測試工具

### 自動化工具

| 工具 | 用途 | 整合方式 |
|-----|------|---------|
| axe-core | 自動檢測 | Cypress/Playwright 外掛 |
| Lighthouse | 綜合評分 | Chrome DevTools |
| WAVE | 視覺化檢測 | 瀏覽器外掛 |
| pa11y | CI 整合 | CLI 工具 |

### Cypress + axe 範例

```typescript
// cypress/e2e/accessibility.cy.ts

describe('無障礙測試', () => {
  beforeEach(() => {
    cy.visit('/search')
    cy.injectAxe()
  })

  it('搜尋頁無障礙檢測', () => {
    cy.checkA11y()
  })

  it('搜尋結果無障礙檢測', () => {
    cy.get('[data-testid="search-input"]').type('2330')
    cy.get('[data-testid="stock-list"]').should('be.visible')
    cy.checkA11y()
  })
})
```

### 手動測試 Checklist

- [ ] 只用鍵盤完成主要流程
- [ ] 使用螢幕閱讀器（VoiceOver/NVDA）測試
- [ ] 放大至 200% 檢查排版
- [ ] 使用色彩對比檢查工具
- [ ] 關閉 CSS 檢查內容順序

---

## AI 協作指南

### 讓 AI 幫你檢查無障礙

**Prompt 範本**：

```
請檢查以下 design.md 的無障礙規格：

{design.md 內容}

請檢查：
1. 色彩對比是否符合 WCAG AA
2. 互動元素是否有足夠的觸控區域
3. 是否定義了焦點狀態
4. 是否有適當的 ARIA 標籤
5. 鍵盤導航是否完整

請列出問題和建議。
```

### 讓 AI 幫你產生 ARIA 標籤

**Prompt 範本**：

```
請根據以下元件清單，建議適當的 ARIA 標籤：

{元件清單}

每個元件請建議：
1. 適當的 role
2. 需要的 aria-* 屬性
3. 使用範例
```

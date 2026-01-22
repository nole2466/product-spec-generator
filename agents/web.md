# Web Developer 角色定義

> Web Developer：網頁前端實作

---

## 角色概述

| 項目 | 說明 |
|-----|------|
| **核心職責** | 根據設計和 API 契約實作網頁介面 |
| **主要產出** | Web 程式碼（直接實作） |
| **協作對象** | PD、Backend RD、App Developer |
| **不負責** | 需求定義、視覺設計、API 設計、App 實作 |

---

## 與 App Developer 的分工

| 項目 | Web Developer | App Developer |
|-----|--------------|---------------|
| 平台 | 瀏覽器（Desktop/Mobile Web） | iOS / Android |
| 技術棧 | React, Vue, Angular 等 | Swift, Kotlin, Flutter, React Native 等 |
| 發布 | 部署到 Server | 上架 App Store / Google Play |
| 更新 | 即時生效 | 需要用戶更新 |

---

## 輸入 / 輸出

### 輸入（你需要讀什麼）

| 來源 | 文件 | 目的 |
|-----|------|------|
| PD | design.md | 了解 UI 規格 |
| PD | mockup/ | 了解視覺設計 |
| Backend | contract.md | 了解 API 格式 |

### 輸出（你需要產出什麼）

| 產出 | 說明 |
|-----|------|
| Web 程式碼 | 直接實作，不需要額外文件 |

**注意**：Web Developer 不需要產出 spec 文件，直接從 design.md 和 contract.md 實作。

---

## 職責邊界

### ✅ Web Developer 該做的

- 根據 design.md 實作 Web UI
- 根據 contract.md 串接 API
- 實作互動和動畫
- 處理各種狀態（Loading/Error/Empty）
- 決定 Web 前端技術選型
- 處理瀏覽器相容性
- 實作 RWD（響應式設計）
- 處理 SEO 需求

### ❌ Web Developer 不該做的

- 改變 API 格式（Backend 的事）
- 改變 UI 設計（PD 的事）
- 改變功能邏輯（PD 的事）
- 實作 App 版本（App Developer 的事）

### 邊界範例

```markdown
✅ Web Developer 說：
「我用 React Query 做 API 快取」
「我用 Framer Motion 做動畫」
「我用 Next.js 處理 SSR」

❌ Web Developer 不該自己決定：
「我覺得搜尋結果改成顯示 30 筆比較好」
（這要跟 PD/Backend 討論）

❌ Web Developer 不該自己決定：
「API 回傳格式不好用，我自己改一下」
（這要跟 Backend 討論，更新 contract.md）
```

---

## Web 專屬考量

### 瀏覽器相容性

在 design.md 或 acceptance.md 確認支援的瀏覽器：

| 瀏覽器 | 版本 | 優先級 |
|-------|------|:------:|
| Chrome | 最新 2 版 | 必須 |
| Safari | 最新 2 版 | 必須 |
| Firefox | 最新 2 版 | 必須 |
| Edge | 最新 2 版 | 必須 |
| IE | 11 | 視專案需求 |

### RWD 斷點

依照 design.md 定義的斷點實作：

| 名稱 | 寬度範圍 | 說明 |
|-----|---------|------|
| Mobile | < 768px | 手機 |
| Tablet | 768px - 1024px | 平板 |
| Desktop | > 1024px | 桌機 |

### SEO 考量

| 項目 | 處理方式 |
|-----|---------|
| Meta Tags | 動態設定 title, description |
| 結構化資料 | JSON-LD |
| SSR/SSG | 視 SEO 需求選擇 |
| 語意化 HTML | 使用正確的 HTML 標籤 |

### 效能優化

| 項目 | 目標 | 量測工具 |
|-----|------|---------|
| LCP | < 2.5s | Lighthouse |
| FID | < 100ms | Lighthouse |
| CLS | < 0.1 | Lighthouse |
| Bundle Size | 視專案而定 | webpack-bundle-analyzer |

---

## 常用技術棧

### 框架選擇

| 框架 | 適用情境 |
|-----|---------|
| React | SPA、複雜互動 |
| Next.js | SSR/SSG、SEO 需求 |
| Vue | 中小型專案 |
| Nuxt | Vue + SSR |
| Angular | 企業級應用 |

### 狀態管理

| 方案 | 適用情境 |
|-----|---------|
| React Query | Server State |
| Zustand | 輕量 Client State |
| Redux | 複雜 Client State |
| Jotai | 原子化狀態 |

### CSS 方案

| 方案 | 特點 |
|-----|------|
| Tailwind CSS | Utility-first |
| CSS Modules | Scoped CSS |
| Styled Components | CSS-in-JS |
| Sass | 傳統預處理器 |

---

## 讀取文件指南

### 從 design.md 讀取

**需要注意的區塊**：

1. **頁面結構**：了解佈局和元件組成
2. **狀態設計**：所有狀態都要實作
3. **互動規格**：動畫時間、觸發條件
4. **RWD 規格**：各斷點的佈局差異

**Checklist**：
- [ ] 所有頁面都有實作
- [ ] 所有狀態都有處理
- [ ] 所有互動都有實作
- [ ] 所有斷點都有測試

### 從 contract.md 讀取

**需要注意的區塊**：

1. **Data Schema**：資料型別定義
2. **API Endpoints**：Request/Response 格式
3. **Error Codes**：錯誤處理方式

**Checklist**：
- [ ] API 呼叫格式正確
- [ ] 回應資料正確解析
- [ ] 所有錯誤都有處理

---

## 實作原則

### 狀態處理

每個頁面都要處理以下狀態：

| 狀態 | 處理方式 |
|-----|---------|
| Initial | 初始畫面 |
| Loading | 顯示載入中（Skeleton/Spinner）|
| Success | 顯示資料 |
| Empty | 顯示空狀態 |
| Error | 顯示錯誤訊息 + 重試 |

### 錯誤處理

根據 contract.md 的錯誤碼處理：

| 錯誤碼 | 處理方式 |
|-------|---------|
| UNAUTHORIZED | 導向登入頁 |
| NOT_FOUND | 顯示「找不到」 |
| RATE_LIMITED | 顯示「請稍後再試」|
| INTERNAL_ERROR | 顯示「系統錯誤」+ 重試按鈕 |

---

## 審核 Checklist

當 Web Developer 審核規格時：

### 技術可行性
- [ ] UI 設計可在 Web 實作
- [ ] 動畫效果可實作
- [ ] 效能要求合理

### API 可用性
- [ ] API 回傳的欄位足夠顯示
- [ ] 分頁設計符合 UI 需求
- [ ] 錯誤碼涵蓋所有情境

### Web 專屬
- [ ] RWD 斷點定義清楚
- [ ] 瀏覽器相容性明確
- [ ] SEO 需求明確

### 一致性
- [ ] design.md 和 contract.md 資料對得上
- [ ] 錯誤處理有對應的 UI 狀態

---

## 常見問題

### Q: 發現 API 回傳缺少需要的欄位？

**A**: 不要自己造假資料，請：
1. 確認 design.md 是否真的需要這個欄位
2. 和 Backend 討論，更新 contract.md
3. 等 contract.md 更新後再實作

### Q: 發現設計稿有問題？

**A**: 不要自己改設計，請：
1. 和 PD 討論
2. 等 design.md 更新後再實作

### Q: Web 和 App 規格不一致怎麼辦？

**A**: 
1. 確認是否為刻意差異（平台特性）
2. 若應該一致，和 PD 討論統一規格
3. 若為平台特性，各自按規格實作

---

## AI 協作指南

### 讓 AI 幫你實作

**Prompt 範本**：

```
我是 Web Developer，需要根據以下規格實作網頁 UI。

design.md:
{內容}

contract.md:
{內容}

技術棧：React + Next.js + Tailwind CSS

請幫我實作：
1. 頁面結構和元件
2. API 串接（使用 React Query）
3. 所有狀態處理（Loading/Empty/Error）
4. RWD 響應式設計
5. 互動和動畫

請確保：
- 所有設計稿的狀態都有實作
- 所有錯誤碼都有處理
- 支援 Mobile/Tablet/Desktop 斷點
```

### 讓 AI 審核規格

**Prompt 範本**：

```
請以 Web Developer 的角度審核以下規格：

design.md:
{內容}

contract.md:
{內容}

檢查項目：
1. UI 設計是否可在 Web 實作
2. API 回傳欄位是否足夠
3. RWD 斷點是否定義清楚
4. 瀏覽器相容性是否明確
5. 兩份文件是否一致

請列出問題和建議。
```

# 核心原則

> 所有角色（人類或 AI）都必須遵守的原則

---

## 原則 1：角色導向（Role-Oriented）

每個角色有明確的：
- **輸入**：需要讀什麼
- **輸出**：需要產出什麼
- **職責邊界**：什麼該做、什麼不該做

### 角色職責總覽

| 角色 | 核心職責 | 主要產出 |
|-----|---------|---------|
| PM | 定義需求和優先級 | prd.md |
| PD | 需求轉規格、設計體驗、協調各方 | spec.md |
| Backend | API 和資料結構設計 | contract.md |
| Web | 網頁前端實作 | Web 程式碼 |
| App | iOS/Android App 實作 | App 程式碼 |
| QA | 驗收標準定義 | acceptance.md |

### 角色不越界

```
✅ PM 說：「用戶需要能搜尋股票」
❌ PM 說：「用 Elasticsearch 實作搜尋」（這是 Backend 的決定）

✅ PD 說：「搜尋結果要有 Loading 狀態，使用 Skeleton 效果」
❌ PD 說：「用 React Suspense 做 Loading」（這是 Frontend 的決定）
```

---

## 原則 2：完整結構（Complete Structure）

企業級專案使用完整的文件結構。

### 標準結構

```
specs/{feature}/
├── prd.md          # PM 產出
├── spec.md         # PD 產出
├── contract.md     # Backend 產出
└── acceptance.md   # QA 產出
```

### 文件產出順序

```
PM 產出 prd.md
    ↓
PD 產出 spec.md（含設計規格、介面描述）
    ↓
Backend 產出 contract.md
    ↓
QA 產出 acceptance.md
```

---

## 原則 3：Human-AI Hybrid

文件格式讓人類和 AI 都能：
- **讀懂**：結構清晰、無歧義
- **產出**：有模板、有範例
- **驗證**：有 checklist、可測試

### AI 友善格式

**Metadata Header**：
```markdown
---
id: FE-001
title: 搜尋股票
status: draft | review | approved | done
owner: pm | pd | backend | frontend | qa
version: 1.0
---
```

**Section 標準化**：
```markdown
## Overview        # 30 秒讀完，必要
## Requirements    # 需求清單，必要
## Specifications  # 詳細規格，必要
## Acceptance      # 驗收標準，建議
## Changelog       # 變更歷史，建議
```

**AI 指令區塊**（可選）：
```markdown
<!-- @ai-context
role: frontend
task: implement
dependencies: [contract.md, design.md]
-->
```

---

## 原則 4：最小化 Context

只讀需要的，避免資訊過載。

### 角色讀取矩陣

| 角色 | prd.md | spec.md | contract.md | acceptance.md |
|-----|:------:|:-------:|:-----------:|:-------------:|
| PM | ✅ 寫 | 👀 審 | - | 👀 審 |
| PD | 👀 讀 | ✅ 寫 | 👀 審 | 👀 審 |
| Backend | 👀 讀 | 👀 讀 | ✅ 寫 | - |
| Web | - | 👀 讀 | 👀 讀 | - |
| App | - | 👀 讀 | 👀 讀 | - |
| QA | 👀 讀 | 👀 讀 | 👀 讀 | ✅ 寫 |

### 文件大小原則

- **Overview**：< 30 秒讀完
- **單一文件**：< 500 行
- **單一章節**：< 100 行

超過就該拆分。

---

## 原則 5：What vs How 分離

規格文件描述「做什麼」，不描述「怎麼做」。

### 正確示範

```markdown
## 搜尋功能

用戶輸入關鍵字，系統回傳符合的股票列表。

### 規格
- 輸入：關鍵字（1-50 字元）
- 輸出：股票列表（最多 20 筆）
- 回應時間：< 500ms
```

### 錯誤示範

```markdown
## 搜尋功能

用 Elasticsearch 建立倒排索引，透過 React Query 做快取...

（這是實作細節，不該出現在規格中）
```

### 例外

`contract.md` 可以包含技術細節，因為它是前後端的「合約」。

---

## 原則 6：變更可追蹤

每個文件都要有版本和變更歷史。

### Metadata 版本

```markdown
---
version: 1.2
last_updated: 2024-03-01
---
```

### Changelog 區塊

```markdown
## Changelog

### v1.2 - 2024-03-01
- 新增排序功能

### v1.1 - 2024-02-15
- 調整搜尋結果上限從 10 改為 20

### v1.0 - 2024-02-01
- 初版
```

### 內文變更標註

```markdown
搜尋結果最多顯示 **20 筆** <!-- v1.1: 從 10 改為 20 -->
```

---

## 原則 7：可驗證

每個需求都要有對應的驗收標準。

### 好的驗收標準

```markdown
## 驗收：搜尋功能

| # | 情境 | 操作 | 預期結果 |
|:-:|-----|------|---------|
| 1 | 正常搜尋 | 輸入「2330」 | 顯示台積電 |
| 2 | 無結果 | 輸入「zzzzz」 | 顯示「無搜尋結果」 |
| 3 | 空輸入 | 不輸入，按搜尋 | 顯示錯誤提示 |
```

### 壞的驗收標準

```markdown
## 驗收

- 搜尋功能要正常運作
- 使用者體驗要好

（太模糊，無法測試）
```

---

## Checklist：文件品質自檢

產出文件後，確認以下項目：

### 格式檢查
- [ ] 有 Metadata Header
- [ ] 有 Overview 區塊
- [ ] 單一文件 < 500 行

### 內容檢查
- [ ] 只描述 What，不描述 How
- [ ] 每個需求都有驗收標準
- [ ] 無歧義，只有一種解讀方式

### 角色檢查
- [ ] 沒有越界（PM 不寫技術細節）
- [ ] 標註了 owner
- [ ] 標註了需要誰 review

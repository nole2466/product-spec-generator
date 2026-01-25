# 範例：商品搜尋功能

這是一個完整的功能規格範例，展示從 PRD 到驗收的完整流程。

## 📁 文件結構

```
product-search/
├── README.md         # 你在這裡
├── prd.md            # PM 的功能需求
├── spec.md           # PD 的功能規格（含設計）
├── contract.md       # Backend 的 API 契約
└── acceptance.md     # QA 的驗收標準
```

## 👥 角色與產出

| 角色 | 產出 | 負責人 |
|-----|------|-------|
| PM | [prd.md](./prd.md) | @pm-david |
| PD | [spec.md](./spec.md) | @pd-sarah |
| Backend | [contract.md](./contract.md) | @backend-tom |
| QA | [acceptance.md](./acceptance.md) | @qa-emma |

## 📋 功能概述

### 需求背景

用戶反映難以在大量商品中找到想要的商品，需要提供搜尋功能。

### 核心功能

1. **關鍵字搜尋**：輸入關鍵字搜尋商品
2. **搜尋建議**：輸入時即時顯示建議
3. **結果篩選**：按價格、分類、評價篩選
4. **結果排序**：按相關度、價格、銷量排序

### 成功指標

| 指標 | 目標 |
|-----|------|
| 搜尋使用率 | > 40% |
| 搜尋成功率 | > 80% |
| 搜尋轉換率 | > 5% |

## 🔗 文件流程

```
prd.md (PM)
    │ PM 定義需求和目標
    ▼
spec.md (PD)
    │ PD 轉換為詳細規格和設計
    ▼
contract.md (Backend)
    │ Backend 定義 API 契約
    ▼
acceptance.md (QA)
    │ QA 定義驗收標準
    ▼
實作 & 測試
```

## 💡 學習重點

### PRD（PM）
- 如何描述背景和目標
- 如何定義成功指標（KPI）
- 如何撰寫 User Stories
- 如何區分 In/Out of Scope

### Spec（PD）
- 如何將需求轉為功能規格
- 如何用 ASCII 描述介面
- 如何定義互動細節
- 如何定義元件規格

### Contract（Backend）
- 如何設計 RESTful API
- 如何定義資料結構
- 如何處理錯誤碼
- 如何定義效能需求

### Acceptance（QA）
- 如何撰寫測試案例
- 如何設計邊界測試
- 如何定義驗收標準
- 如何進行相容性測試

## 📊 時程

| 里程碑 | 日期 | 狀態 |
|-------|------|:----:|
| PRD 定稿 | 2024-01-15 | ✅ |
| Spec 完成 | 2024-01-22 | ✅ |
| Contract 完成 | 2024-01-25 | ✅ |
| Acceptance 完成 | 2024-01-28 | ✅ |
| 開發完成 | 2024-02-15 | 🔵 |
| 上線 | 2024-03-01 | ⚪ |

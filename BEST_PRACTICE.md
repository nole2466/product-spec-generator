# Best Practice 快速上手指南

> 讓每個角色都能在 10 分鐘內開始使用這套規格系統

---

## 📍 你是誰？直接跳到你的章節

| 角色 | 快速入口 |
|-----|---------|
| PM（產品經理） | [→ PM 篇](#pm-篇) |
| PD（產品設計師） | [→ PD 篇](#pd-篇) |
| Backend（後端工程師） | [→ Backend 篇](#backend-篇) |
| Frontend（Web/App 工程師） | [→ Frontend 篇](#frontend-篇) |
| QA（測試工程師） | [→ QA 篇](#qa-篇) |
| Scrum Master（流程協調） | [→ Scrum Master 篇](#scrum-master-篇) |
| Tech Lead（技術主管） | [→ Tech Lead 篇](#tech-lead-篇) |
| 新人 Onboarding | [→ 新人篇](#新人篇) |

---

## PM 篇

### 你的核心職責

```
定義「做什麼」和「為什麼做」
```

### 5 分鐘快速開始

**Step 1**：複製範本
```bash
cp templates/prd.md specs/{你的功能名稱}/prd.md
```

**Step 2**：填寫這 5 個必填區塊
1. **背景目標** - 為什麼要做？解決什麼問題？
2. **成功指標** - 怎麼衡量成功？（KPI）
3. **User Stories** - 用戶想要什麼？
4. **功能清單** - 要做哪些功能？優先級？
5. **範圍定義** - 這次做什麼？不做什麼？

**Step 3**：請 PD Review
```
@PD 請幫我 Review 這份 PRD，確認是否可執行
```

### 常見錯誤 ❌

| 錯誤 | 正確做法 |
|-----|---------|
| 沒有寫成功指標 | 一定要有可量化的 KPI |
| In/Out Scope 不清楚 | 明確列出不做什麼，避免 scope creep |
| User Story 太模糊 | 用「作為...我想要...以便...」格式 |
| 一次塞太多功能 | 按優先級分 P0/P1/P2，先做 P0 |

### 你需要讀的文件

```
必讀：core/principles.md
參考：templates/prd.md, examples/product-search/prd.md
```

### Checklist

```markdown
## PRD 自檢清單

- [ ] 背景和目標清楚
- [ ] KPI 可量化
- [ ] User Stories 完整
- [ ] 功能清單有優先級
- [ ] In/Out Scope 明確
- [ ] PD 已 Review
```

---

## PD 篇

### 你的核心職責

```
把「做什麼」轉成「怎麼做」，讓工程師能直接開發
定義和維護 Design System，確保設計一致性
```

### 5 分鐘快速開始

**Step 1**：讀 PRD，確認理解需求
```
先確認：目標、User Stories、功能清單、範圍
```

**Step 2**：複製範本
```bash
cp templates/spec.md specs/{功能名稱}/spec.md
```

**Step 3**：填寫核心區塊

1. **功能規格** - 每個功能的觸發條件、處理邏輯、輸出結果
2. **介面描述** - 用 ASCII 畫出畫面結構
3. **互動規格** - 用戶怎麼操作、系統怎麼反應
4. **狀態設計** - Loading、Empty、Error 狀態

**Step 4**：請技術團隊 Review
```
@Backend @Web @App 請確認這份 Spec 是否可實作
```

### Design Token 使用（必學）

**為什麼要用 Token？**
- 確保全產品設計一致
- 方便全域調整（改一處，處處改）
- 工程師和設計師說同一種語言

**Token 位置**：`templates/design-system/tokens.md`

**兩大類別**：

| 類別 | 內容 | 範例 |
|-----|------|------|
| **Color** | 品牌色、文字色、背景色、狀態色 | `color.brand.primary` |
| **Size** | 間距、字體、圓角、元件尺寸 | `size.spacing.md` |

**在 Spec 中這樣寫**：

```markdown
### 主按鈕樣式

| 屬性 | Token | 值 |
|-----|-------|-----|
| 背景色 | `color.brand.primary` | #0066FF |
| 文字色 | `color.text.inverse` | #FFFFFF |
| 高度 | `size.button.md` | 40px |
| 圓角 | `size.radius.md` | 8px |
```

**❌ 錯誤**：直接寫 `背景色 #0066FF`
**✅ 正確**：引用 Token `color.brand.primary`

### ASCII 介面描述技巧

```
┌─────────────────────────────────────┐
│ Header                              │
├─────────────────────────────────────┤
│                                     │
│           主要內容區                 │
│                                     │
├─────────────────────────────────────┤
│ Footer / Tab Bar                    │
└─────────────────────────────────────┘
```

**常用符號**：
- `┌ ┐ └ ┘` - 四個角
- `─` - 橫線
- `│` - 直線
- `├ ┤ ┬ ┴ ┼` - 交叉點

### 常見錯誤 ❌

| 錯誤 | 正確做法 |
|-----|---------|
| 沒有畫 Error 狀態 | 每個畫面都要有 Loading/Empty/Error |
| 互動細節不清楚 | 明確寫出觸發條件和反應 |
| 沒有考慮邊界情況 | 想清楚：空值？超長？超多？ |
| 直接跳去畫 Figma | 先用 ASCII 確認流程，再畫高保真 |
| 直接寫色碼/數值 | 引用 Design Token |

### 你需要讀的文件

```
必讀：core/principles.md, agents/pd.md
必讀：templates/design-system/tokens.md（Design Token）
參考：templates/spec.md, examples/product-search/spec.md
```

### Checklist

```markdown
## Spec 自檢清單

- [ ] 所有功能都有詳細規格
- [ ] 介面描述清楚（ASCII）
- [ ] 三種狀態都有設計（Loading/Empty/Error）
- [ ] 互動規格完整
- [ ] **所有樣式都引用 Design Token**
- [ ] Backend 已確認 API 可行
- [ ] Frontend 已確認可實作
```

---

## Backend 篇

### 你的核心職責

```
定義 API 契約，讓前後端能獨立開發、最後順利串接
```

### 5 分鐘快速開始

**Step 1**：讀 Spec，理解功能需求
```
重點看：功能規格、資料對應、非功能需求
```

**Step 2**：複製範本
```bash
cp templates/contract.md specs/{功能名稱}/contract.md
```

**Step 3**：定義 API

1. **API 總覽** - 列出所有 Endpoints
2. **Request** - Headers、Query Parameters、Body
3. **Response** - 成功和錯誤的回傳格式
4. **資料結構** - TypeScript interface 定義

**Step 4**：請 Frontend Review
```
@Web @App 請確認這份 API 契約是否符合需求
```

### API 設計原則

```
✅ RESTful 風格
✅ 一致的回傳格式
✅ 明確的錯誤碼
✅ 版本控制 (/api/v1/)
```

**標準回傳格式**：
```json
// 成功
{
  "success": true,
  "data": { ... }
}

// 失敗
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "錯誤訊息"
  }
}
```

### 常見錯誤 ❌

| 錯誤 | 正確做法 |
|-----|---------|
| 沒有定義錯誤碼 | 每個錯誤都要有 code |
| Response 格式不一致 | 統一用 success/data/error 結構 |
| 沒有寫效能需求 | 要寫回應時間目標（如 < 500ms） |
| 欄位命名不一致 | 統一用 camelCase |

### 你需要讀的文件

```
必讀：core/principles.md, agents/backend.md
參考：templates/contract.md, examples/product-search/contract.md
```

### Checklist

```markdown
## Contract 自檢清單

- [ ] 所有 API Endpoints 都有定義
- [ ] Request/Response 格式完整
- [ ] 錯誤碼都有定義
- [ ] 資料結構用 TypeScript 定義
- [ ] 效能需求有寫
- [ ] Frontend 已確認可串接
```

---

## Frontend 篇

### 你的核心職責

```
按照 Spec 和 Contract 實作介面，確保用戶體驗
```

### 5 分鐘快速開始

**Step 1**：讀這兩份文件
```
1. spec.md - 介面長什麼樣、怎麼互動
2. contract.md - API 怎麼串接
```

**Step 2**：確認你理解

- [ ] 所有畫面的結構
- [ ] 三種狀態（Loading/Empty/Error）
- [ ] 互動細節（點擊、滑動、輸入）
- [ ] API 的 Request/Response 格式

**Step 3**：有問題立刻問

```
看不懂 Spec？→ 問 PD
API 格式有問題？→ 問 Backend
```

### 實作 Checklist

```markdown
## 開發自檢清單

### 畫面
- [ ] 所有畫面都實作了
- [ ] RWD / 不同螢幕尺寸
- [ ] 三種狀態都有處理

### 互動
- [ ] 按鈕點擊有 feedback
- [ ] Loading 有顯示
- [ ] Error 有顯示並可重試

### API 串接
- [ ] 所有 API 都串接了
- [ ] 錯誤處理完整
- [ ] 網路斷線有處理
```

### 常見錯誤 ❌

| 錯誤 | 正確做法 |
|-----|---------|
| 沒看 Spec 就開始做 | 先讀完 Spec，有問題先問 |
| 忘記處理 Error 狀態 | 每個 API 都要有錯誤處理 |
| 自己猜 API 格式 | 照 Contract 實作，有問題問 Backend |
| 只測試 Happy Path | 也要測試邊界情況和錯誤情況 |

### 你需要讀的文件

```
必讀：specs/{功能}/spec.md, specs/{功能}/contract.md
參考：agents/web.md 或 agents/app.md
```

---

## QA 篇

### 你的核心職責

```
定義驗收標準，確保功能符合需求
```

### 5 分鐘快速開始

**Step 1**：讀所有規格文件
```
prd.md → spec.md → contract.md
```

**Step 2**：複製範本
```bash
cp templates/acceptance.md specs/{功能名稱}/acceptance.md
```

**Step 3**：撰寫測試案例

1. **功能測試** - 正常流程能不能跑
2. **邊界測試** - 極端情況會不會壞
3. **錯誤處理** - 錯誤有沒有正確顯示
4. **狀態測試** - Loading/Empty/Error 對不對

**Step 4**：定義驗收標準
```
- 所有 P0 測試通過
- 95% P1 測試通過
- 無 Critical/Major Bug
```

### 測試案例撰寫技巧

```markdown
#### TC-001: {測試案例名稱}

| 項目 | 內容 |
|-----|------|
| **前置條件** | {測試前的狀態} |
| **優先級** | P0 / P1 / P2 |

**測試步驟**：
1. {步驟 1}
2. {步驟 2}
3. {步驟 3}

**預期結果**：
- {結果 1}
- {結果 2}
```

### 常見錯誤 ❌

| 錯誤 | 正確做法 |
|-----|---------|
| 只測試 Happy Path | 一定要測試邊界和錯誤情況 |
| 測試案例太模糊 | 步驟要具體，結果要明確 |
| 沒有優先級 | P0 是阻擋上線的，要分清楚 |
| 沒有測試 Spec 的狀態設計 | Loading/Empty/Error 都要測 |

### 你需要讀的文件

```
必讀：所有規格文件（prd, spec, contract）
參考：templates/acceptance.md, examples/product-search/acceptance.md
```

### Checklist

```markdown
## Acceptance 自檢清單

- [ ] 所有功能都有測試案例
- [ ] 邊界測試完整
- [ ] 錯誤處理測試完整
- [ ] 狀態測試完整
- [ ] 測試案例有優先級
- [ ] 驗收標準明確
```

---

## Scrum Master 篇

### 你的核心職責

```
協調各角色、推進開發階段、追蹤進度、移除障礙
```

### AI Scrum Master 何時出現？

AI Scrum Master 會在以下時機**自動協助**：

| 時機 | AI 協助內容 |
|-----|------------|
| 📋 **階段轉換時** | 檢查前一階段文件是否完成，確認可以進入下一階段 |
| 🔴 **進度落後時** | 識別阻塞問題，建議解決方案 |
| 📊 **Sprint 規劃時** | 協助拆解任務、識別依賴關係 |
| 🔍 **Review 前** | 預檢文件一致性，提前發現問題 |
| 📝 **會議後** | 整理會議紀錄、追蹤 Action Items |

### 使用 AI Scrum Master

```bash
# 檢視專案狀態
/scrum-master status

# 規劃 Sprint
/scrum-master plan [backlog items]

# 識別風險
/scrum-master risks

# 執行回顧
/scrum-master retro [sprint info]
```

### 開發階段流程

```
需求階段 (PM)
    │ ← AI 檢查：PRD 是否完整？
    ▼
規格階段 (PD)
    │ ← AI 檢查：Spec 是否可執行？
    ▼
設計審核 (All)
    │ ← AI 檢查：各角色 Review 是否完成？
    ▼
API 設計 (Backend) + 驗收標準 (QA)
    │ ← AI 檢查：Contract 和 Acceptance 是否一致？
    ▼
開發階段 (RD)
    │ ← AI 追蹤：進度是否正常？有無阻塞？
    ▼
測試驗收 (QA)
    │ ← AI 檢查：Bug 是否都修復？
    ▼
上線
```

### 階段轉換檢查點

| 從 → 到 | AI 檢查項目 |
|--------|------------|
| 需求 → 規格 | PRD 已 approved、目標明確、KPI 可量化 |
| 規格 → 審核 | Spec 完整、狀態設計完整、Design Token 引用正確 |
| 審核 → API 設計 | Review 意見已處理、Spec 已 approved |
| API → 開發 | Contract 已確認、Acceptance 已完成 |
| 開發 → 測試 | 功能完成、已部署測試環境 |
| 測試 → 上線 | 無 Critical/Major Bug、驗收通過 |

### 進度追蹤模板

```markdown
## Sprint 狀態看板

**Sprint**: {Sprint 名稱}
**目標**: {Sprint 目標}

| 階段 | 狀態 | 負責人 | 預計完成 | 實際完成 |
|-----|:----:|-------|---------|---------|
| PRD | ✅ | PM | MM/DD | MM/DD |
| Spec | 🔵 | PD | MM/DD | - |
| Review | ⚪ | All | MM/DD | - |
| Contract | ⚪ | Backend | MM/DD | - |
| 開發 | ⚪ | RD | MM/DD | - |
| 測試 | ⚪ | QA | MM/DD | - |

**圖例**：✅ 完成 | 🔵 進行中 | ⚪ 待開始 | 🔴 阻塞

### 阻塞問題

| 問題 | 影響 | 負責人 | 狀態 |
|-----|------|-------|:----:|
| {問題描述} | {影響範圍} | SM | 🔵 |
```

### 常見錯誤 ❌

| 錯誤 | 正確做法 |
|-----|---------|
| 階段沒完成就往下走 | 確認檢查點都通過再進入下一階段 |
| 阻塞問題沒有追蹤 | 記錄所有阻塞，指派負責人，定期更新 |
| 進度只看開發 | 要追蹤整個流程，包含需求、規格、測試 |
| 沒有預警風險 | 發現延誤風險要提早溝通 |

### 你需要讀的文件

```
必讀：agents/scrum-master.md
參考：core/review-workflow.md, templates/backlog/
```

### Checklist

```markdown
## Scrum Master 自檢清單

### 階段管理
- [ ] 各階段狀態清楚
- [ ] 檢查點都有確認
- [ ] 阻塞問題有追蹤

### 進度追蹤
- [ ] Sprint 目標明確
- [ ] 進度看板更新
- [ ] 風險有識別和處理

### 協調溝通
- [ ] 各角色了解自己的任務
- [ ] 依賴關係清楚
- [ ] 問題有及時溝通
```

---

## Tech Lead 篇

### 你的核心職責

```
確保整個流程順暢、文件品質、團隊協作
```

### 專案初始化 Checklist

```markdown
## 專案設置

### 目錄結構
- [ ] 建立 specs/ 目錄
- [ ] 建立 backlog/ 目錄
- [ ] 建立 knowledge/ 目錄
- [ ] 複製必要範本

### 流程設置
- [ ] 確認團隊都讀過 core/principles.md
- [ ] 設定 MR 流程和範本
- [ ] 設定 Review 機制

### 知識庫
- [ ] 建立業務規則文件
- [ ] 建立術語表
- [ ] 建立第三方串接文件
```

### 你要關注的重點

| 階段 | 關注點 |
|-----|-------|
| PRD Review | 目標明確嗎？KPI 可衡量嗎？ |
| Spec Review | 技術可行嗎？有遺漏嗎？ |
| Contract Review | API 設計合理嗎？前後端同意嗎？ |
| 開發中 | 進度正常嗎？有阻塞嗎？ |
| 驗收 | 測試覆蓋夠嗎？Bug 都修了嗎？ |

### 文件維護

確保團隊遵守 `core/document-maintenance.md`：
- 規格變更要更新文件
- 迭代結束要更新 Backlog
- 功能上線要更新狀態

### 你需要讀的文件

```
必讀：所有 core/ 文件
重要：core/document-maintenance.md, core/review-workflow.md
```

---

## 新人篇

### 第一天：了解全貌

```
1. 讀 README.md（5 分鐘）
   → 了解這是什麼

2. 讀 core/principles.md（10 分鐘）
   → 了解核心原則

3. 讀 core/glossary.md（5 分鐘）
   → 了解術語
```

### 第二天：了解你的角色

```
1. 讀 agents/{你的角色}.md
   → 了解你要做什麼

2. 讀 templates/ 裡相關的範本
   → 了解要產出什麼

3. 讀 examples/product-search/ 的範例
   → 看看填完長什麼樣
```

### 第三天：實際操作

```
1. 找一個小功能練習
2. 按照範本填寫
3. 請資深同事 Review
4. 根據回饋修改
```

### 新人常見問題

| 問題 | 答案 |
|-----|------|
| 文件太多不知道從哪開始？ | 只讀你角色需要的，見上方 |
| 範本每個欄位都要填嗎？ | 必填的要填，選填的看情況 |
| 填錯了怎麼辦？ | 沒關係，會有 Review，改就好 |
| 不確定怎麼填？ | 看 examples/ 裡的範例 |

### 學習路徑

```
Week 1: 了解系統，讀完核心文件
Week 2: 開始寫第一份文件，多問多改
Week 3: 獨立完成文件，接受 Review
Week 4: 開始 Review 別人的文件
```

---

## 📚 快速參考

### 文件對照表

| 我要... | 看這份文件 |
|--------|-----------|
| 了解整體架構 | `README.md`, `SKILL.md` |
| 了解核心原則 | `core/principles.md` |
| 看範本 | `templates/` |
| 看完整範例 | `examples/product-search/` |
| 了解我的角色 | `agents/{角色}.md` |
| 了解審核流程 | `core/review-workflow.md` |
| 了解文件維護 | `core/document-maintenance.md` |
| 協調開發流程 | `agents/scrum-master.md` |

### 常用指令

```bash
# 建立新功能目錄
mkdir -p specs/{功能名稱}

# 複製範本
cp templates/prd.md specs/{功能名稱}/
cp templates/spec.md specs/{功能名稱}/
cp templates/contract.md specs/{功能名稱}/
cp templates/acceptance.md specs/{功能名稱}/

# 建立 Feature 任務
cp templates/backlog/feature.md backlog/features/{功能名稱}.md
```

### 狀態圖示

| 圖示 | 意思 |
|:---:|------|
| 💡 | 規劃中 |
| 📋 | 規格中 / 待開始 |
| 🚧 | 開發中 / 進行中 |
| 🔍 | Review 中 |
| ✅ | 已完成 / 已上線 |
| ❌ | 已取消 / 已下線 |

---

## 變更紀錄

| 日期 | 版本 | 變更內容 | 作者 |
|-----|------|---------|------|
| {日期} | 1.0 | 初版 | @{username} |

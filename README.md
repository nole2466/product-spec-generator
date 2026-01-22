# Product Spec Generator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

> From Requirements to Code, Together with AI

讓產品團隊和 AI 協作產出規格的企業級標準。

**繁體中文** | [English](./docs/en/README.md)

---

## ✨ 特色

- **🎭 角色導向**：PM、PD、Backend、Web、App、QA、Scrum Master 各有明確職責
- **🤖 Human-AI Hybrid**：真人和 AI 都能讀懂、都能產出
- **📚 知識集中**：商業邏輯、領域知識、第三方串接統一管理
- **🔄 審核流程**：內建多角色審核機制

---

## 🚀 快速開始

### 方式一：Claude Code Plugin（推薦）

在 Claude Code 中安裝 Plugin，即可使用所有角色技能：

```bash
# 1. 加入 Marketplace
/plugin marketplace add nole2466/product-spec-generator

# 2. 安裝 Plugin
/plugin install product-spec-generator@product-spec-marketplace

# 3. 使用 Skills
/pm generate 購物車功能           # PM 產出 PRD
/pd generate [PRD 內容]          # PD 產出 Spec
/backend generate [Spec 內容]    # Backend 產出 API Contract
/qa generate [Spec 內容]         # QA 產出驗收標準
/scrum-master status             # 追蹤專案進度
/review [Spec 內容]              # 多角色審核
```

**可用的 Skills：**

| Skill | 說明 | 使用方式 |
|-------|------|----------|
| `/pm` | Product Manager | 產出 PRD 或審核需求 |
| `/pd` | Product Designer | 產出 Spec + 設計規格 |
| `/backend` | Backend Developer | 產出 API Contract |
| `/data-schema` | Data Architect | 定義資料結構、Entity、Enum |
| `/web` | Web Developer | 審核 Web 實作可行性 |
| `/app` | App Developer | 審核 App 實作可行性 |
| `/qa` | QA Engineer | 產出驗收標準 |
| `/scrum-master` | Scrum Master | 協調開發階段、追蹤進度 |
| `/chatbot` | AI Agent Architect | 設計 LLM 聊天機器人規格 |
| `/review` | 多角色審核 | 全面審核規格文件 |

### 方式二：複製到專案

```bash
# 使用 degit
npx degit nole2466/product-spec-generator my-project/specs

# 或直接下載
git clone https://github.com/nole2466/product-spec-generator.git
```

### 2. 建立你的第一個功能規格

```
my-project/
├── specs/
│   ├── _map.md                 # 功能地圖
│   └── user-login/             # 你的第一個功能
│       ├── prd.md              # PM 寫需求
│       ├── spec.md             # PD 寫規格
│       ├── contract.md         # Backend 定義 API
│       └── acceptance.md       # QA 寫驗收
└── knowledge/
    ├── business/               # 商業邏輯
    ├── domain/                 # 領域知識
    └── integrations/           # 第三方串接
```

### 3. 選擇你的角色開始

| 你是誰 | 從這裡開始 |
|-------|-----------|
| PM | 複製 `templates/prd.md` 開始寫需求 |
| PD | 閱讀 PRD，用 `templates/spec.md` 寫規格 |
| Backend | 閱讀 Spec，用 `templates/contract.md` 定義 API |
| QA | 閱讀全部，用 `templates/acceptance.md` 寫驗收 |
| Scrum Master | 閱讀 `agents/scrum-master.md` 協調各階段 |
| AI Agent | 閱讀 `SKILL.md` 了解如何協助 |

---

## 📁 專案結構

```
product-spec-generator/
│
├── .claude-plugin/           # Claude Code Plugin 設定
│   ├── plugin.json           # Plugin 資訊
│   └── marketplace.json      # Marketplace 設定
│
├── skills/                   # Claude Code Skills
│   ├── pm/SKILL.md           # PM 技能
│   ├── pd/SKILL.md           # PD 技能
│   ├── backend/SKILL.md      # Backend 技能
│   ├── data-schema/SKILL.md  # 資料結構設計技能
│   ├── web/SKILL.md          # Web 技能
│   ├── app/SKILL.md          # App 技能
│   ├── qa/SKILL.md           # QA 技能
│   ├── scrum-master/SKILL.md # Scrum Master 技能
│   ├── chatbot/SKILL.md      # AI 聊天機器人設計技能
│   └── review/SKILL.md       # 多角色審核技能
│
├── README.md                 # 你在這裡
├── SKILL.md                  # AI Agent 入口（傳統方式）
├── LICENSE                   # MIT License
├── CONTRIBUTING.md           # 貢獻指南
├── CHANGELOG.md              # 變更日誌
│
├── core/                     # 核心定義
│   ├── principles.md         # 核心原則（必讀）
│   ├── glossary.md           # 術語表
│   └── review-workflow.md    # 審核流程
│
├── agents/                   # 角色定義（詳細版）
│   ├── pm.md
│   ├── pd.md
│   ├── backend.md
│   ├── web.md
│   ├── app.md
│   ├── qa.md
│   └── scrum-master.md
│
├── templates/                # 文件範本
│   ├── _map.md               # 功能地圖
│   ├── prd.md                # PRD 範本
│   ├── spec.md               # Spec 範本
│   ├── contract.md           # API 契約範本
│   └── acceptance.md         # 驗收標準範本
│
├── examples/                 # 完整範例
│   └── product-search/       # 商品搜尋功能
│
└── references/               # 參考指南
    ├── business-logic.md
    ├── domain-knowledge.md
    └── integrations.md
```

---

## 🎭 角色與產出

```
                    ┌─────────────────┐
                    │  Scrum Master   │ ◄── 協調各階段推進
                    │   (協調角色)     │
                    └────────┬────────┘
                             │ 協調
         ┌───────────────────┼───────────────────┐
         ▼                   ▼                   ▼
PM ─────► prd.md        PD ─────► spec.md    QA ─────► acceptance.md
(功能需求)              (功能規格+設計)        (驗收標準)
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
         Backend         Web/App        測試驗收
         contract.md     程式碼實作
         (API 契約)
```

---

## 🤖 與 AI 協作

### 產出模式

讓 AI 扮演某角色產出規格：

```
請以 PD 的身份，根據以下 PRD 產出 spec.md：

{PRD 內容}

請先閱讀 agents/pd.md 和 templates/spec.md
```

### 審核模式

讓 AI 扮演下游角色審核規格：

```
請以 Backend 的身份審核以下 spec.md：

{Spec 內容}

請檢查 API 是否可行，並產出審核結果。
```

詳細說明請見 [SKILL.md](./SKILL.md)

---

## 📖 文件

- [Best Practice 快速上手](./BEST_PRACTICE.md) - **新手必讀**
- [核心原則](./core/principles.md) - 所有人必讀
- [完整範例](./examples/product-search/) - 看看填完長什麼樣
- [AI 協作指南](./SKILL.md) - 如何與 AI 協作

---

## 🤝 貢獻

歡迎貢獻！請閱讀 [CONTRIBUTING.md](./CONTRIBUTING.md) 了解如何參與。

### 貢獻方式

- 🐛 [回報 Bug](https://github.com/nole2466/product-spec-generator/issues)
- 💡 [建議功能](https://github.com/nole2466/product-spec-generator/issues)
- 📝 [改善文件](./CONTRIBUTING.md)
- 🌍 [翻譯](./docs/)

---

## 📜 授權

本專案採用 [MIT License](./LICENSE) 授權。

---

## 🙏 致謝

感謝所有貢獻者和使用者的支持。

---

## 📬 聯絡

- GitHub Issues: [提問或建議](https://github.com/nole2466/product-spec-generator/issues)
- Discussions: [討論區](https://github.com/nole2466/product-spec-generator/discussions)

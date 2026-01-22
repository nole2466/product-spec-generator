# 貢獻指南

感謝你有興趣為 Product Spec Generator 做出貢獻！

## 📋 目錄

- [行為準則](#行為準則)
- [如何貢獻](#如何貢獻)
- [開發流程](#開發流程)
- [提交規範](#提交規範)
- [文件規範](#文件規範)

---

## 行為準則

請保持友善和尊重。我們致力於提供一個歡迎所有人的環境。

---

## 如何貢獻

### 🐛 回報 Bug

1. 先搜尋 [Issues](https://github.com/nole2466/product-spec-generator/issues) 確認是否已有相同問題
2. 如果沒有，建立新的 Issue，並使用 Bug Report 模板
3. 提供以下資訊：
   - 問題描述
   - 重現步驟
   - 預期行為
   - 實際行為
   - 環境資訊

### 💡 建議功能

1. 先搜尋 [Issues](https://github.com/nole2466/product-spec-generator/issues) 確認是否已有相同建議
2. 如果沒有，建立新的 Issue，並使用 Feature Request 模板
3. 說明：
   - 你想解決什麼問題
   - 你建議的解決方案
   - 其他替代方案

### 📝 改善文件

文件改善永遠受歡迎！包括：
- 修正錯字
- 改善說明
- 新增範例
- 翻譯

### 🔧 提交程式碼

1. Fork 這個專案
2. 建立你的分支 (`git checkout -b feature/amazing-feature`)
3. 提交你的修改 (`git commit -m 'feat: add amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 建立 Pull Request

---

## 開發流程

### 環境設置

```bash
# Clone 專案
git clone https://github.com/nole2466/product-spec-generator.git
cd product-spec-generator

# 安裝依賴（如果有）
npm install
```

### 分支命名

| 類型 | 格式 | 範例 |
|-----|------|------|
| 功能 | `feature/<name>` | `feature/add-search-template` |
| 修復 | `fix/<name>` | `fix/typo-in-readme` |
| 文件 | `docs/<name>` | `docs/add-chinese-translation` |
| 重構 | `refactor/<name>` | `refactor/simplify-templates` |

### Pull Request 流程

1. 確保你的分支是從最新的 `main` 分支建立
2. 確保所有檢查通過
3. 填寫 PR 模板
4. 等待 Review
5. 根據回饋修改
6. 合併！

---

## 提交規範

我們使用 [Conventional Commits](https://www.conventionalcommits.org/) 規範。

### 格式

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type

| Type | 說明 |
|------|------|
| `feat` | 新功能 |
| `fix` | 修復 Bug |
| `docs` | 文件變更 |
| `style` | 格式調整（不影響程式碼邏輯） |
| `refactor` | 重構（不是新功能也不是修復） |
| `test` | 新增或修改測試 |
| `chore` | 其他雜項 |

### Scope（可選）

- `templates` - 範本相關
- `agents` - 角色定義相關
- `core` - 核心原則相關
- `examples` - 範例相關
- `docs` - 文件相關

### 範例

```bash
# 新增功能
git commit -m "feat(templates): add iteration template for backlog"

# 修復 Bug
git commit -m "fix(agents): correct PM output file name"

# 更新文件
git commit -m "docs: update README quick start section"

# 重構
git commit -m "refactor(templates): simplify spec template structure"
```

---

## 文件規範

### Markdown 格式

- 使用 ATX 風格標題（`#`）
- 標題後空一行
- 列表使用 `-` 而非 `*`
- 程式碼區塊標註語言

### 範本結構

所有範本應包含：

```markdown
# 標題

> 一句話描述

---

## Metadata

| 項目 | 內容 |
|-----|------|
| ... | ... |

---

## 內容區塊

...

---

## 變更紀錄

| 日期 | 版本 | 變更內容 | 作者 |
|-----|------|---------|------|
```

### 命名規範

| 類型 | 規範 | 範例 |
|-----|------|------|
| 檔案名稱 | kebab-case | `user-login.md` |
| 目錄名稱 | kebab-case | `product-search/` |
| 範本變數 | `{描述}` | `{功能名稱}` |

---

## 🛠️ 新增 Skill

如果你想為這個專案新增一個 Skill（技能），請遵循以下步驟：

### Skill 結構

每個 Skill 都必須放在 `skills/` 目錄下，結構如下：

```
skills/
└── {skill-name}/
    └── SKILL.md
```

### SKILL.md 格式

每個 `SKILL.md` 必須包含 YAML frontmatter 和完整的技能定義：

```markdown
---
name: {skill-name}
description: {One-sentence description of what this skill does and when to use it}
argument-hint: "[command] [arguments description]"
---

# {Role Name} Role

{Skill content...}

## Commands

### {Command 1}
When user says "{trigger phrase}":
1. Step 1
2. Step 2
...

## Reference Files

- `agents/{role}.md` - Full role definition
- `templates/{template}.md` - Related templates
```

### Frontmatter 欄位

| 欄位 | 必填 | 說明 | 範例 |
|-----|:----:|------|------|
| `name` | ✅ | Skill 名稱（kebab-case） | `pm`, `backend`, `data-schema` |
| `description` | ✅ | 一句話描述功能和使用時機 | `Act as PM to produce PRD...` |
| `argument-hint` | ✅ | 提示使用者如何呼叫 | `"[generate\|review] [file]"` |

### 內容建議

一個完整的 Skill 應該包含：

1. **角色概述** - 這個角色是誰、負責什麼
2. **職責邊界** - 該做什麼、不該做什麼
3. **輸出格式** - 標準輸出範本
4. **工作流程** - 使用 Mermaid 圖表說明流程
5. **檢查清單** - 自我審核用的 Checklist
6. **TODO 追蹤格式** - 統一的追蹤格式
7. **指令說明** - 支援的指令和使用方式
8. **參考文件** - 相關的模板和文件

### 品質標準

- [ ] 使用英文撰寫（與其他 Skills 一致）
- [ ] 包含至少一個 Mermaid 流程圖
- [ ] 包含完整的 Checklist
- [ ] 包含統一的 TODO 追蹤格式（✅🔵⚪🔴）
- [ ] 內容長度至少 200 行
- [ ] 包含 Commands 區塊說明如何使用
- [ ] 包含 Reference Files 區塊

### 更新相關文件

新增 Skill 後，請同時更新：

1. **根目錄 SKILL.md** - 在角色表格中新增
2. **docs/en/README.md** - 更新英文文檔的 Skills 表格
3. **README.md** - 更新中文文檔的 Skills 表格（如有）

### 範例 PR

新增 Skill 的 PR 應包含：

```
feat(skills): add {skill-name} skill

- Add skills/{skill-name}/SKILL.md
- Update root SKILL.md with new role
- Update docs/en/README.md skills table
```

---

## 🏷️ Issue 標籤

| 標籤 | 說明 |
|-----|------|
| `bug` | Bug 回報 |
| `enhancement` | 功能建議 |
| `documentation` | 文件相關 |
| `good first issue` | 適合新手 |
| `help wanted` | 需要協助 |
| `question` | 問題討論 |

---

## 📞 聯絡方式

- GitHub Issues: 問題回報和功能建議
- GitHub Discussions: 一般討論
- Email: maintainer@example.com

---

## 🙏 感謝

感謝所有貢獻者！

<a href="https://github.com/nole2466/product-spec-generator/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=user/product-spec-generator" />
</a>

# Changelog

所有重要變更都會記錄在這個檔案中。

格式基於 [Keep a Changelog](https://keepachangelog.com/zh-TW/1.0.0/)，
版本號遵循 [Semantic Versioning](https://semver.org/lang/zh-TW/)。

## [Unreleased]

### Added
- 準備中的新功能

---

## [1.0.0] - 2024-01-28

### Added

#### 核心功能
- 新增 SKILL.md 作為 AI Agent 入口
- 新增 README.md 作為開源入口
- 新增 LICENSE (MIT)
- 新增 CONTRIBUTING.md 貢獻指南

#### 角色定義 (agents/)
- 新增 PM 角色定義 (`pm.md`)
- 新增 PD 角色定義 (`pd.md`)
- 新增 Backend 角色定義 (`backend.md`)
- 新增 Web Developer 角色定義 (`web.md`)
- 新增 App Developer 角色定義 (`app.md`)
- 新增 QA 角色定義 (`qa.md`)

#### 文件範本 (templates/)
- 新增功能地圖範本 (`_map.md`)
- 新增 PRD 範本 (`prd.md`)
- 新增 Spec 範本 (`spec.md`) - 含設計規格和介面描述
- 新增 API 契約範本 (`contract.md`)
- 新增驗收標準範本 (`acceptance.md`)
- 新增任務追蹤範本 (`TASKS.md`)
- 新增 Bug 報告範本 (`bug.md`)
- 新增 Backlog 相關範本

#### 核心定義 (core/)
- 新增核心原則 (`principles.md`)
- 新增術語表 (`glossary.md`)
- 新增審核流程 (`review-workflow.md`)
- 新增變更管理 (`change-management.md`)
- 新增 AI 人格定義 (`ai-personas.md`)

#### 參考指南 (references/)
- 新增商業邏輯規範 (`business-logic.md`)
- 新增領域知識規範 (`domain-knowledge.md`)
- 新增第三方串接規範 (`integrations.md`)
- 新增 OpenAPI 整合指南 (`openapi-integration.md`)
- 新增自動化測試指南 (`test-automation.md`)
- 新增無障礙規範 (`accessibility.md`)

#### 完整範例 (examples/)
- 新增商品搜尋功能完整範例
  - PRD 範例
  - Spec 範例（含 ASCII 介面描述）
  - API 契約範例
  - 驗收標準範例（46 個測試案例）

### Changed
- 將 design.md 整合進 spec.md
- 移除 Level 0-2，專注於企業級結構
- Frontend 拆分為 Web 和 App 兩個角色

### Removed
- 移除 `templates/minimal/` 目錄
- 移除 `scripts/` 目錄（Quick Start 腳本）
- 移除 `design.md` 獨立範本

---

## [0.1.0] - 2024-01-01

### Added
- 初始版本
- 基本角色定義
- 基本範本結構

---

## 版本說明

- **Major (X.0.0)**：不相容的 API 變更
- **Minor (0.X.0)**：向下相容的功能新增
- **Patch (0.0.X)**：向下相容的問題修正

[Unreleased]: https://github.com/nole2466/product-spec-generator/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/nole2466/product-spec-generator/compare/v0.1.0...v1.0.0
[0.1.0]: https://github.com/nole2466/product-spec-generator/releases/tag/v0.1.0

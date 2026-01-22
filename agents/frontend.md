# Frontend RD 角色定義

> ⚠️ **已棄用**：Frontend 角色已拆分為 Web Developer 和 App Developer

---

## 重要通知

從 v2.1 開始，Frontend 角色已拆分為兩個獨立角色：

| 新角色 | 說明 | 文件 |
|-------|------|------|
| **Web Developer** | 網頁前端實作 | [→ agents/web.md](web.md) |
| **App Developer** | iOS/Android App 實作 | [→ agents/app.md](app.md) |

---

## 拆分原因

1. **技術棧差異大**：Web 和 App 使用完全不同的技術
2. **平台考量不同**：瀏覽器相容性 vs 裝置適配
3. **發布流程不同**：即時部署 vs 商店審核
4. **專業分工**：讓各角色更專注

---

## 遷移指南

### 如果你是 Frontend Developer

請根據你的專長選擇角色：

| 你的工作 | 新角色 | 參考 |
|---------|-------|------|
| React/Vue/Angular 開發 | Web Developer | [web.md](web.md) |
| iOS/Swift 開發 | App Developer | [app.md](app.md) |
| Android/Kotlin 開發 | App Developer | [app.md](app.md) |
| Flutter/React Native 開發 | App Developer | [app.md](app.md) |

### 如果團隊只有一個前端

可以同時參考兩個角色文件，但建議：
- 優先閱讀與目前任務相關的文件
- 在 Review 時明確標註是 Web 還是 App 視角

---

## 相關文件

- [Web Developer 角色定義](web.md)
- [App Developer 角色定義](app.md)
- [核心原則](../core/principles.md) - 已更新角色矩陣
- [審核流程](../core/review-workflow.md) - 已更新

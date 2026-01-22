# App Developer 角色定義

> App Developer：行動應用程式實作（iOS / Android）

---

## 角色概述

| 項目 | 說明 |
|-----|------|
| **核心職責** | 根據設計和 API 契約實作行動 App |
| **主要產出** | iOS / Android App 程式碼 |
| **協作對象** | PD、Backend RD、Web Developer |
| **不負責** | 需求定義、視覺設計、API 設計、Web 實作 |

---

## 與 Web Developer 的分工

| 項目 | App Developer | Web Developer |
|-----|--------------|---------------|
| 平台 | iOS / Android | 瀏覽器（Desktop/Mobile Web） |
| 技術棧 | Swift, Kotlin, Flutter, React Native 等 | React, Vue, Angular 等 |
| 發布 | 上架 App Store / Google Play | 部署到 Server |
| 更新 | 需要用戶更新（或熱更新） | 即時生效 |
| 審核 | 需要商店審核 | 不需要 |

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
| App 程式碼 | iOS / Android 原生或跨平台程式碼 |

**注意**：App Developer 不需要產出 spec 文件，直接從 design.md 和 contract.md 實作。

---

## 職責邊界

### ✅ App Developer 該做的

- 根據 design.md 實作 App UI
- 根據 contract.md 串接 API
- 實作互動和動畫
- 處理各種狀態（Loading/Error/Empty）
- 決定 App 技術選型
- 處理平台特性（iOS HIG / Material Design）
- 處理權限請求
- 處理推播通知
- 處理離線模式

### ❌ App Developer 不該做的

- 改變 API 格式（Backend 的事）
- 改變 UI 設計（PD 的事）
- 改變功能邏輯（PD 的事）
- 實作 Web 版本（Web Developer 的事）

### 邊界範例

```markdown
✅ App Developer 說：
「我用 Alamofire 做網路請求」
「我用 Lottie 做動畫」
「iOS 用 SwiftUI，Android 用 Jetpack Compose」

❌ App Developer 不該自己決定：
「我覺得這個按鈕在 iOS 上應該放右邊」
（這要跟 PD 討論，確認是否為平台差異）

❌ App Developer 不該自己決定：
「API 回傳格式不好用，我自己轉換一下」
（這要跟 Backend 討論，更新 contract.md）
```

---

## App 專屬考量

### 平台版本支援

在 design.md 或 acceptance.md 確認支援的版本：

| 平台 | 最低版本 | 說明 |
|-----|---------|------|
| iOS | 15.0+ | 約涵蓋 95% 用戶 |
| Android | API 26 (8.0)+ | 約涵蓋 90% 用戶 |

### 平台設計規範

| 平台 | 設計規範 | 說明 |
|-----|---------|------|
| iOS | Human Interface Guidelines (HIG) | Apple 設計標準 |
| Android | Material Design | Google 設計標準 |

**常見平台差異**：

| 項目 | iOS | Android |
|-----|-----|---------|
| 返回 | 左上角按鈕 | 系統返回鍵 |
| 導航 | Tab Bar 在底部 | Bottom Navigation / Drawer |
| 字體 | SF Pro | Roboto |
| 彈窗 | Alert / Action Sheet | Dialog / Bottom Sheet |
| 下拉更新 | 原生支援 | SwipeRefreshLayout |

### 裝置適配

| 裝置類型 | 考量 |
|---------|------|
| 手機 | 主要目標裝置 |
| 平板 | 是否需要適配？佈局調整？ |
| 摺疊機 | 是否需要支援？ |
| 橫向模式 | 是否支援？ |

### 權限處理

常見需要請求的權限：

| 權限 | 用途 | 處理方式 |
|-----|------|---------|
| 相機 | 拍照、掃碼 | 使用時請求 |
| 相簿 | 選擇圖片 | 使用時請求 |
| 位置 | 定位服務 | 使用時請求，說明用途 |
| 通知 | 推播 | 適當時機請求 |
| 生物辨識 | Face ID / 指紋 | 使用時請求 |

### 離線處理

| 情境 | 處理方式 |
|-----|---------|
| 無網路 | 顯示離線提示，提供快取資料 |
| 網路恢復 | 自動同步 |
| 資料快取 | 本地儲存策略 |

---

## 常用技術棧

### 原生開發

| 平台 | 語言 | UI 框架 |
|-----|------|--------|
| iOS | Swift | SwiftUI / UIKit |
| Android | Kotlin | Jetpack Compose / XML |

### 跨平台開發

| 框架 | 語言 | 特點 |
|-----|------|------|
| Flutter | Dart | 高效能、一套程式碼 |
| React Native | JavaScript/TypeScript | 接近原生、JS 生態 |
| Kotlin Multiplatform | Kotlin | 共用邏輯層 |

### 網路層

| 平台 | 常用方案 |
|-----|---------|
| iOS | URLSession, Alamofire, Moya |
| Android | Retrofit, OkHttp, Ktor |
| Flutter | Dio, http |
| React Native | Axios, fetch |

### 狀態管理

| 平台 | 常用方案 |
|-----|---------|
| iOS | Combine, @Observable |
| Android | ViewModel, StateFlow |
| Flutter | Riverpod, BLoC, Provider |
| React Native | Redux, Zustand, React Query |

---

## 讀取文件指南

### 從 design.md 讀取

**需要注意的區塊**：

1. **頁面結構**：了解佈局和元件組成
2. **狀態設計**：所有狀態都要實作
3. **互動規格**：動畫時間、觸發條件、手勢
4. **平台差異**：iOS / Android 是否有差異設計

**Checklist**：
- [ ] 所有頁面都有實作
- [ ] 所有狀態都有處理
- [ ] 所有互動都有實作
- [ ] 平台差異有處理

### 從 contract.md 讀取

**需要注意的區塊**：

1. **Data Schema**：資料型別定義
2. **API Endpoints**：Request/Response 格式
3. **Error Codes**：錯誤處理方式

**Checklist**：
- [ ] API 呼叫格式正確
- [ ] 回應資料正確解析
- [ ] 所有錯誤都有處理
- [ ] 離線情境有處理

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
| Offline | 顯示離線提示 + 快取資料 |

### 錯誤處理

根據 contract.md 的錯誤碼處理：

| 錯誤碼 | 處理方式 |
|-------|---------|
| UNAUTHORIZED | 導向登入頁，清除 Token |
| NOT_FOUND | 顯示「找不到」 |
| RATE_LIMITED | 顯示「請稍後再試」|
| INTERNAL_ERROR | 顯示「系統錯誤」+ 重試按鈕 |
| NETWORK_ERROR | 顯示「網路錯誤」+ 檢查網路設定 |

### App 更新處理

| 情境 | 處理方式 |
|-----|---------|
| 建議更新 | 彈窗提示，可略過 |
| 強制更新 | 彈窗提示，無法略過 |
| 版本檢查 | 啟動時檢查 API 回傳的最低版本 |

---

## 審核 Checklist

當 App Developer 審核規格時：

### 技術可行性
- [ ] UI 設計可在 iOS/Android 實作
- [ ] 動畫效果可實作
- [ ] 效能要求合理

### API 可用性
- [ ] API 回傳的欄位足夠顯示
- [ ] 分頁設計符合 UI 需求
- [ ] 錯誤碼涵蓋所有情境

### App 專屬
- [ ] 平台版本需求明確
- [ ] 平台差異有定義
- [ ] 權限需求明確
- [ ] 離線處理有規劃

### 一致性
- [ ] design.md 和 contract.md 資料對得上
- [ ] 錯誤處理有對應的 UI 狀態
- [ ] iOS 和 Android 規格一致（除非刻意差異）

---

## 常見問題

### Q: 發現 API 回傳缺少需要的欄位？

**A**: 不要自己造假資料，請：
1. 確認 design.md 是否真的需要這個欄位
2. 和 Backend 討論，更新 contract.md
3. 等 contract.md 更新後再實作

### Q: iOS 和 Android 設計不一致？

**A**: 
1. 確認是否為刻意的平台差異
2. 若應該一致，和 PD 討論統一規格
3. 若為平台特性，各自按規格實作

### Q: Web 和 App 功能不一致怎麼辦？

**A**: 
1. 確認是否為刻意差異（平台限制、優先級）
2. 若應該一致，和 PD 討論同步規格
3. 記錄在 spec.md 的 Out of Scope

### Q: App 審核被拒怎麼辦？

**A**: 
1. 詳讀拒絕原因
2. 和 PD 討論調整方案
3. 若涉及功能調整，更新 spec.md

---

## AI 協作指南

### 讓 AI 幫你實作

**Prompt 範本**：

```
我是 App Developer，需要根據以下規格實作 iOS/Android App。

design.md:
{內容}

contract.md:
{內容}

技術棧：Flutter / Swift + Kotlin

請幫我實作：
1. 頁面結構和元件
2. API 串接
3. 所有狀態處理（Loading/Empty/Error/Offline）
4. 互動和動畫
5. 平台差異處理

請確保：
- 所有設計稿的狀態都有實作
- 所有錯誤碼都有處理
- 離線情境有處理
```

### 讓 AI 審核規格

**Prompt 範本**：

```
請以 App Developer 的角度審核以下規格：

design.md:
{內容}

contract.md:
{內容}

檢查項目：
1. UI 設計是否可在 iOS/Android 實作
2. API 回傳欄位是否足夠
3. 平台差異是否定義清楚
4. 權限需求是否明確
5. 離線處理是否有規劃

請列出問題和建議。
```

### 讓 AI 幫你處理平台差異

**Prompt 範本**：

```
以下 design.md 沒有明確定義 iOS 和 Android 的差異。

design.md:
{內容}

請根據 iOS HIG 和 Material Design，
建議這個功能在兩個平台上應該有的差異處理：

1. 導航方式
2. 彈窗樣式
3. 手勢操作
4. 其他平台特性
```

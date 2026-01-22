# Design Tokens

> 設計系統的基礎變數定義

---

## Metadata

| 項目 | 內容 |
|-----|------|
| 產品名稱 | {產品名稱} |
| 版本 | 1.0.0 |
| 更新日期 | {YYYY-MM-DD} |
| 負責 PD | @{username} |

---

## 1. Color 色彩

### 1.1 Brand Colors 品牌色

| Token | Value | 用途 | 預覽 |
|-------|-------|------|------|
| `color.brand.primary` | `#0066FF` | 主要品牌色、主按鈕 | 🟦 |
| `color.brand.primary.light` | `#3385FF` | 主色淺色變體 | 🟦 |
| `color.brand.primary.dark` | `#0052CC` | 主色深色變體 | 🟦 |
| `color.brand.secondary` | `#6B7280` | 次要品牌色 | ⬜ |

### 1.2 Semantic Colors 語意色

#### 文字色彩

| Token | Value | 用途 |
|-------|-------|------|
| `color.text.primary` | `#1F2937` | 主要文字 |
| `color.text.secondary` | `#6B7280` | 次要文字、說明文字 |
| `color.text.tertiary` | `#9CA3AF` | 輔助文字、Placeholder |
| `color.text.disabled` | `#D1D5DB` | 禁用狀態文字 |
| `color.text.inverse` | `#FFFFFF` | 反白文字（深色背景上） |
| `color.text.link` | `#0066FF` | 連結文字 |

#### 背景色彩

| Token | Value | 用途 |
|-------|-------|------|
| `color.bg.primary` | `#FFFFFF` | 主要背景 |
| `color.bg.secondary` | `#F9FAFB` | 次要背景、卡片 |
| `color.bg.tertiary` | `#F3F4F6` | 輔助背景、分隔區 |
| `color.bg.inverse` | `#1F2937` | 反白背景 |
| `color.bg.overlay` | `rgba(0,0,0,0.5)` | 遮罩層 |

#### 邊框色彩

| Token | Value | 用途 |
|-------|-------|------|
| `color.border.default` | `#E5E7EB` | 預設邊框 |
| `color.border.strong` | `#D1D5DB` | 強調邊框 |
| `color.border.focus` | `#0066FF` | Focus 狀態 |

#### 狀態色彩

| Token | Value | 用途 | 預覽 |
|-------|-------|------|------|
| `color.status.success` | `#10B981` | 成功 | 🟩 |
| `color.status.success.bg` | `#D1FAE5` | 成功背景 | |
| `color.status.warning` | `#F59E0B` | 警告 | 🟨 |
| `color.status.warning.bg` | `#FEF3C7` | 警告背景 | |
| `color.status.error` | `#EF4444` | 錯誤 | 🟥 |
| `color.status.error.bg` | `#FEE2E2` | 錯誤背景 | |
| `color.status.info` | `#3B82F6` | 資訊 | 🟦 |
| `color.status.info.bg` | `#DBEAFE` | 資訊背景 | |

### 1.3 Dark Mode 深色模式

| Light Token | Dark Value | 說明 |
|-------------|-----------|------|
| `color.text.primary` | `#F9FAFB` | 主要文字 |
| `color.text.secondary` | `#D1D5DB` | 次要文字 |
| `color.bg.primary` | `#111827` | 主要背景 |
| `color.bg.secondary` | `#1F2937` | 次要背景 |
| `color.border.default` | `#374151` | 預設邊框 |

---

## 2. Size 尺寸

### 2.1 Spacing 間距

基礎單位：`4px`

| Token | Value | 用途 |
|-------|-------|------|
| `size.spacing.none` | `0px` | 無間距 |
| `size.spacing.xs` | `4px` | 極小間距 |
| `size.spacing.sm` | `8px` | 小間距 |
| `size.spacing.md` | `16px` | 中間距（預設） |
| `size.spacing.lg` | `24px` | 大間距 |
| `size.spacing.xl` | `32px` | 極大間距 |
| `size.spacing.2xl` | `48px` | 超大間距 |
| `size.spacing.3xl` | `64px` | 區塊間距 |

### 2.2 Typography 文字尺寸

| Token | Font Size | Line Height | 用途 |
|-------|-----------|-------------|------|
| `size.font.xs` | `12px` | `16px` (1.33) | 標籤、註解 |
| `size.font.sm` | `14px` | `20px` (1.43) | 輔助文字 |
| `size.font.md` | `16px` | `24px` (1.5) | 內文（預設） |
| `size.font.lg` | `18px` | `28px` (1.56) | 大內文 |
| `size.font.xl` | `20px` | `28px` (1.4) | 小標題 |
| `size.font.2xl` | `24px` | `32px` (1.33) | 標題 |
| `size.font.3xl` | `30px` | `36px` (1.2) | 大標題 |
| `size.font.4xl` | `36px` | `40px` (1.11) | 超大標題 |

### 2.3 Font Weight 字重

| Token | Value | 用途 |
|-------|-------|------|
| `size.font.weight.regular` | `400` | 一般內文 |
| `size.font.weight.medium` | `500` | 強調文字 |
| `size.font.weight.semibold` | `600` | 標題 |
| `size.font.weight.bold` | `700` | 重要標題 |

### 2.4 Border Radius 圓角

| Token | Value | 用途 |
|-------|-------|------|
| `size.radius.none` | `0px` | 無圓角 |
| `size.radius.sm` | `4px` | 小圓角 |
| `size.radius.md` | `8px` | 中圓角（預設） |
| `size.radius.lg` | `12px` | 大圓角 |
| `size.radius.xl` | `16px` | 極大圓角 |
| `size.radius.full` | `9999px` | 全圓 |

### 2.5 Border Width 邊框寬度

| Token | Value | 用途 |
|-------|-------|------|
| `size.border.none` | `0px` | 無邊框 |
| `size.border.thin` | `1px` | 細邊框（預設） |
| `size.border.medium` | `2px` | 中邊框 |
| `size.border.thick` | `4px` | 粗邊框 |

### 2.6 Icon Size 圖示尺寸

| Token | Value | 用途 |
|-------|-------|------|
| `size.icon.xs` | `12px` | 極小圖示 |
| `size.icon.sm` | `16px` | 小圖示 |
| `size.icon.md` | `20px` | 中圖示（預設） |
| `size.icon.lg` | `24px` | 大圖示 |
| `size.icon.xl` | `32px` | 極大圖示 |

### 2.7 Component Size 元件尺寸

#### 按鈕高度

| Token | Value | 用途 |
|-------|-------|------|
| `size.button.sm` | `32px` | 小按鈕 |
| `size.button.md` | `40px` | 中按鈕（預設） |
| `size.button.lg` | `48px` | 大按鈕 |

#### 輸入框高度

| Token | Value | 用途 |
|-------|-------|------|
| `size.input.sm` | `32px` | 小輸入框 |
| `size.input.md` | `40px` | 中輸入框（預設） |
| `size.input.lg` | `48px` | 大輸入框 |

#### 頭像尺寸

| Token | Value | 用途 |
|-------|-------|------|
| `size.avatar.xs` | `24px` | 極小頭像 |
| `size.avatar.sm` | `32px` | 小頭像 |
| `size.avatar.md` | `40px` | 中頭像（預設） |
| `size.avatar.lg` | `56px` | 大頭像 |
| `size.avatar.xl` | `80px` | 極大頭像 |

---

## 3. 其他 Tokens

### 3.1 Shadow 陰影

| Token | Value | 用途 |
|-------|-------|------|
| `shadow.none` | `none` | 無陰影 |
| `shadow.sm` | `0 1px 2px rgba(0,0,0,0.05)` | 輕微陰影 |
| `shadow.md` | `0 4px 6px rgba(0,0,0,0.1)` | 中陰影（卡片） |
| `shadow.lg` | `0 10px 15px rgba(0,0,0,0.1)` | 大陰影（浮動） |
| `shadow.xl` | `0 20px 25px rgba(0,0,0,0.15)` | 極大陰影（Modal） |

### 3.2 Z-Index 層級

| Token | Value | 用途 |
|-------|-------|------|
| `zIndex.base` | `0` | 基礎層 |
| `zIndex.dropdown` | `100` | 下拉選單 |
| `zIndex.sticky` | `200` | 黏性元素 |
| `zIndex.fixed` | `300` | 固定元素 |
| `zIndex.modal` | `400` | Modal |
| `zIndex.toast` | `500` | Toast 通知 |
| `zIndex.tooltip` | `600` | Tooltip |

### 3.3 Transition 過渡動畫

| Token | Value | 用途 |
|-------|-------|------|
| `transition.fast` | `150ms ease` | 快速過渡 |
| `transition.normal` | `200ms ease` | 一般過渡 |
| `transition.slow` | `300ms ease` | 慢速過渡 |

### 3.4 Breakpoints 斷點

| Token | Value | 說明 |
|-------|-------|------|
| `breakpoint.sm` | `640px` | 小螢幕（手機橫向） |
| `breakpoint.md` | `768px` | 中螢幕（平板） |
| `breakpoint.lg` | `1024px` | 大螢幕（小筆電） |
| `breakpoint.xl` | `1280px` | 超大螢幕（桌面） |

---

## 4. 使用指南

### 4.1 命名規則

```
{category}.{property}.{variant}

範例：
- color.text.primary
- size.spacing.md
- size.font.lg
```

### 4.2 在程式碼中使用

**CSS Variables**
```css
:root {
  --color-brand-primary: #0066FF;
  --color-text-primary: #1F2937;
  --size-spacing-md: 16px;
  --size-font-md: 16px;
}

.button {
  background: var(--color-brand-primary);
  padding: var(--size-spacing-sm) var(--size-spacing-md);
  font-size: var(--size-font-md);
}
```

**Tailwind Config**
```javascript
module.exports = {
  theme: {
    colors: {
      brand: {
        primary: '#0066FF',
        'primary-light': '#3385FF',
        'primary-dark': '#0052CC',
      },
      text: {
        primary: '#1F2937',
        secondary: '#6B7280',
      }
    },
    spacing: {
      'xs': '4px',
      'sm': '8px',
      'md': '16px',
      'lg': '24px',
    }
  }
}
```

**React Native / StyleSheet**
```javascript
const tokens = {
  color: {
    brand: { primary: '#0066FF' },
    text: { primary: '#1F2937' }
  },
  size: {
    spacing: { sm: 8, md: 16, lg: 24 },
    font: { sm: 14, md: 16, lg: 18 }
  }
};
```

### 4.3 Spec 中的使用方式

在 `spec.md` 中引用 Token：

```markdown
#### 按鈕樣式

| 屬性 | Token | 值 |
|-----|-------|-----|
| 背景色 | `color.brand.primary` | #0066FF |
| 文字色 | `color.text.inverse` | #FFFFFF |
| 高度 | `size.button.md` | 40px |
| 圓角 | `size.radius.md` | 8px |
| 內距 | `size.spacing.sm` / `size.spacing.md` | 8px / 16px |
```

---

## 變更紀錄

| 日期 | 版本 | 變更內容 | 作者 |
|-----|------|---------|------|
| {日期} | 1.0.0 | 初版 | @{username} |

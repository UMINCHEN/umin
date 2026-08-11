# UMIN Portfolio - Design System (design.md)

單頁作品集的設計系統。像素 / 復古風、深色暖調、低飽和軍綠為唯一強調色。
此檔為修改後的設計系統紀錄，供未來編輯沿用。實作在 `style.css`，token 定義於 `:root`。

- **風格定調**：深色暖色系、極簡排版、像素 / retro
- **主題**：單一深色主題（brief 指定「深色暖色系」，不做淺色反轉）
- **動畫**：低。只有 `:hover` / `:active` 與彈窗淡入，並支援 `prefers-reduced-motion`
- **圓角**：全站直角（radius 0），像素風一致
- **字體**：Noto Sans TC（內文 / 標題）、Press Start 2P（僅大數字）

---

## 1. 色彩 Tokens

| Token | 值 | 用途 |
|---|---|---|
| `--bg` | `#16150F` | 頁面底（暖近黑，不用純黑） |
| `--surface` | `#1E1C13` | 卡片 / 面板 |
| `--surface-2` | `#2A2718` | 抬升 / hover / 次要按鈕底 |
| `--line` | `#3A3620` | 邊框 / 分隔線 |
| `--line-soft` | `#2E2B1B` | 更淡的線 / 佔位斜紋 |
| `--ink` | `#ECE6D3` | 主要文字（暖骨白） |
| `--ink-mid` | `#C4BC9E` | 次要文字 |
| `--ink-dim` | `#928A6F` | 輔助 / meta 文字 |
| `--army` | `#767C4E` | 主色，低飽和軍綠（主要按鈕填色） |
| `--army-lite` | `#B0B87A` | 深底上的強調（連結、大數字、標籤字、像素標記） |
| `--army-deep` | `#4C5130` | 按下狀態 / 硬陰影偏移色 |
| `--army-ink` | `#14150C` | 軍綠填色上的文字 |

**規則**
- 只有一個強調色（軍綠），全站一致，不在任何區塊換成別的顏色。
- 不用純黑 `#000` 或純白 `#fff`；不用漸層、不用外發光 (glow)。
- 深底上的軍綠強調一律用 `--army-lite`（對比足夠）；軍綠填色上的文字用 `--army-ink`。

## 2. 字體 Typography

- `--font-cjk: "Noto Sans TC"` - 內文、標題、按鈕；標題用 `font-weight: 900` + 負字距 `-0.01em ~ -0.02em`。
- `--font-pixel: "Press Start 2P"` - **只用在大數字 / 拉丁字**（年份、`5`、`6`、步驟 `01`、logo「UMIN」）。中文不套像素字。
- `.pixel-num` = 套用像素字的 helper；`.pixel-num--inline` = 內文中的小型像素數字（`0.82em`、軍綠）。

| 角色 | 大小 | 備註 |
|---|---|---|
| Hero H1 | `clamp(2.9rem, 8vw, 5rem)` / 900 | 「UMIN」用像素字 `0.62em` + `text-shadow` 立體塊 |
| Section title | `clamp(1.9rem, 5vw, 2.7rem)` / 900 | |
| Card title | `clamp(1.25rem, 2.6vw, 1.6rem)` / 900 | |
| Modal title | `clamp(1.7rem, 4.4vw, 2.4rem)` / 900 | |
| 內文 | `~1rem` / 1.7-1.85 | `--ink-mid` |

## 3. 間距與容器

- 內容容器 `.wrap`：`max-width: 1080px`，左右 padding 24px（手機 18px）。
- 導航高度 `--nav-h: 64px`。
- 緩動 `--ease: cubic-bezier(0.16, 1, 0.3, 1)`。

## 4. 陰影（像素硬陰影）

- `--shadow: 4px 4px 0 var(--army-deep)`（無模糊、硬邊，retro 立體感）。
- `--shadow-sm: 3px 3px 0 var(--army-deep)`。
- 互動時位移抵銷陰影，模擬實體按壓。

---

## 5. 元件 Components

### 按鈕 `.btn`（像素風）
- 直角、2px 實邊、硬陰影 `4px 4px 0`。
- `:hover` → `translate(2px,2px)` 且陰影縮小；`:active` → `translate(4px,4px)` 陰影歸零（按壓感）。
- 變體：
  - `.btn--primary`：軍綠填色 `--army` + `--army-ink` 文字（深字淺底，對比達 AA）。
  - （預設）：`--surface-2` 底 + `--ink` 文字。
  - `.btn--ghost`：透明底 + 淡邊（次要動作，如「前往 VIP 頁面」）。
  - `.btn--sm`：導航列用的小尺寸。
- `.btn-icon`：40x40 純圖示方鈕（彈窗關閉）。

### 標籤 `.tag`（像素 chip）
- 直角、2px 邊 `--line`、軍綠字 `--army-lite`、透明底。用於 hashtag 與專案技能標。

### 圖片佔位 `.ph`
- 45° 斜紋 + 虛線邊 + 四角像素直角標記 + 像素字檔名 + 中文說明。
- 變體：`.ph--portrait`(4:5)、`.ph--cover`(4:3)、`.ph--wide`(16:9)。
- 替換方式：把 `<figure class="ph ..." data-name="檔名">…</figure>` 換成 `<img src="images/檔名" alt="…">`（放進 `images/` 資料夾）。

### 導航 `.nav`
- 固定頂部、半透明 + 模糊、底線 2px。**永遠可見**（不做隨捲動隱藏，配合「減少動畫」）。
- 桌面：logo(UMIN 像素) + 關於我 / 專案 / 聯絡 + 下載履歷按鈕，單行。
- `≤720px`：漢堡選單（menu / close 像素圖示切換），展開為抽屜；點連結自動收合。

### 全螢幕彈窗 `.modal`（滿版）
- 「了解更多 / 經歷與優勢」開啟，**不跳轉頁面**。`position: fixed; inset: 0` 滿版。
- 結構：`.modal__bar`（像素 kicker + 關閉鈕）+ `.modal__scroll`（內容區，內部捲動，內容 `max-width: 760px` 置中）。
- 開啟：淡入 + 輕微上移；鎖住 body 捲動。
- 關閉：關閉鈕 / 點背景 scrim / `Esc`。
- 案例內文元件：`.case__h`（左側 4px 軍綠邊標題）、`.case__p`、`.step`（像素編號 `01-04` + 標題 + 段落）。

### 像素圖示
- 內嵌 SVG sprite（`#i-menu / i-close / i-download / i-arrow / i-mail / i-plus / i-infinity`），16 網格 + `shape-rendering: crispEdges`，`fill: currentColor` 隨字色。
- `i-infinity` = 兩個相連空心方塊，作為「無限圖騰」循環意象。

---

## 6. 版面規則

- **Hero**：非置中的左右分割（文字左、形象照右），手機收成單欄。
- **專案**：長方卡片，圖片與文字**左右交錯**（`.work-card` / `.work-card--flip`），`≤860px` 收成單欄（圖在上）。
- 全站鎖定同一主題、同一強調色、同一直角系統。

## 7. 禁用（承 taste-skill）

- 不用 em-dash `—` / en-dash `–`（用一般 `-` 或全形 `｜`）。
- 不用 AI 紫、漸層、外發光、玻璃擬態、裝飾性狀態圓點、scroll 提示、版本標籤。
- 不改任何使用者撰寫的文字內容。

## 8. 無障礙

- 文字對比達 WCAG AA；`:focus-visible` 有 2px 軍綠外框。
- 彈窗 `role="dialog" aria-modal`、可 Esc 關閉、開啟時 focus 到關閉鈕。
- 支援 `prefers-reduced-motion`（關閉所有位移 / 過場）。

# UMIN Portfolio - Design System (design.md)

單頁作品集的設計系統。像素 / 復古風。**底色深綠、主色亮橘、頁尾淺綠**。
此檔為現行設計系統紀錄，供未來編輯沿用。實作在 `style.css`，token 定義於 `:root`。

- **風格定調**：像素 / retro、極簡、色層少
- **底色 = 深綠**；**主色（唯一強調色）= 亮橘**；**頁尾 = 黑底 + 淡像素星空**（作為段落斷差）
- **色層要少、降低填充**：卡片透明（露出底色綠 + 格線），只有必要面板才填色
- **動畫**：低。只有按鈕 `:hover`/`:active` 與彈窗淡入；**區塊本身無 hover 特效**；支援 `prefers-reduced-motion`
- **圓角**：結構容器直角；按鈕與 chips 用 4px（`--radius`，唯一例外）
- **字體**：內文黑體 Noto Sans TC；**大標題用中文像素字 Zpix**；年份 / 步驟編號用 Press Start 2P

---

## 1. 色彩 Tokens

| Token | 值 | 用途 |
|---|---|---|
| `--bg` | `#0F1712` | 頁面底（深綠，不用純黑） |
| `--surface` | `#17241B` | 少數真正的面板（佔位、chips、彈窗、core） |
| `--surface-2` | `#1E2E24` | 預設按鈕填色 |
| `--line` | `#3C523F` | 邊框（綠、可見） |
| `--line-soft` | `#263A2D` | 格線 / 佔位點陣 |
| `--ink` | `#EEF3E4` | 主要文字（暖骨白） |
| `--ink-mid` | `#C3CDB4` | 次要 / 內文 |
| `--ink-dim` | `#8B9A82` | 輔助 / meta |
| `--accent` | `#FF8A3C` | **主色，亮橘**（連結、大數字、studs、chip 的 #、primary 填色） |
| `--accent-hi` | `#FFA766` | primary hover |
| `--accent-deep` | `#A6490F` | 按下 / 硬陰影 / 像素浮凸 |
| `--on-accent` | `#1A1005` | 橘色上的深色文字（primary 按鈕、年份框、步驟號） |
| `--foot-bg` | `#C9D8A6` | 頁尾淺綠底 |
| `--foot-ink` | `#1C2A1B` | 頁尾深色文字 |

**規則**
- 只有一個強調色（亮橘），全站一致。底色與結構用綠，強調 / 互動用橘。
- 不用純黑 `#000` / 純白 `#fff`；不用漸層、外發光。
- **色層要少**：底色綠 + 一個面板綠 + 骨白文字 + 橘強調 + 頁尾淺綠。卡片透明以降低填充。
- 亮橘上的文字一律用深色 `--on-accent`（白字在亮橘上對比不足，故 primary 按鈕改深字）。

## 2. 字體 Typography

- `--font-cjk: "Noto Sans TC"` - **所有內文與一般標題**（卡片標題、彈窗標題、按鈕）。標題 `font-weight: 900`。
- `--font-pixel-cjk: "Zpix"` - **用在大標題、導航列、卡片標題、彈窗標題與所有按鈕文字**（`哩賀!` / `我是 UMIN` / `感謝您的時間!` / `歡迎常來逛逛` 等）。Zpix 為向量像素字、放大不糊，含中英；透過 jsDelivr 載入（`@font-face`），失敗則 fallback 到 Noto Sans TC。
- `--font-pixel: "Press Start 2P"` - **只用在年份與步驟編號**（`2026`、`01`）。內文數字用黑體。
- 大標題加像素浮凸 `text-shadow`（hero 用 `--accent-deep` 深橘、頁尾用 `--accent` 亮橘）。

## 3. 間距與容器
- `.wrap` `max-width: 1080px`，左右 padding 24px（手機 18px）。導航高 `--nav-h: 64px`。緩動 `--ease: cubic-bezier(0.16,1,0.3,1)`。

## 4. 陰影（像素硬陰影）
- `--shadow: 4px 4px 0 rgba(6,10,7,0.65)`（半透明深色、硬邊，可用於深底與淺綠頁尾）。
- 按鈕互動時位移抵銷陰影，模擬實體按壓。

## 4.5 像素風細節（內文維持黑體）
- **角釘 `--corner-studs`**：卡片與 core 四角的 6px **淺 sage** 小方塊 `--stud #CFD6A8`（非橘；單一 `::after` + 四角漸層）。**站內不使用任何虛線**。
- **格線畫布 `body::before`**：固定 44px 淡格線，只在底色露出處顯現。
- **像素虛線 `.pixel-rule`**：專案區頂端的方塊虛線分隔。
- **像素圖示**：內嵌 SVG sprite（crispEdges）。`i-arrow` 為長「>」箭頭、`i-menu` 粗漢堡、`i-mail` 像素信封、`i-download`、`i-close`、`i-infinity`（無限圖騰）。

## 5. 元件 Components
- **按鈕 `.btn`**：**像素字體（Zpix）、無陰影**、直角 2px 邊 + 4px 圓角 + 按壓位移。`--primary`＝亮橘填色 + 深字；預設＝深綠面板 + 骨白字；`--sm`＝導航用。`.btn-icon`＝彈窗關閉方鈕。
- **chips `.tag`**：**實心無框**（`--surface-2` 填色）、4px 圓角、文字前用 CSS `::before` 加**白色 `#`**（`--ink`；HTML 不寫 #，避免重複）。
- **佔位 `.ph`**：綠面板 + 點陣 + 亮橘像素相片圖示 + 像素檔名 + 說明。變體 `--portrait`(4:5)、`--cover`、`--wide`(16:9)。替換：把 `<figure class="ph …" data-name="檔名">` 換成 `<img src="images/檔名" alt="…">`。
- **導航 `.nav`**：固定、永遠可見。桌面單行：logo + 關於我 / 專案 / 聯絡我 + 下載履歷。`≤720px` 漢堡（粗像素）；抽屜**文字置中**、點連結自動收合。
- **全螢幕彈窗 `.modal`**：滿版、不跳頁；Esc / 點背景 / 關閉鈕關閉；**內容置中對齊**；`modal__kicker` = 專案名（**不含年份**）；標題用 Zpix；`.case__h`（橘色置中）、`.step`（像素編號置中）。
- **頁尾 `.foot`**：**黑底 `#07080B` + 淡像素星空**（背景 SVG 白點）、骨白文字、`id-line` 主色橘、加大高度（約 `124–134px`）；黑底本身即「滑到下一段」的斷差。

## 6. 版面規則
- **Hero**：左右分割（文字左、形象照右）；手機單欄且**形象照 fill 滿版寬**。
- **專案**：長方卡片、圖文左右交錯（`.work-card` / `--flip`）；卡片透明只留邊框 + 角釘；年份為**內文色純文字**（Press Start 2P、無實心底）；`≤860px` 單欄。**無區塊 hover 特效**。
- 全站鎖定：同一底色綠、同一強調橘、同一直角系統。

## 7. 禁用 / 無障礙
- 不用 em-dash `—`（用 `-` 或全形 `｜`）。不改任何使用者撰寫的文字。
- 對比達 WCAG AA；`:focus-visible` 有亮橘外框；彈窗 `role="dialog"`、可 Esc；支援 `prefers-reduced-motion`。

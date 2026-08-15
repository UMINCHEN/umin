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
- `--font-pixel-cjk: "Zpix"` - **用在大標題、導航列、卡片標題、彈窗標題與所有按鈕文字**（`哩賀!` / `我是 UMIN` / `感謝您的時間!` / `歡迎常來逛逛` 等）。Zpix 為向量像素字、放大不糊，含中英；透過 jsDelivr 載入（`@font-face`），失敗則 fallback 到 Noto Sans TC。**像素標題一律明確指定字重**（避免瀏覽器對 `<h1>/<h2>/<h3>` 合成假粗體、造成相鄰兩行粗細不一，例 `哩賀!` vs `我是 UMIN`）：hero／彈窗／頁尾大標題用 `700`；**專案卡片標題用 `400`**（小字級下合成粗體會糊，故改回 400 並放大字級）；年份與 chips 維持 `400`。chips 文字也用 Zpix。hero 的 `UMIN` 為白字（非橘）。
- `--font-pixel: "Press Start 2P"` - **只用在年份與步驟編號**（`2026`、`01`）。內文數字用黑體。
- 大標題加像素浮凸 `text-shadow`（hero 用 `--accent-deep` 深橘、頁尾用 `--accent` 亮橘）。

## 3. 間距與容器
- `.wrap` `max-width: 1080px`，左右 padding 24px（手機 18px）。導航高 `--nav-h: 64px`。緩動 `--ease: cubic-bezier(0.16,1,0.3,1)`。

## 4. 陰影（像素硬陰影）
- `--shadow: 4px 4px 0 rgba(6,10,7,0.65)`（半透明深色、硬邊，可用於深底與淺綠頁尾）。
- 按鈕互動時位移抵銷陰影，模擬實體按壓。

## 4.5 像素風細節（內文維持黑體）
- **角釘 `--corner-studs`**：卡片與 core 四角的 6px 小方塊 `--stud = var(--surface-2)`（單一 `::after` + 四角漸層）。**站內不使用任何虛線**。
- **格線畫布 `body::before`**：固定 44px 淡格線，只在底色露出處顯現。
- **像素虛線 `.pixel-rule`**：專案區頂端的方塊虛線分隔。
- **像素圖示**：內嵌 SVG sprite（crispEdges）。`i-arrow` 為長「>」箭頭、`i-menu` 粗漢堡、`i-mail` 像素信封、`i-download`、`i-close`、`i-infinity`（無限圖騰）。

## 5. 元件 Components
- **按鈕 `.btn`**：**像素字體（Zpix）**、直角 2px 邊 + 4px 圓角 + **硬陰影（Windows 98 式色塊陰影，無模糊）`3px 3px 0`**，預設用 `rgba(6,10,7,.65)`、`--primary` 用 `--accent-deep`；按下時位移 3px 抵銷陰影，模擬實體按壓。`--primary`＝亮橘填色 + 深字；預設＝深綠面板 + 骨白字；`--sm`＝導航用。`.btn-icon`＝彈窗關閉方鈕（同陰影）。文字級距：一般 1rem／`--sm` 0.85rem。
- **chips `.tag`**：**透明無底色、無框**、4px 圓角、**字級與內文一致（1rem）、左右內距縮窄（6px）**，文字前用 CSS `::before` 加**白色 `#`**（`--ink`；HTML 不寫 #，避免重複）。
- **佔位 `.ph`**：綠面板 + 點陣 + 亮橘像素相片圖示 + 像素檔名 + 說明。變體 `--portrait`(4:5)、`--cover`、`--wide`(16:9)。替換：把 `<figure class="ph …" data-name="檔名">` 換成 `<img src="images/檔名" alt="…">`。
- **導航 `.nav`**：固定、永遠可見。桌面單行：logo + 關於我 / 專案 / 聯絡我 + 下載履歷。`≤720px` 漢堡（粗像素）；抽屜**文字置中**、點連結自動收合。
- **全螢幕彈窗 `.modal`**：滿版、不跳頁；Esc / 點背景 / 關閉鈕關閉；**內容區塊水平置中、文字靠左**（`.modal__scroll > *` max-width 760 + `margin:auto`）；`modal__kicker` = 完整專案名（**不含年份**）用 Zpix；標題用 Zpix；`.case__h` 左橘邊。
- **頁尾 `.foot`**：**黑底 `#07080B` + 淡像素星空**、骨白文字、**標題細體 `400`**、`id-line` 主色橘且與內文同字級（1.02rem）；**滿版高度 `min-height:100dvh`、內容垂直置中、`scroll-snap-align:start`**（搭配 `html{scroll-snap-type:y proximity}`，滑到底自動吸附）。

## 6. 版面規則
- **Hero**：左右分割（文字左、形象照右）；手機單欄且**形象照 fill 滿版寬**。文字區：問候語／標題／id-line／hashtag chips／單一 CTA（`經歷與優勢`，開彈窗）。
- **專案**：長方卡片、圖文左右交錯（`.work-card` / `--flip`）；卡片透明只留邊框 + 角釘；**標題下方即接 chips**，接著才是描述與按鈕；**年份一律緊接在標題文字後（inline，`.modal__title-year`，Zpix、`--ink-mid`、比標題小一級）**：有案例彈窗的專案，年份放在彈窗白色標題內、卡片本身不重複顯示；沒有彈窗的專案（例如純外部連結案例），年份就接在卡片標題文字後面。卡片標題放大加浮凸；**內文段落用白字 `--ink`**；`≤860px` 單欄。**無區塊 hover 特效**。
- **案例彈窗內容區塊**：每個 `case__h` 段落（背景與挑戰／我的任務／設計行動／成果與影響）都預留至少一個 `.ph--wide` 圖片佔位，供未來逐一替換成實際畫面截圖。
- 全站鎖定：同一底色綠、同一強調橘、同一直角系統。

## 7. 禁用 / 無障礙
- 不用 em-dash `—`（用 `-` 或全形 `｜`）。不改任何使用者撰寫的文字。
- 對比達 WCAG AA；`:focus-visible` 有亮橘外框；彈窗 `role="dialog"`、可 Esc；支援 `prefers-reduced-motion`。

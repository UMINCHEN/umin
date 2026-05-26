# UMIN Portfolio — Project Memory

這份文件記錄了專案的設計準則、使用者偏好與既有決策，供未來任何 Claude session 沿用。

---

## 專案基本資訊

- **用途**：UI/UX 設計師個人作品集（單頁式網站）
- **本機路徑**：`C:/Users/uuu01/Desktop/portfolio/`
- **GitHub**：https://github.com/UMINCHEN/umin
- **線上預覽**：https://uminchen.github.io/umin/ （GitHub Pages，main 分支根目錄）
- **檔案結構**：
  - `index.html` — 單一頁面，所有區段
  - `style.css` — 全部樣式
  - `IMAGE_GUIDE.md` — 圖片佔位符命名規則
  - `images/` — 圖片資料夾（user 自行放圖）

---

## 設計原則（不可違背）

### 視覺風格
- **暖色系**：背景 `#FAF4EA`（暖奶油），交替區段 `#F3E9D7`，主色 `#C45A33`（陶土橘紅）
- **淺色底**：白底或暖米色，不用深色底（除了「挑戰」區塊與最末感謝頁）
- **標題粗體**：使用 `font-weight: 900`，搭配負字距 `letter-spacing: -0.01em ~ -0.02em`
- **簡潔**：留白充足，無多餘裝飾
- **避免 AI 套版感**：不用漸層背景、不用 emoji 裝飾、不對稱版面、編輯風格的大號區段編號
- **字體**：Noto Sans TC（黑體），不用襯線字體
- **Icon**：Material Symbols Rounded **必須是 fill 版本**（`FILL=1`），不要 outline

### 內容處理
- **⚠️ 絕對不要修改任何使用者寫的文字**（即使有刪除線、特殊符號、口語化句子都保留）
- 例：`~~馬上就要~~` 刪除線要保留、`>` 大於符號要保留

---

## 既有功能與行為

### 導覽列
- **桌面版**（>720px）：顯示完整文字選單，**不顯示 01/02/03/04 編號**
- **平板以下**（≤720px）：漢堡選單，點任一連結自動關閉
- Logo `UMIN` 永遠在左

### 區段架構
1. Hero（首頁）
2. **01 背景與優勢**
3. **02 核心專案 : 安防AIOT生態系**（含挑戰、產品思維、設計系統、實務 UX 等子主題）
4. **03 其他專案**
5. **04 反思與展望**
6. 感謝頁（footer，深色底）
- **沒有 Q&A 區塊**（已移除，不要加回去）

### 「挑戰」區塊特殊樣式
- 深色底（`#2A1F18`），淺色文字
- 標題上方**不要有 icon + 小字標籤**（其他區塊有的那種 `<div class="block__label">` 結構在挑戰區要省略）

### 動畫
- 區段標題與內容滾動到畫面時 **純淡入**（opacity 0 → 1）
- **不可有方向位移**（不要 translateY、不要 translateX）
- 1 秒緩動，使用 cubic-bezier(0.22, 1, 0.36, 1)
- 不加 `prefers-reduced-motion` 限制（一定要播放）

### 容器對齊
- 所有區塊（包含 `.grid-2`、`.block--feature`、`.block--challenge`）都必須**水平置中**且**左右對齊上方 section_head**
- 不要用 `margin: 0` 否則會破壞 `.section--alt > *` 的 auto-centering
- 統一用 `margin: Xpx auto`

---

## 圖片管理

詳見 `IMAGE_GUIDE.md`。重點規則：

- **命名格式**：`{區段前綴}-{主題}-{編號}.{副檔名}`
- **前綴**：`hero-` / `intro-` / `career-` / `philosophy-` / `aiot-` / `aiot-detail-NN-` / `other-` / `reflection-`
- **佔位符**：HTML 用 `<div class="placeholder" data-name="檔名">…</div>`
- 替換真實圖片時，把該 `<div>` 換成 `<img src="images/檔名" />`
- 不存在的圖會顯示虛線佔位框，不影響其他內容

---

## 雙語/i18n 狀態

- **目前只有繁體中文**
- 使用者考慮過雙語但暫不實作（內容尚未定稿）
- 未來若實作，傾向用 `?lang=en` query parameter 方案 + JS 字典 + localStorage 記憶偏好

---

## Git 流程

- 每次有意義的修改都要 commit + push 到 `main`
- Commit message 用簡明英文，描述「為什麼」改而不是「改了什麼」
- GitHub Pages 會自動部署，約 1–2 分鐘生效
- 帳號為 `UMINCHEN`

---

## 對話風格偏好（與使用者互動）

- 使用者是 UI/UX 設計師，**不是工程師**
- 用視覺與設計語言溝通，少用艱深技術術語
- 重視美感與細節
- 修完問題後簡短報告：改了什麼、為什麼、線上連結
- 不必每次都長篇大論，**重點明確即可**

---

## 已知技術細節（避免再次踩坑）

- `.placeholder` 同時擁有 `--wide` 與 `--tall` class 時，後者會覆蓋前者的 `aspect-ratio`。**解法**：`.placeholder--tall:not(.placeholder--wide) { aspect-ratio: 4/5; }`
- `.details li` 是 grid `64px 1fr`，placeholder 必須加 `grid-column: 1 / -1` 才會跨欄
- `.section--alt > *` 的 `margin: auto` 會被子層的 `margin: Xpx 0` 覆蓋；用 `margin: Xpx auto` 才不會破壞置中
- Material Symbols 一定要載入 `FILL=1` 變數，否則圖示是 outline

# 圖片放置與命名指南

所有作品集圖片請放在 `portfolio/images/` 資料夾，並依照以下命名規則命名。
網頁會自動依檔名載入；如果檔案不存在，會顯示虛線佔位框（不影響其他內容）。

---

## 命名邏輯總覽

格式： **`{區段前綴}-{主題}-{編號}.{副檔名}`**

| 前綴 | 對應區段 | 用途 |
|------|---------|------|
| `hero-` | 首頁 Hero | 形象照、主視覺 |
| `intro-` | 區段 01 自我介紹 | 個人 / 工作環境 |
| `career-` | 區段 01 經歷 | 職涯時間軸 |
| `philosophy-` | 區段 01 理念 | 無限圖騰 |
| `aiot-` | 區段 02 安防 AIOT | 核心專案所有圖 |
| `aiot-detail-NN-` | 區段 02 展開細節 | 10 項細節對應圖 |
| `other-` | 區段 03 其他專案 | 其他案例 |
| `reflection-` | 區段 04 反思與展望 | 反思相關圖 |

副檔名建議：
- 一般照片 / 截圖 → `.jpg`
- 透明背景 / 圖示 → `.png` 或 `.svg`
- 圖騰 / icon → `.svg`

---

## 完整檔名清單（依出現順序）

### Hero 首頁
| 檔名 | 內容說明 |
|------|---------|
| `hero-portrait.jpg` | 形象照 / 工作照（直式建議 3:4） |

### 區段 01 — 背景與優勢
| 檔名 | 內容說明 |
|------|---------|
| `intro-photo.jpg` | 自我介紹用個人照或工作環境照 |
| `career-timeline.jpg` | 職涯時間軸圖（橫向） |
| `philosophy-infinity.svg` | 無限圖騰 / 循環圖示 |

### 區段 02 — 安防 AIOT 核心專案
| 檔名 | 內容說明 |
|------|---------|
| `aiot-cover.jpg` | 專案主視覺 / 產品全家福（封面，16:7） |
| `aiot-team-collab.jpg` | 團隊協作流程圖 |
| `aiot-product-thinking.jpg` | 競品分析表 / 功能架構圖 |
| `aiot-design-system.jpg` | 設計系統元件 / token 一覽 |

### 區段 02 — 實務導向 UX 展開細節（10 項）
| 檔名 | 對應細節 |
|------|---------|
| `aiot-detail-01-research.jpg` | 01 研究競品 / 功能架構 |
| `aiot-detail-02-workflow.jpg` | 02 即時工作流 / 高規格文件 |
| `aiot-detail-03-crossplatform.jpg` | 03 跨平台一致性 |
| `aiot-detail-04-naming.jpg` | 04 語意化命名 |
| `aiot-detail-05-i18n.jpg` | 05 多國語系版面 |
| `aiot-detail-06-failure.jpg` | 06 失效模式 / 斷線提示 |
| `aiot-detail-07-efficiency.jpg` | 07 設備設定簡化 |
| `aiot-detail-08-app.jpg` | 08 App 步驟拆分 |
| `aiot-detail-09-llm.jpg` | 09 LLM 預測與除錯 |
| `aiot-detail-10-workflow.jpg` | 10 跨平台工作流 |

### 區段 03 — 其他專案
| 檔名 | 內容說明 |
|------|---------|
| `other-dashboard.jpg` | 工地自組儀錶板畫面 |
| `other-gis.jpg` | GIS 圖台介面 |
| `other-nft.jpg` | NFT 研究流程 / 決策圖 |

### 區段 04 — 反思與展望
| 檔名 | 內容說明 |
|------|---------|
| `reflection-handsketch.jpg` | 手繪 UI 草稿照片 |
| `reflection-ai.jpg` | AI 應用相關示意 / 截圖 |

---

## 啟用圖片的方法

目前頁面使用「虛線佔位框」標示每張圖的位置與檔名。
要替換成真實圖片，有兩個方法：

### 方法 A（推薦）— 直接放圖檔
1. 把圖檔放進 `portfolio/images/`，並依上表命名
2. 開啟 `portfolio/index.html`
3. 找到對應的 `<div class="placeholder" data-name="檔名.jpg">…</div>`
4. 把整段 `<div class="placeholder">` 換成：
   ```html
   <img src="images/檔名.jpg" alt="說明文字" class="img" />
   ```

> 💡 每個 placeholder 區塊內都有寫上對應檔名，搜尋檔名即可快速定位。

### 方法 B — 直接搜尋取代
在 `index.html` 用編輯器搜尋功能：
- 搜尋：`data-name="aiot-cover.jpg"`
- 即可找到對應位置

---

## 尺寸建議

| 用途 | 比例 | 建議寬度 |
|------|------|---------|
| Hero 形象照 | 3:4（直） | 760 px |
| 封面圖（cover） | 16:7（寬） | 2200 px |
| 一般作品圖（wide） | 16:9 | 1600 px |
| 細節圖（detail） | 16:8 | 1600 px |
| 直式圖（tall） | 4:5 | 1200 px |
| 無限圖騰 | 5:2 | 960 px |

匯出格式建議 `.jpg`（品質 85），人物 / icon 用 `.svg` 或透明 `.png`。

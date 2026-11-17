# AGENTS.md - VolleyPlan 🏐 系隊練球菜單與戰術系統開發規範

## 1. 專案目的 (Project Purpose)
本專案為大學排球系隊專用的「VolleyPlan 練球菜單生成器與自由拖曳戰術系統」，採用行動優先（Mobile-First）設計，協助隊長快速排程訓練項目、自動計算分組人數、匯出 LINE 文本與 PNG 菜單圖卡，並持續擴充系隊自由拖曳戰術板與自訂戰術庫分頁。

## 2. 技術架構與檔案結構 (Architecture & File Structure)
本專案採用免建置（Zero-Build）純前端架構，透過 CDN 引入 Tailwind CSS、SortableJS 與 html2canvas，確保可直接部署於 GitHub Pages。
* / (專案根目錄)
  * AGENTS.md：AI 開發規範書（本文件）
  * README.md：專案說明與線上展示連結
  * index.html：主應用程式 — 練球菜單生成器（含智慧排程、菜單庫與圖卡匯出）
  * tactics.html：延伸內容頁 — 自由拖曳排球戰術板與自訂戰術庫
* **命名規則**：所有新增分頁一律放置在根目錄，使用「全小寫英文 + 連字號（kebab-case）」命名（例如：tactics.html、blocking-guide.html）。

## 3. 視覺設計系統 (Neo-Brutalism / Pop Style)
所有頁面必須在 <head> 中載入 Tailwind CDN 並維持完全一致的 tailwind.config 自訂色票與硬陰影設定：
* **核心色票**：
  * 背景奶油白 cream: #FDFBF7（bg-cream）
  * 主邊框與文字深墨藍 ink: #1E293B（border-ink、text-ink）
  * 五大功能強調色：vGreen (#4ADE80)、vYellow (#FACC15)、vOrange (#FB923C)、vBlue (#38BDF8)、vPurple (#C084FC)
* **元件造型規範**：
  * 卡片容器：bg-white border-2 border-ink rounded-2xl shadow-pop（3px 3px 0px #1E293B）。
  * 互動按鈕：必須加上 border-2 border-ink rounded-xl font-black shadow-pop-sm btn-pop，點擊時觸發 translate(2px, 2px) 按壓回饋。
  * 版面寬度：主容器統一使用 max-w-md mx-auto px-4，維持手機單手操作友善體驗。

## 4. 資料結構與核心規範 (Data Schema & Logic)
1. **訓練菜單資料庫 (DEFAULT_DRILL_DATABASE)**：
   * 儲存於 localStorage（鍵值 volleyplan_drill_db_v2）。
   * 每個訓練物件必須包含：id（字串）、category（warmup / basic / defense / attack / scrimmage / custom）、name（字串）、duration（數字分鐘）、groupType（none / pair / trio / six）、color（Tailwind 淺色背景 class）、desc（操作說明）。
2. **戰術庫資料庫 (savedTactics)**：
   * 儲存於 localStorage（鍵值 volleyplan_tactics_v1），紀錄戰術標題、備註與各球員座標百分比（x, y）。
3. **圖卡匯出相容性 (exportCardImage)**：
   * 隱藏截圖容器 #exportCardWrapper 必須維持 width: 380px 與純 HTML Table（.render-row / .render-cell）排版，禁止改用 Flexbox，以免手機版 html2canvas 截圖發生高度壓扁或文字裁切。

## 5. AI 新增頁面與擴充規則 (Rules for AI Agents)
當未來需要請 AI 協助新增「體能週期表」或「新訓練模組」時，必須嚴格遵守以下指令：
1. **建立新分頁時**：必須複製現有的 <head>（包含 tailwind.config 色票與 .btn-pop 樣式），並使用 max-w-md mx-auto 單欄卡片結構。
2. **導覽列同步**：新增分頁後，必須在 index.html 與所有分頁的 <header> 導覽按鈕區補上雙向切換連結，維持「普普貼紙按鈕」風格。
3. **擴充資料時**：僅允許在既有的 localStorage 陣列結構中依標準 Schema 擴充物件，不得更動既有的欄位名稱與儲存鍵值。

# AGENTS.md - VolleyPlan 🏐 系隊練球菜單與戰術系統開發規範

## 1. 專案目的 (Project Purpose)
本專案為大學排球系隊專用的「VolleyPlan 練球菜單生成器與戰術指南系統」，採用行動優先（Mobile-First）設計，協助隊長快速排程訓練項目、自動計算分組人數、匯出 LINE 文本與 PNG 菜單圖卡，並持續擴充系隊專項技術與輪轉戰術分頁。

## 2. 技術架構與檔案結構 (Architecture & File Structure)
本專案採用免建置（Zero-Build）純前端架構，透過 CDN 引入 Tailwind CSS、SortableJS 與 html2canvas，確保可直接部署於 GitHub Pages。
```text
/
├── AGENTS.md           # AI 開發規範書（本文件）
├── README.md           # 專案說明與軟體需求規格書 (SRS)
├── index.html          # 主應用程式：練球菜單生成器（含排程、菜單庫與圖卡匯出）
└── tactics.html        # 延伸內容頁：系隊基礎站位與輪轉戰術指南

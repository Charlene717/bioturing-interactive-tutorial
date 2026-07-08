# BioTuring — Interactive Tutorial

繁體中文 / English 雙語互動式教學，介紹 **BioTuring** 無程式碼單細胞與空間體學分析生態系。

## 中文簡介

以 GUI「按鈕背後的演算法」為主軸，帶你認識 **BBrowserX**（單細胞：匯入 → QC → 標準化/降維 → 分群/批次校正 → 註釋 → Venice 差異表達 → 軌跡/細胞通訊 → 多模態）、**SpatialX**（空間）與 **Talk2Data**（公開資料庫）。瀏覽器直接開啟 `index.html` 即可使用，無需安裝或伺服器。

## English

A bilingual (繁體中文 / English) interactive tutorial for the **BioTuring** no-code single-cell & spatial ecosystem — **BBrowserX**, **SpatialX**, and **Talk2Data** — mapping each GUI action to the algorithm behind it (Louvain, UMAP, Harmony, Venice, Monocle 2, CellChat…). Open `index.html` in any modern browser; no build step, no server.

## 內容結構 (Structure)

- `index.html` — 首頁 / hub
- `overview.html` — 生態系總覽
- `import.html` · `qc.html` · `normalization.html` · `clustering.html` · `annotation.html` · `dge.html` — BBrowserX 核心流程
- `trajectory.html` · `multimodal.html` — 進階與多模態
- `spatialx.html` · `talk2data.html` — 生態系其他平台
- `references/index.html` — 參考資料（官方頁面、演算法論文、Best Practices，附疑義注記）
- `bioturing-quiz/index.html` — 互動式考題（練習／考試模式、錯題複習、多使用者進度）
- `_research_notes/research-notes.md` — 建構本站所蒐集整理的研究資料與來源

## 注意 (Note)

本教程為教學用途，非 BioTuring 官方文件。產品命名、官方數字與 GUI 選單可能隨版本更新，請以官方文件為準（見 `references/index.html` 的疑義注記）。

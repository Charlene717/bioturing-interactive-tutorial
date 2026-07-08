# BioTuring 教程 — 研究資料整理 (Research Notes)

> 蒐集日期：2026-07-06。用於建構 BioTuring 互動式教學網站的事實依據。
> 所有產品資訊以 BioTuring 官方網站 (bioturing.com) 與同儕評論／論文為準。

---

## 1. 公司與定位 (Company)

- **BioTuring, Inc.** — 位於美國加州 San Diego（4445 Eastgate Mall, Suite 200）。
- 定位：為**沒有寫程式經驗**的科學家打造的單細胞 / 空間體學（single-cell & spatial omics）**無程式碼 (no-code) GUI 分析平台**。
- 通過 ISO/IEC 27001（資訊安全）與 ISO/IEC 27701（隱私）認證。
- 服務規模（官網宣稱）：10K+ 科學家、90+ 公司、300+ 研究機構、20 個國家。

## 2. 產品生態系 (Platform Ecosystem)

官網目前列出四大平台：

| 平台 | 定位 | 資料類型 |
|---|---|---|
| **BBrowserX** / **BBrowserX Pro** | 大規模單細胞 RNA-seq 分析平台 | scRNA-seq, snRNA-seq, TCR/BCR, ADT (CITE-seq), demultiplexing |
| **SpatialX**（前身 Lens） | 空間生物學分析平台（Windows、無程式碼） | Visium, Xenium, MERFISH/Vizgen, CosMx, GeoMx DSP, Slide-seq |
| **Talk2Data** | 公開單細胞 + 空間資料的分析中樞 / 資料庫 | 單細胞轉錄組、組織級空間轉錄組、單細胞空間轉錄組、空間蛋白體 |
| **SmartBulk** | Bulk RNA-seq 分析平台 | bulk RNA-seq |

其他工具：**BioVinci**（繪圖 / 視覺化）、**BioColab**、**Signac**（BioTuring 開發的單細胞分析套件，Venice 演算法內建其中）。

## 3. BBrowserX / BBrowserX Pro — 核心特性

- **GPU 加速**，可擴展到數百萬（Pro 版可達 **10M+**）細胞。
- **無程式碼 GUI**，適合 wet-lab 研究者；免寫 R/Python。
- 支援格式：`.h5ad`(AnnData)、**Seurat** 物件、**10x HDF5**、**MTX** bundle。
- **細胞類型自動預測**：MetaReference / 建立於 BioTuring **超過 1 億 (100M+) 單細胞** 的資料庫；可分類 **54 種細胞類型、183 種亞型**，持續新增。
- 分析功能：subclustering / reclustering、細胞類型預測、差異表達（Venice + t-test + Wilcoxon）、基因集富集 (GSEA)、軌跡分析（**Monocle 2** pseudotime）、細胞通訊（**CellChat** ligand–receptor 資料庫）。
- 多模態：CITE-seq / ADT、TCR/BCR 免疫圖譜、樣本 demultiplexing。
- 視覺化：**UMAP、t-SNE**、violin plot、heatmap、3D 視覺化、cell search（依表達模式搜尋細胞）。
- 降維／分群：PCA → UMAP / t-SNE；分群用 **Louvain**。
- 批次校正：**Harmony**（BBrowserX 主要支援之方法）。
- 標準化：以 **log transformation** 為主（相較程式碼工具選項較少）。
- Pro 版另含進階多模態與臨床模組，包括**癌細胞預測 (cancer cell prediction)**。
- 可直接上傳並分析來自 NCBI GEO 等已發表資料集。

## 4. Venice — 差異表達 / marker gene 演算法

- BioTuring 自研，用於在單細胞資料中找 marker genes / 差異表達基因。
- 動機：傳統方法（Seurat、CellRanger、EdgeR）以「平均表達值」定義 DE；但單細胞群體常是多種細胞類型/狀態的**混合**，單一參數（平均值）無法代表整個群體。
- 可辨識多種差異型態：
  - **DE** 傳統差異表達（平均不同）
  - **DP** differential proportion（各 mode 內比例不同）
  - **DM** differential modality（分佈的 modality 不同）
  - **DB** 同時 DM + DE
- benchmark：在模擬資料上對比 15 種方法有最佳 AUC。
- open-source、學術免費，內建於 BioTuring 的 **Signac** 套件。
- 論文：Nguyen et al., *Venice: A New Algorithm for Finding Marker Genes in Single-Cell Transcriptomic Data*, bioRxiv 2020. DOI: 10.1101/2020.11.16.384479

## 5. SpatialX — 空間分析平台

- 無程式碼、Windows-based；探索大規模空間資料。
- 支援平台：10x **Visium**（tissue-level）、10x **Xenium**、Vizgen **MERFISH**、NanoString **CosMx**、NanoString **GeoMx DSP**、**Slide-seq**。
- 功能：在組織結構脈絡中詮釋結果、鄰近細胞分析、細胞註釋、cell-to-cell interaction。
- 使用者證言：Stanford（CosMx/spatial）、University of Tokyo（CosMx）。

## 6. Talk2Data — 資料庫與跨研究分析中樞

- 建於 BioTuring 精選 (curated) 的大型公開資料庫。
- 規模（官網數字）：
  - **120M+** scRNA-seq 單細胞
  - **20M+** 單細胞空間轉錄組細胞
  - **100M+** 空間蛋白體細胞
  - **1800** bulk 空間轉錄組切片
  - （另一來源提及 3000+ scRNA-seq 資料集、跨物種可達 500M+ profiles，含 Human Cell Atlas、Tahoe-100M；由 NVIDIA 加速）
- 功能：單一研究分析 (single-study)、跨研究分析 (cross-study)、自訂細胞圖譜 (custom cell atlas)、跨整個資料庫的 **Gene Search**（基因表達查詢）。

## 7. 與程式碼工具 (Seurat / Scanpy) 的定位差異

- BioTuring = **GUI / no-code**，強項為速度、易用、公開資料探索、自動註釋、免寫程式。
- 程式碼工具（Seurat/Scanpy）= 彈性最高、方法選項最多、可完全客製與重現。
- BBrowserX 的限制（同儕評論指出）：normalization 僅 log、batch 僅 Harmony、部分 QC 選項較少 → 適合探索與快速分析，深度客製仍需程式碼工具。
- 教學定位：把 BioTuring 當作「把標準 scRNA-seq 流程視覺化、互動化」的入口，並對照背後演算法概念。

---

## 來源 (Sources)

- BBrowserX 平台頁：https://bioturing.com/single-cell-analysis-bbrowserx
- Talk2Data 平台頁：https://bioturing.com/single-cell-and-spatial-database-talk2data
- BioTuring 平台總覽：https://bioturing.com/platforms
- SpatialX：https://bioturing.com/spatialx
- BioTuring Lens（空間，前身）：https://bioturing.com/visualize-analyze-spatial-data-lens
- Venice 論文 (bioRxiv)：https://www.biorxiv.org/content/10.1101/2020.11.16.384479v1.full
- 工具比較（OmnibusX blog）：https://blog.omnibusx.com/comparing-tools-for-single-cell-and-spatial-transcriptomics-analysis/
- BBrowserX 更新（Single Cell Discoveries）：https://www.scdiscoveries.com/blog/updates/bioturing-single-cell-browser-update-bbrowserx/
- BioTuring 文件：https://bioturing.com/documentation

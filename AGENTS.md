# AGENTS.md — Research LLM Wiki Maintenance Guide

本檔案是本知識庫的核心運作規範與 Schema 設定檔。每當 Agent 進行文獻入庫（Ingest）、知識檢索與合成（Query）、或維護巡檢（Lint）時，均須嚴格遵照本指南執行。

---

## 1. 核心哲學與角色分工 (Core Philosophy)

本知識庫遵循 Andrej Karpathy 的 **LLM Wiki Pattern**：
- **知識是可複利積累的程式碼庫（Compounding Codebase）**：不同於每次重新檢索的 RAG，Wiki 是經過主動編譯、深度交叉引用、標註矛盾與演進脈絡的持久化知識網絡。
- **工具定位**：
  - **Obsidian**：使用者的知識探索 IDE（瀏覽 Graph View、查看雙向鏈結、使用 Dataview 篩選）。
  - **LLM Agent**：知識庫的工程師與維護者（負責高密度的摘要、萃取概念、雙向鏈結、維護跨篇綜述與健康檢查）。
  - **使用者**：首席研究員（負責文獻篩選、提問探索、方向指引與價值判斷）。
- **不可變層原則（Immutability）**：`raw/` 目錄下的文獻（PDF、原始筆記、文字稿）為真理來源，**Agent 永不直接修改 `raw/` 內的檔案**。

---

## 2. 目錄架構 (Directory Architecture)

```text
LLM Wiki Notes/
├── AGENTS.md               # [規範] 本知識庫行為守則與 Schema 定義
├── index.md                # [索引] 內容導覽目錄，依學門、主題、概念分類
├── log.md                  # [日誌] 時間軸追加日誌（Append-only）
├── raw/                    # [原始] 不可變來源
│   ├── papers/             # 存放本地 PDF 檔案
│   └── notes/              # 存放外部抓取的原始文字或使用者隨手筆記
├── papers/                 # [論文] 單篇論文核心筆記（YYYY-Author-Slug.md）
├── concepts/               # [概念] 跨領域理論、問題定義、核心假說
├── methods/                # [方法] 演算法、模型架構、實驗方法、技術實作
├── syntheses/              # [綜述] 跨論文橫向對比、演進脈絡、學術爭點矩陣
└── topics/                 # [領域] 高階學科或研究主題骨幹（如 machine-learning.md）
```

---

## 3. 語言與格式規範 (Conventions & Style)

1. **語言風格**：
   - 內文論述採用**繁體中文**進行深度解析與邏輯梳理。
   - 學術專有名詞、演算法名稱、變數、架構組件保持**英文原文**（例如：`KV Cache`, `Multi-Head Attention`, `Ablation Study`, `Perplexity`, `Gradient Clipping`），避免生硬翻譯造成學術理解斷層。
2. **數學公式**：
   - 行內公式使用 `$E = mc^2$`。
   - 獨立多行公式使用 KaTeX 區塊：
     ```latex
     $$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$
     ```
3. **Obsidian 雙向鏈結（Wikilinks）**：
   - 凡提及既有或應當建檔的概念、方法、論文，一律使用 `[[檔案名稱]]` 或 `[[檔案名稱|顯示文字]]`。
   - 檔名一律使用小寫或標準英文名稱，單詞以連字號 `-` 分隔（例：`[[transformer]]`, `[[kv-cache-optimization]]`）。

---

## 4. 頁面 Schema 與範本

### 4.1 論文頁範本 (`papers/YYYY-Author-Slug.md`)
每篇入庫論文必須包含標準 YAML Frontmatter（支援 Obsidian Dataview）：

```markdown
---
type: paper
title: "Paper Full Title"
authors: [Author One, Author Two, Author Three]
year: 2024
venue: "ArXiv / NeurIPS / Nature / etc."
arxiv: "YYMM.NNNNN"
doi: ""
primary_domain: "cs.AI"
domains: ["cs.AI", "stat.ML"]
topics: ["[[machine-learning]]"]
methods_introduced: ["[[method-name]]"]
key_concepts: ["[[concept-name]]"]
status: ingested
date_ingested: YYYY-MM-DD
---

# Paper Full Title

## 1. 核心結論與一句話精華 (TL;DR)
> 用 1-2 句話精準概括本論文的核心假說、解決的問題與最大突破。

## 2. 背景動機與痛點 (Motivation & Problem Formulation)
- **現狀與痛點**：過去研究遇到了什麼瓶頸？
- **核心假說**：本文提出了什麼前所未有的視角或假設？

## 3. 核心方法與技術架構 (Methodology)
- 架構分解、數學表述或機制解析。
- 與現有主流方法的根本本質差異（引用相關 `[[methods/...]]`）。

## 4. 關鍵實驗與成果 (Key Results & Benchmarks)
- 採用了哪些基準測試或數據集？
- 與 Baseline 的具體量化對比結果。
- 重要的消融實驗（Ablation Study）發現。

## 5. 局限性與批判性思考 (Limitations & Critiques)
- 作者承認的局限性。
- 未提及的潛在缺陷（如運算開銷過大、特定場景失效、假設過於嚴苛等）。

## 6. 知識網絡鏈結 (Network Links)
- **奠基於 (Built Upon)**：[[prior-method-or-paper]]
- **啟發/競爭者 (Competitors/Successors)**：[[competing-paper]]
- **延伸主題**：[[syntheses/relevant-synthesis-page]]
```

---

## 5. 三大核心工作流 (Core Workflows)

### 5.1 入庫作業：`/ingest`
當使用者提供 **PDF 檔名** 或 **ArXiv 連結/ID** 時執行：
1. **讀取原始來源**：
   - 若為 PDF，讀取 `raw/papers/<filename>.pdf`。
   - 若為 ArXiv 連結/ID，先擷取其標題、作者、發表年份、摘要與核心章節。
2. **對話互動（30 秒速讀摘要）**：
   - 快速向使用者回報：(a) 核心突破、(b) 實驗結論、(c) 預計更新/建立的 Wiki 頁面清單。
   - 詢問使用者是否有特定要加強分析的重點（例如模型架構細節、數學證明、實驗復現細節）。
3. **建立論文筆記**：
   - 於 `papers/` 建立 `YYYY-Author-Slug.md`，填充上述結構化內容。
4. **連鎖擴散更新（Fan-Out Updates — 最關鍵的一步）**：
   - **檢查 Concept / Method**：這篇論文是否提出了新方法？若是，在 `methods/` 建立專屬頁面；若使用了既有方法，在該頁面追加「文獻應用與驗證」紀錄。
   - **更新橫向綜述**：若有相關的 `syntheses/`（例如某個技術排行榜或對比綜述），將本篇數據與結論補充進比較表格。
   - **標記矛盾與爭點**：若本篇結果推翻或修正了既有論文的結論，在相關頁面中標註「⚠️ 爭議/對立觀點」。
5. **登記索引與日誌**：
   - 在 `index.md` 的適當分類下加入條目與一句話簡介。
   - 在 `log.md` 追加一筆紀錄：`## [YYYY-MM-DD] ingest | Title (ArXiv:ID)`。

---

### 5.2 查詢與探索：`/query`
當使用者針對知識庫提問時執行：
1. **查閱索引**：先檢索 `index.md` 與相關概念頁面，鎖定關聯的 3~5 篇論文與筆記。
2. **多文獻綜合回答**：深入讀取目標頁面，綜合給出條理清晰的解答，並精確附帶 `[[論文頁]]` 引用。
3. **回寫長青知識**：若提問引導出一個有價值的橫向對比、技術演進梳理或跨領域整合，Agent 應主動提示使用者：
   > 「這個綜述非常具備累積價值，我已將其整理並沉澱至 `syntheses/<topic-name>.md`。」
   並同步更新 `index.md`。

---

### 5.3 健康檢查：`/lint`
定期或在使用者要求時巡檢知識庫：
1. **孤島檢查（Orphan Pages）**：尋找沒有被任何其他頁面或 `index.md` 鏈結的檔案。
2. **死鏈檢查（Broken Links）**：檢查是否有 `[[...]]` 指向不存在的頁面。
3. **概念盲點（Missing Entity Pages）**：檢查哪些關鍵字在多篇論文中被反覆提及，但尚未建立專屬的 `concepts/` 或 `methods/` 頁面。
4. **爭點與過時論述（Stale Claims & Contradictions）**：檢查是否有新文獻已淘汰舊結論，但舊頁面尚未更新備註的情況。
5. **產出建議**：條列檢查報告，並在 `log.md` 追加 lint 日誌。

---

## 6. 日誌與索引維護規範

- **`index.md` 格式**：
  保持主題層級清楚。每個條目格式：
  `- [[papers/2024-author-slug|論文簡稱]] (2024, Venue) — 一句話核心貢獻或特色。`
- **`log.md` 格式**：
  保持可快速被工具解析的標準標頭：
  ```markdown
  ## [YYYY-MM-DD] ingest | Attention Is All You Need (ArXiv:1706.03762)
  - 建立了論文筆記：[[papers/2017-vaswani-attention-is-all-you-need]]
  - 建立了新方法：[[methods/transformer]], [[methods/self-attention]]
  - 更新了主題頁：[[topics/machine-learning]]
  - 更新了索引 index.md
  ```

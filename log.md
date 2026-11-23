# Research LLM Wiki Maintenance Log

本檔案為時間軸追加日誌（Append-only Chronological Log）。記錄每次 Ingest、Query 沉澱、以及 Lint 健康檢查的歷史。

---

## [2026-11-24] init | 知識庫初始化
- 建立核心規範：[[AGENTS.md]]
- 建立主索引：[[index.md]]
- 初始化日誌：[[log.md]]
- 建立核心資料夾架構：`raw/papers/`, `raw/notes/`, `papers/`, `concepts/`, `methods/`, `syntheses/`, `topics/`

## [2026-11-24] ingest | Large Language Models for Education: A Survey (ArXiv:2405.13001)
- 原始文字存檔：[[raw/notes/2024-xu-llm-for-education-survey.txt]]
- 建立論文筆記：[[papers/2024-xu-llm-for-education-survey]]
- 建立/更新概念頁：[[concepts/llmedu]], [[concepts/ai-hallucination-in-education]]
- 建立/更新方法頁：[[methods/intelligent-tutoring-system]], [[methods/prompt-engineering]]
- 建立領域骨幹頁：[[topics/smart-education]], [[topics/artificial-intelligence]]
- 沉澱橫向綜述頁：[[syntheses/llm-educational-applications-matrix]]
- 同步更新索引：[[index.md]]

## [2026-11-24] ingest | Chain-of-Thought Prompting Elicits Reasoning in Large Language Models (ArXiv:2201.11903)
- 建立論文筆記：[[papers/2022-wei-chain-of-thought]]
- 建立核心方法頁：[[methods/chain-of-thought]]
- 更新提示詞方法頁：[[methods/prompt-engineering]]
- 同步更新索引：[[index.md]]

## [2026-11-24] ingest | Let's Verify Step by Step (ArXiv:2305.20050)
- 建立論文筆記：[[papers/2023-lightman-lets-verify-step-by-step]]
- 建立核心方法頁：[[methods/process-supervision]]
- 更新概念頁：[[concepts/ai-hallucination-in-education]]
- 同步更新索引：[[index.md]]

## [2026-11-24] ingest | Toolformer: Language Models Can Teach Themselves to Use Tools (ArXiv:2302.04761)
- 建立論文筆記：[[papers/2023-schick-toolformer]]
- 建立核心方法頁：[[methods/toolformer]]
- 更新智慧導師系統方法頁：[[methods/intelligent-tutoring-system]]
- 建立推理演進橫向綜述：[[syntheses/reasoning-enhancement-pathway]]
- 更新教育應用綜述矩陣：[[syntheses/llm-educational-applications-matrix]]
- 同步更新索引：[[index.md]]

## [2026-11-24] query / export | 產生投影片簡報《LLM 在教學上的運用問題與核心挑戰》
- 產出檔案：[[slides/llm-in-education-challenges.html]]
- 涵蓋文獻：[[papers/2024-xu-llm-for-education-survey]], [[papers/2023-lightman-lets-verify-step-by-step]], [[papers/2023-schick-toolformer]], [[papers/2022-wei-chain-of-thought]]
- 同步更新索引：[[index.md]]

## [2026-11-24] query / export | 產生現代日系圖文型深度講義《大語言模型在教育中的運用問題與突破路徑》
- 產出檔案：[[handouts/llm-in-education-handout.html]]
- 特色：純原生網頁技術、零外部環境依賴、整合 8 張靜態圖表、內建目錄吸頂導航、支援一鍵列印/存為 PDF
- 同步更新索引：[[index.md]]

## [2026-11-24] query / export | 產生 Prezi 風格大畫布平移縮放圖譜簡報《LLM 在教學上的運用問題（無限畫布演講版）》
- 產出檔案：[[slides/llm-education-graph-presentation.html]]
- 特色：純原生網頁技術、零環境依賴、3600x2600 像素大畫布、10 個空間攝影機平滑平移視角、SVG 動態光流連線、點擊任意節點平滑飛行聚焦
- 同步更新索引：[[index.md]]

# Research LLM Wiki Index

本頁面為知識庫的全域內容索引（Content-Oriented Catalog）。由 Agent 在每次執行文獻入庫（Ingest）或建立綜述（Synthesis）時自動同步維護。

---

## 📚 論文目錄 (Papers by Domain & Year)

### Computer Science / AI & NLP (`cs.CL`, `cs.AI`, `stat.ML`)
- [[papers/2024-xu-llm-for-education-survey|Xu et al. (2024)]] (ArXiv:2405.13001) — 大語言模型賦能智慧教育（LLMEdu）的系統性綜述，涵蓋三大融合模式、十大教育影響與長程推理衰減等挑戰。
- [[papers/2023-lightman-lets-verify-step-by-step|Lightman et al. (2023)]] (OpenAI / ArXiv:2305.20050) — 提出過程監督（Process Supervision）與 PRM800K 數據集，以步驟級反饋擊潰結果監督（ORM），大幅提升數理長程推論正確率。
- [[papers/2023-schick-toolformer|Schick et al. (2023)]] (Meta AI / NeurIPS 2023 / ArXiv:2302.04761) — 提出 Toolformer，展示語言模型可透過自監督損失差值自主學習調用計算機、檢索器等外部 API。
- [[papers/2022-wei-chain-of-thought|Wei et al. (2022)]] (Google Research / NeurIPS 2022 / ArXiv:2201.11903) — 思維鏈提示（Chain-of-Thought, CoT）開山之作，開創在提示中引導中間步驟以激發大模型湧現推理能力的範式。

---

## 🔬 核心方法與演算法 (Methods & Architectures)
- [[methods/chain-of-thought|Chain-of-Thought (CoT)]] — 思維鏈提示：將單次預測因子化為中間自然語言推導步驟，激發複雜推理湧現。
- [[methods/process-supervision|Process Supervision (PRM)]] — 過程監督：對推導過程的每個步驟獨立提供獎勵與診斷，消除「歪打正著」謬誤。
- [[methods/toolformer|Toolformer / Tool-Augmented LMs]] — 自監督工具調用：讓語言模型自主決定調用計算機、搜尋等外部工具的解耦計算架構。
- [[methods/intelligent-tutoring-system|Intelligent Tutoring System (ITS)]] — 智慧導師系統：從傳統專家規則邁向基於 LLM 的啟發式自適應輔導架構。
- [[methods/prompt-engineering|Prompt Engineering]] — 提示詞工程：在教育情境下的防爆雷引導、思維鏈激發與角色模擬指令設計。

---

## 💡 理論與問題定義 (Concepts & Problems)
- [[concepts/llmedu|LLMEdu]] — 大語言模型教育：融合大模型技術重構即時反饋與個人化學習的理論體系。
- [[concepts/ai-hallucination-in-education|AI Hallucination in Education]] — 教育場景中的 AI 幻覺危害、多步推理崩潰與緩解策略。

---

## 📊 橫向綜述與技術對比 (Syntheses & Surveys)
- [[syntheses/reasoning-enhancement-pathway|Reasoning Enhancement Pathway]] — 大模型推理與數理能力突破三部曲：從思維鏈 (CoT) 到過程監督 (PRM) 再到工具調用 (Toolformer) 的演進對比與教育賦能整合。
- [[syntheses/llm-educational-applications-matrix|LLM Educational Applications Matrix]] — 生成式 AI 在教育五大核心場景（個性化、引導、跨學科、即時答疑、數學）的優劣勢與挑戰對比矩陣。

---

## 🖥️ 專題簡報與成果產出 (Presentations & Artifacts)
- [[slides/llm-education-graph-presentation.html|LLM 在教學上的運用問題（無限畫布圖譜演講版）]] — Prezi 風格大畫布平移縮放簡報：日系輕透微光畫布，支援 10 個視角平滑飛行、卡片高亮聚焦、SVG 能量光流與全景鳥瞰切換。
- [[handouts/llm-in-education-handout.html|大語言模型在教育中的運用問題與突破路徑（圖文型深度講義）]] — 現代日系編輯風格深度圖文講義：整合八大視覺圖表、四大問題向度、二十步斷崖實證與 CoT+PRM+Tool 三角解法，支援一鍵列印儲存為 PDF。
- [[slides/llm-in-education-challenges.html|LLM 在教學上的運用問題與核心挑戰（卡片翻頁版）]] — 互動式簡報投影片：現代日系透明感風格，深入剖析機器幻覺、二十步推理斷崖、認知外包與人本治理。

---

## 🌐 研究領域與學門 (Topics & Disciplines)
- [[topics/smart-education|Smart Education]] — 智慧教育領域骨幹。
- [[topics/artificial-intelligence|Artificial Intelligence]] — 人工智慧全域骨幹。

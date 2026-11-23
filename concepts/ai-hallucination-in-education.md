# AI Hallucination in Education (教育中的 AI 幻覺)

## 1. 概念定義 (Definition)
**AI 幻覺（Machine Hallucination）** 在教育場景中特指大語言模型生成看似權威、語法通順，但實際上事實錯誤、邏輯矛盾或捏造文獻的「一本正經胡說八道（Serious Nonsense）」現象。

---

## 2. 教育環境下的特殊危害 (Pedagogical Risks)
相較於通用問答，教育領域對「正確性」具備極致要求：
1. **認知弱勢學生的誤導**：處於基礎學習階段的學生缺乏完整的批判思維與領域知識儲備，容易無條件採信 AI 給出的偽知識。
2. **多語言偏差與不平衡**：多數開源與商業模型以英文語料為大宗，在針對非英語文化、本地歷史或本土語言教材進行個人化解題時，幻覺發生率顯著攀升。
3. **長程嚴密推導的骨牌效應**：在物理、化學、數學等序列推導中，初期的一個微小幻覺會導致後續所有結論完全失真。

---

## 3. 防範與緩解機制 (Mitigation Strategies)
- **檢索增強生成 (Retrieval-Augmented Generation, RAG)**：將 LLM 錨定於經權威審核的校本教材與教科書知識庫。
- **過程監督 (Process-Supervision)**：採用 [[methods/process-supervision]] 機制（如 [[papers/2023-lightman-lets-verify-step-by-step]]），不只對最終答案給出獎勵，而是對逐步推理過程進行單步核驗，截斷邏輯謬誤鏈。
- **外接符號引擎與計算器**：如整合 [[Toolformer]] 架構或形式化系統（[[Lean 4]]），將純計算與定理驗證交由確定性引擎執行。
- **反向教學運用**：教育工作者可刻意利用「AI 幻覺」作為教材，設計「尋找 AI 錯誤」的探究式任務，反向培養學生的批判性思維與資訊素養（Information Literacy）。

---

## 4. 關聯文獻 (Literature)
- [[2024-xu-llm-for-education-survey]]：指出學生認知能力限制與過度信任是偽知識氾濫的主因，提倡 RAG 與人機協同教學治理。

---
type: paper
title: "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models"
authors: [Jason Wei, Xuezhi Wang, Dale Schuurmans, Maarten Bosma, Fei Xia, Ed Chi, Quoc V. Le, Denny Zhou]
year: 2022
venue: "NeurIPS 2022"
arxiv: "2201.11903"
doi: ""
primary_domain: "cs.CL"
domains: ["cs.CL", "cs.AI"]
topics: ["[[artificial-intelligence]]", "[[smart-education]]"]
methods_introduced: ["[[chain-of-thought]]"]
key_concepts: ["[[emergent-abilities]]", "[[multi-step-reasoning]]"]
status: ingested
date_ingested: 2026-11-24
---

# Chain-of-Thought Prompting Elicits Reasoning in Large Language Models

## 1. 核心結論與一句話精華 (TL;DR)
> 本文提出「思維鏈提示（Chain-of-Thought Prompting, CoT）」，透過在 Few-shot 示範中加入中間自然語言推理步驟，使大語言模型能夠將複雜問題分解為循序漸進的推導過程，顯著提升模型在算術推理、常識推論與符號操作上的解題正確率。

---

## 2. 背景動機與痛點 (Motivation & Problem Formulation)
- **現狀與痛點**：
  - 傳統標準提示（Standard Prompting / Input-Output Prompting）直接要求模型輸出最終答案，模型在處理需要多步驟推導的複雜問題（如多步驟數學應用題、邏輯推理）時表現極為低落。
  - 單純擴增模型參數規模（Scaling）無法自然克服「跳躍式推理」所帶來的邏輯斷裂與高錯誤率。
- **核心假說**：
  - 人類在解決多步驟問題時會撰寫「草稿」或心中默想中間步驟；若以自然語言思維鏈（CoT）引導模型在生成最終答案前先產生中間推導軌跡，即可為後續 Token 的生成提供強大的條件機率依據與計算緩衝空間。

---

## 3. 核心方法與技術架構 (Methodology)
- **CoT 提示機制**：
  - 在 Few-shot Exemplars 中，為每個示範題目提供由三元組組成的結構：$\langle \text{Input}, \text{Chain of Thought}, \text{Output} \rangle$。
  - 中間的思維鏈（Chain of Thought）以人類可讀的自然語言文字描述分解步驟，無需任何微調（Fine-tuning）或修改神經網絡權重。
- **湧現能力 (Emergent Ability)**：
  - 實驗觀察發現：CoT 的效益並非線性增長，而是具備湧現特徵。當模型規模小於特定閥值（例如參數小於約 100B）時，CoT 往往無法帶來收益甚至略微降低表現；唯有模型規模達到足夠大（如 PaLM 540B、GPT-3 175B）時，CoT 才會激發強烈的推理躍升。

---

## 4. 關鍵實驗與成果 (Key Results & Benchmarks)
- **GSM8K 數學基準**：
  - 在 GSM8K 8-grade 數學應用題測試集上，PaLM 540B 搭配 CoT 取得突破性的 56.9% 正確率，大幅超越標準 Few-shot（17.9%），並優於當時許多專門經過微調的監督模型。
- **常識推理與符號操作**：
  - 在 SVAMP、ASDiv、AQuA、StrategyQA 以及 Last Letter Concatenation 等符號與常識基準上，CoT 均呈現顯著的性能優勢，證明其泛化能力不僅限於數值計算。

---

## 5. 局限性與批判性思考 (Limitations & Critiques)
- **幻覺累積效應 (Cascading Errors)**：
  - 若推理鏈中某一中間步驟產生事實性或計算性錯誤（如加減法失誤），後續所有推理步驟將基於錯誤前提展開，導致最終結論錯誤（關聯 [[concepts/ai-hallucination-in-education]]）。
- **計算推論延遲與成本增加**：
  - 生成多行中間推理文字顯著增加了解碼的 Token 數量，導致推論時間延長與 API 呼叫成本上升。
- **缺乏自省與驗證機制**：
  - 標準 CoT 屬於純貪婪式或取樣式的單向前向生成，模型無法在發現錯誤時回溯（Backtrack），此瓶頸後續促成了自我修正與樹狀推理架構（如 Tree of Thoughts）以及過程監督機制的發展。

---

## 6. 知識網絡鏈結 (Network Links)
- **奠基於**：Few-shot In-Context Learning, [[methods/prompt-engineering]]
- **被引用/應用於**：[[papers/2024-xu-llm-for-education-survey]]（引為改善 ITS 與學生多步數理推理的核心基礎技術）
- **後續改進與競爭者**：[[methods/process-supervision]]（對 CoT 每一步進行即時獎勵核驗）、[[methods/toolformer]]（將符號計算步驟委派給計算器）

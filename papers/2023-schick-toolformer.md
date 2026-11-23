---
type: paper
title: "Toolformer: Language Models Can Teach Themselves to Use Tools"
authors: [Timo Schick, Jane Dwivedi-Yu, Roberto Dessì, Roberta Raileanu, Maria Lomeli, Luke Zettlemoyer, Nicola Cancedda, Thomas Scialom]
year: 2023
venue: "NeurIPS 2023"
arxiv: "2302.04761"
doi: ""
primary_domain: "cs.CL"
domains: ["cs.CL", "cs.AI"]
topics: ["[[artificial-intelligence]]", "[[smart-education]]"]
methods_introduced: ["[[toolformer]]", "[[tool-augmented-lms]]"]
key_concepts: ["[[self-supervised-api-calling]]", "[[grounding]]"]
status: ingested
date_ingested: 2026-11-24
---

# Toolformer: Language Models Can Teach Themselves to Use Tools

## 1. 核心結論與一句話精華 (TL;DR)
> Meta AI 團隊提出 Toolformer，展示大語言模型無需依賴大量人工標註，即可透過自監督方式自主學習何時、調用何種外部工具（如計算機、搜尋引擎、維基百科檢索、問答系統與翻譯引擎），並將工具回傳結果無縫整合進文本生成中，徹底解決模型在數值運算與即時事實性上的根本瓶頸。

---

## 2. 背景動機與痛點 (Motivation & Problem Formulation)
- **現狀與痛點**：
  - 純神經網絡語言模型本質上是基於統計關聯的預測器，在兩類任務上表現極度孱弱：
    1. **精確數值計算**：對於大數運算、浮點數運算容易出錯（算力無法勝過幾塊錢的電子計算機）。
    2. **最新事實與時效性資訊**：模型權重凍結於預訓練截止點，對最新事件或長尾事實容易產生幻覺。
  - 先前工具調用方法高度依賴人工撰寫提示（如 ReAct）或大量專門標註的對話數據，擴展性低且通用性差。
- **核心假說**：
  - 語言模型可利用自身的 In-Context Learning 能力自我生成潛在的 API 調用候選，再透過過濾與自我監督訓練，自發學會「在最能降低預測損失（Loss）的地方」插入 API 呼叫。

---

## 3. 核心方法與技術架構 (Methodology)
- **自監督 API 採樣與過濾演算法 (Self-supervised Annotation)**：
  1. **候選採樣 (Sampling)**：給定普通無標註文本，利用 Few-shot Prompt 引導模型在文本任意位置插入候選 API 呼叫：`[API_Name(parameters)]`。
  2. **執行與獲取結果 (Execution)**：真實呼叫對應外部工具，獲得回傳結果 $r$，並組裝為完整帶有結果的文字標記串。
  3. **損失過濾 (Loss Filtering)**：關鍵機制——比對模型在「有工具結果 $r$」與「沒有工具結果」兩種情況下預測後續 Token 的 Cross-Entropy Loss。**唯有當工具回傳結果能顯著降低後續文本預測的困惑度（Perplexity）時**，該 API 調用才會被保留為正樣本數據。
  4. **微調蒸餾 (Fine-tuning)**：將過濾後的優質數據用於微調原始模型（基於 GPT-J 6.7B），使模型內化工具調用決策能力。
- **整合的五大核心工具集**：
  - 計算機 (Calculator)
  - 維基百科檢索器 (Wikipedia Search)
  - 機器翻譯系統 (Machine Translation)
  - 外部問答系統 (QA System)
  - 行事曆/時間查詢 (Calendar)

---

## 4. 關鍵實驗與成果 (Key Results & Benchmarks)
- **運算與常識基準測試**：
  - 僅具備 6.7B 參數的 Toolformer 在數學推理（SVAMP, ASDiv, MAWPS）、時效性知識問答與多語言檢索上，全面擊敗了參數規模大其 25 倍以上的 GPT-3 (175B)。
- **自主調用精準度**：
  - 模型在推論過程中展現高度克制，只在遭遇複雜算術或長尾實體時自主發起 API 呼叫，而在一般自然語言對話時保持原生流暢度，未損害基礎語言生成能力。

---

## 5. 局限性與批判性思考 (Limitations & Critiques)
- **工具鏈單步限制 (No Tool Chaining)**：
  - 原生 Toolformer 無法連續或遞迴串聯多個工具（例如：先搜尋維基百科取得數字，再將數字傳給計算機運算），各 API 調用彼此獨立。
- **缺乏多輪互動與反思**：
  - 工具調用是一次性（Single-pass）的，若外部 API 報錯或回傳無效資訊，模型缺乏動態重試或修改搜尋關鍵詞的閉環機制。

---

## 6. 知識網絡鏈結 (Network Links)
- **奠基於**：自監督學習 (Self-Supervised Learning), In-Context Learning
- **被引用/應用於**：[[papers/2024-xu-llm-for-education-survey]]（引為教育輔助系統突破數值計算與事實幻覺的關鍵利器）
- **互補技術**：[[methods/chain-of-thought]]（思維鏈提供思考路徑，Toolformer 提供具體執行工具）、[[methods/intelligent-tutoring-system]]

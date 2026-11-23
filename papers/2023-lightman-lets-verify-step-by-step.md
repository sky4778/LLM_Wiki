---
type: paper
title: "Let's Verify Step by Step"
authors: [Hunter Lightman, Vineet Kosaraju, Yura Burda, Harri Edwards, Bowen Baker, Teddy Lee, Jan Leike, John Schulman, Ilya Sutskever, Karl Cobbe]
year: 2023
venue: "ArXiv / OpenAI Research"
arxiv: "2305.20050"
doi: ""
primary_domain: "cs.AI"
domains: ["cs.AI", "cs.LG", "stat.ML"]
topics: ["[[artificial-intelligence]]", "[[smart-education]]"]
methods_introduced: ["[[process-supervision]]", "[[prm800k]]"]
key_concepts: ["[[outcome-vs-process-supervision]]", "[[ai-hallucination-in-education]]"]
status: ingested
date_ingested: 2026-11-24
---

# Let's Verify Step by Step

## 1. 核心結論與一句話精華 (TL;DR)
> OpenAI 團隊證明：在複雜多步數學推理中，針對每個解題步驟提供單步獎勵的「過程監督（Process Supervision, PRM）」顯著優於僅針對最終答案給予獎勵的「結果監督（Outcome Supervision, ORM）」，在 MATH 基準測試集上取得了 SOTA 水準的 78.2% 解題率，且顯著提升了模型對非邏輯捷徑的抵抗力與對齊安全性。

---

## 2. 背景動機與痛點 (Motivation & Problem Formulation)
- **現狀與痛點**：
  - 傳統強化學習從人類反饋中學習（RLHF）通常採用**結果監督獎勵模型 (Outcome-supervised Reward Model, ORM)**，即根據模型最終答案是否正確給予正負獎勵。
  - 在高難度數理邏輯任務中，ORM 面臨致命缺陷：**「歪打正著 (False Positive / Right for the wrong reasons)」**。模型可能在中間推導中產生嚴重邏輯幻覺或計算錯誤，卻碰巧得到正確的最終數值；ORM 會錯誤地強化這種有缺陷的推理過程，導致模型在更長程、更複雜問題上崩潰。
- **核心假說**：
  - 若人類評註者針對模型生成的 [[methods/chain-of-thought]] 進行「每一步驟（Step-by-step）」的正確性標註，並訓練一個「過程監督獎勵模型 (Process-supervised Reward Model, PRM)」，將能更精準地指導模型在每一步維持邏輯嚴密，大幅降低幻覺。

---

## 3. 核心方法與技術架構 (Methodology)
- **PRM vs. ORM 架構設計**：
  - **ORM**：輸入整個問題與完整解答，輸出單一純量值評估解答整體正確性。
  - **PRM**：在每個步驟結尾插入特殊標記（Step Delimiter），預測該步驟為「正面（Positive, 正確且有進展）」、「中立（Neutral, 贅述或無效進展）」或「負面（Negative, 出現計算或邏輯錯誤）」的機率分佈。
- **PRM800K 數據集**：
  - 發布了包含 80 萬個由人類專家細緻標註的數學解題步驟數據集（涵蓋 MATH 資料集題目的解題推導過程），是目前規模最大的過程監督公開基準。
- **Best-of-N 搜索採樣**：
  - 於推論時（Inference-time），利用生成模型產生 $N$ 條獨立的解題候選路徑，再由 PRM 為每一路徑的步驟進行評分（通常取路徑中各步驟最小或乘積機率），選取評分最高的路徑作為最終輸出。

---

## 4. 關鍵實驗與成果 (Key Results & Benchmarks)
- **MATH 測試集性能**：
  - 在極具挑戰性的高中數學奧林匹克等級測試集 MATH 上，基於 GPT-4 的 PRM 在 Best-of-N 採樣下達到 **78.2%** 的解題準確率，顯著壓倒同等算力與數據量下的 ORM。
- **非分布樣本泛化 (OOD Generalization)**：
  - 隨採樣數量 $N$ 擴增，PRM 展現更強的 Scaling 效益，且在更複雜的長程多步推導中保持高穩定性，未出現 ORM 常見的「為了迎合最終結果而偽造過程」現象。

---

## 5. 局限性與批判性思考 (Limitations & Critiques)
- **人工標註成本高昂**：
  - 過程監督需要領域專家逐步審視長篇數學推導，標註 80 萬個步驟耗費極大人力與經濟成本，難以快速平移至所有垂直學科。
- **信用卡分配問題 (Credit Assignment)**：
  - 對於具備高度創造性的開放式證明題，一個看似「不合常理」的中間步驟究竟是靈光乍現的捷徑還是邏輯謬誤，人類審閱者自身亦可能產生判斷分歧。

---

## 6. 知識網絡鏈結 (Network Links)
- **奠基於**：[[methods/chain-of-thought]], RLHF / Reward Modeling
- **解決的核心概念**：[[concepts/ai-hallucination-in-education]]（消除教育解題中的偽邏輯）、[[concepts/llmedu]]
- **被引用/呼應於**：[[papers/2024-xu-llm-for-education-survey]]（指引了突破數理教育邏輯推理瓶頸的關鍵路徑）

# Chain-of-Thought (思維鏈, CoT)

## 1. 方法概觀 (Overview)
**思維鏈（Chain-of-Thought, CoT）** 是一種透過在輸入提示中引導大語言模型顯式生成「中間推理步驟」的提示技術（[[methods/prompt-engineering]]）。該方法由 [[papers/2022-wei-chain-of-thought]] 於 2022 年形式化提出，已成為大語言模型執行複雜多步推理的事實標準。

---

## 2. 機制原理 (Mechanism)
傳統預測直接計算目標答案的條件機率：
$$P(\text{Answer} \mid \text{Question})$$

CoT 將該過程因子化為一系列中間推導步驟 $S = (s_1, s_2, \dots, s_k)$：
$$P(\text{Answer}, S \mid \text{Question}) = \prod_{i=1}^k P(s_i \mid \text{Question}, s_{<i}) \cdot P(\text{Answer} \mid \text{Question}, S)$$

透過引導模型逐一輸出 $s_i$，模型在預測後續 Token 時能將注意力分配給先前生成的推導文字，實質上將單一複雜的黑盒映射轉換為多階段動態自適應計算。

---

## 3. 在智慧教育（LLMEdu）中的核心價值
1. **教學思維透明化**：學生透過閱讀中間步驟，能觀察專家級的解題路徑，而非僅獲得冷冰冰的最終數值。
2. **多步推理強化**：有效緩解教育論文 [[papers/2024-xu-llm-for-education-survey]] 中指出的「20 步推理斷崖」，將複雜問題解構為可管理之微單元。
3. **診斷易讀性**：教師與系統能輕易檢視學生在哪一個中間步驟 $s_i$ 產生概念混淆，進而實施精準介入。

---

## 4. 關鍵關聯文獻 (Literature)
- [[papers/2022-wei-chain-of-thought]]：奠基論文，首次展示大模型在數學與符號推理上的 CoT 湧現效應。
- [[papers/2024-xu-llm-for-education-survey]]：評估 CoT 在智慧導師與教育應用中的落實現狀。

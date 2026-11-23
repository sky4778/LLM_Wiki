# Prompt Engineering (提示詞工程)

## 1. 定義與核心價值 (Definition)
**Prompt Engineering** 係指設計、優化與調校輸入給大型語言模型的自然語言指令（Prompts），以最大化激發模型在特定下游任務中的推理品質、事實性與風格適配度。

---

## 2. 在教育領域（LLMEdu）的特殊演變
在通用場景下，Prompt 多旨在追求「快速、準確給出最終成果」；但在教育情境下，Prompt 具備全然不同的設計哲學：
1. **防爆雷原則 (No-Spoilers Instruction)**：嚴格限制模型直接貼出解答，強制其採用啟發式提問引導學生探索。
2. **思維鏈激發 (Chain-of-Thought, CoT)**：引入 [[methods/chain-of-thought]] 範式，引導模型「Step-by-Step」展示推理過程，協助學生觀察解題思維路徑並顯著提升數理推論準確度。
3. **角色扮演機制 (Persona Simulation)**：讓模型扮演特定歷史人物、科學家或同儕學習伴侶，增加情境沉浸感。
4. **難度與語言梯度調控**：根據學習者年齡（如小學生 vs 大學生）動態調節輸出的詞彙艱澀度與句法結構。

---

## 3. 關聯文獻 (Literature)
- [[2024-xu-llm-for-education-survey]]：指出優良的提示詞設計是克服教育場景「胡言亂語（Nonsense）」的關鍵橋樑，並探討了不同教育模型（如 ChatGPT, ERNIE Bot, MathGPT）底層對 Prompt 的敏感性差異。

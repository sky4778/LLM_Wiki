# Toolformer (自監督工具調用大模型)

## 1. 方法概觀 (Overview)
**Toolformer** 是由 Meta AI 於 2023 年提出的神經網絡工具調用架構（[[papers/2023-schick-toolformer]]）。其開創了語言模型**無需人工標註**即可自發學會何時呼叫外部工具（如計算機、搜尋引擎、翻譯器）的自監督範式。

---

## 2. 核心技術原則：損失差值篩選 (Loss Discrepancy Filtering)
Toolformer 的自我進化核心在於判別式篩選準則：
令上下文為 $x$，候選 API 呼叫為 $c$，工具回傳結果為 $r$，後續目標序列為 $y$。
僅當：
$$L(y \mid x, c, r) < \min(L(y \mid x), L(y \mid x, c)) - \tau$$
（其中 $\tau$ 為預設閥值）時，該 API 調用才會被收錄進微調訓練集。這確保模型僅在工具能帶來**實質預測增益**時才調用工具。

---

## 3. 在智慧教育（LLMEdu）的落地意義
在 [[methods/intelligent-tutoring-system]] 與智慧解題場景中，Toolformer 模式提供了最經濟的架構解方：
- **徹底杜絕純計算幻覺**：大模型不再死記浮點運算，遇算式直接交由 Calculator 處理。
- **輕量化端側部署可行性**：如論文實測，6.7B 模型結合 Toolformer 即可在數理計算上壓倒 175B 的大模型，大幅降低教育硬體設備的部署門檻。

---

## 4. 關鍵關聯文獻 (Literature)
- [[papers/2023-schick-toolformer]]：原創論文。
- [[papers/2024-xu-llm-for-education-survey]]：評析工具交互對提升教育模型計算與邏輯嚴密性的賦能價值。

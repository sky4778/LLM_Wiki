# Process Supervision (過程監督 / 步驟級獎勵模型)

## 1. 方法概觀 (Overview)
**過程監督（Process Supervision）** 是一種在訓練或評估大語言模型推理能力時，不只看最終答案是否正確，而是對推導過程中的「每一個中間步驟（Step-by-step）」給予獨立反饋與獎勵信號的對齊與引導機制。該方法由 OpenAI 的 [[papers/2023-lightman-lets-verify-step-by-step]] 正式奠立學術標竿。

---

## 2. 過程監督 (PRM) vs. 結果監督 (ORM)
| 比較維度 | 結果監督 (Outcome Supervision, ORM) | 過程監督 (Process Supervision, PRM) |
| :--- | :--- | :--- |
| **反饋粒度** | 整篇答案結尾給予單一數值 | 每個解題步驟（Step）即時打分 |
| **容錯機制** | 易被「歪打正著（Right for wrong reasons）」欺騙 | 能精確定位初次發生謬誤的關鍵步驟 |
| **解碼搜尋增益** | 僅能評估完整軌跡，搜尋剪枝能力弱 | 支援步驟級蒙地卡羅樹搜尋（MCTS）或早停剪枝 |
| **標註成本** | 低（僅需比對最終答案符號） | 高（需專家逐步標註推導正確性） |

---

## 3. 在教育領域（LLMEdu）的關鍵意涵
在 [[concepts/llmedu]] 與 [[methods/intelligent-tutoring-system]] 中，過程監督能實現真正的「診斷式教學」：
- **細粒度學情診斷**：系統不再只向學生回報「算錯了」，而是能精確指出「你在第 3 步進行因式分解時正負號弄錯了」。
- **抑制幻覺滲透**：有效截斷中途出錯但結論巧合正確的有害示範，避免在數理教育中傳遞偽科學邏輯（關聯 [[concepts/ai-hallucination-in-education]]）。

---

## 4. 關鍵文獻 (Key References)
- [[papers/2023-lightman-lets-verify-step-by-step]]：提出 PRM800K 基準，證明 PRM 於 MATH 題目上大幅超越 ORM。
- [[papers/2024-xu-llm-for-education-survey]]：指明過程監督是賦能教育大模型精準數學推導的核心突破點。

# Intelligent Tutoring System (智慧導師系統, ITS)

## 1. 方法概觀 (Overview)
**智慧導師系統（ITS）** 是致力於為每位學生模擬「一對一人類專家導師」行為的軟體架構。在生成式 AI 時代，ITS 由傳統的專家規則庫與貝氏知識追蹤（BKT），全面演進為以大語言模型（LLM）為核心的自適應對話系統。

---

## 2. LLM-based ITS 核心架構組件
1. **學生狀態感知模組 (Student Profiler)**：分析學習者的作答歷史、錯誤模式與提問風格。
2. **蘇格拉底式引導引擎 (Socratic Dialogue Engine)**：透過特定 Prompt 策略（[[prompt-engineering]]），避免直接提供答案，而是以反問引發學生主動建構知識。
3. **外部驗證與計算介面 (External Tool API)**：針對數理邏輯與多步驟問題，整合 [[methods/toolformer]] 概念自我調用計算引擎，或引入 [[methods/process-supervision]] 進行步驟級核驗與早停剪枝。
4. **評估與反饋生成器 (Personalized Assessment)**：即時分析作文結構、文法錯誤或代碼缺陷。

---

## 3. 代表性商業與學術實踐
- **Khanmigo (Khan Academy & OpenAI)**：以引導式提問為核心的個人化 AI 導師。
- **MathGPT (好未來 TAL)**：針對數學解題特化的教育模型，強調結合解題計算引擎。
- **Spark Desk 學習機 (iFLYTEK 科大訊飛)**：整合中英文作文批改與口語對練。

---

## 4. 關鍵文獻 (Key References)
- [[2024-xu-llm-for-education-survey]]：回顧了從傳統電腦輔助教學（CAI）到 LLM-based ITS 的歷程，並對比了各家主流教育產品。

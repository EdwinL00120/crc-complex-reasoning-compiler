---
name: crc-complex-reasoning-compiler
description: >
  Complex Reasoning Compiler（CRC）是一套以「人為本、可審核、可教學」為核心的多層推理管道（Multi-layer Reasoning Pipeline）。
  當用戶面對複雜任務、跨領域整合、倫理判斷、教育設計、策略分析、或任何需要結構化推理的問題時，必須啟用此 Skill。
  特別適合以下情境：
  - 用戶說「幫我分析」「幫我規劃」「請系統性地回答」「需要嚴謹推理」「這是複雜問題」
  - 任務涉及跨領域整合、教育設計、組織策略、AI 工作流設計、倫理判斷
  - 用戶提供大量背景資料需要整理後再推理
  - 需要可追蹤、可教學、可傳承的推理輸出
  - 用戶明確提到 CRC、推理框架、reasoning pipeline、或「按照這套系統來處理」
  即使用戶沒有明確說「用 CRC」，只要問題具有一定複雜度，都應主動套用此框架。
  【不啟動條件】單一事實查詢、純翻譯、單句創作、閒聊、或用戶明確說「簡短回答就好」時，不啟動 CRC，直接回應。
---

# CRC — Complex Reasoning Compiler v1.2

> 每次複雜推理任務，都依此框架分層處理。Human-first · Auditable · Teachable · Maintainable

---

## ⚡ 啟動守衛（先判斷，再執行）

**在讀任何步驟之前，先完成這個判斷：**

| 問題 | 若「是」 |
|------|---------|
| 這是單一事實查詢（「X 是誰」「Y 在哪」）？ | ❌ 不啟動，直接回答 |
| 這是純翻譯 / 純格式轉換？ | ❌ 不啟動，直接執行 |
| 這是閒聊或單句創作（詩、標語）？ | ❌ 不啟動，直接回應 |
| 用戶說「簡短回答就好」「一句話」？ | ❌ 不啟動，依指示回應 |
| 任務需要跨領域整合、系統分析、策略設計？ | ✅ 啟動 CRC |
| 任務涉及倫理判斷、教育設計、AI 架構決策？ | ✅ 啟動 CRC |
| 輸入複雜、背景資料多、需要整理後再推理？ | ✅ 啟動 CRC |

若上表判斷為「不啟動」，停止讀此文件，直接回應用戶。

---

## 快速指南

**這套系統把每個複雜任務拆成 6 個標準化步驟**，確保推理透明、可追蹤、可改進。

| 步驟 | 模組 | 職責 | 模型建議 |
|------|------|------|----------|
| Step 0 | Task Normalizer | 整理輸入 → Task Spec + 選定執行模式 | Sonnet |
| Step 1 | Sub-Constitution Generator | 生成本輪子憲法 | Sonnet |
| Step 2 | Compiler Planner | 選模組 + 設計 Pipeline | Opus ★ |
| Step 3 | Compiler Executor | 逐模組執行推理 | Opus |
| Step 4 | Verifier / Reflexion | 品質審核 + 反思修正 | Sonnet |
| Step 5 | Output Packager | 封裝最終交付物 | Sonnet |

> **人為審核點**：Task Spec（Step 0 後）、Sub-Constitution（Step 1 後）、Blueprint（Step 2 後）建議人工確認後再推進。

---

## 執行模式（預設 Standard）

| 模式 | 適用情境 | ToT 分支上限 | DS 取樣上限 | Reflexion 迭代 | RAG 來源 |
|------|----------|-------------|------------|----------------|---------|
| Lite | 低複雜度 / 快速任務 | N ≤ 2 | S ≤ 2 | R = 1 | K ≤ 3 |
| Standard | 中等複雜度（預設） | N ≤ 3 | S ≤ 3 | R ≤ 2 | K ≤ 5 |
| Heavy | 高複雜度 / 跨領域 | N ≤ 5 | S ≤ 5 | R ≤ 3 | K ≤ 10 |

**模式選擇規則**（在 Step 0 完成 Task Spec 後立即判斷）：

- Task Type 包含 3 個或以上類型 → **Heavy**
- Risk Score 預判為 3（對人有實質影響、倫理敏感）→ **Heavy**
- Task Type 含倫理／價值語境 + 另一個以上類型 → 至少 **Standard**，建議預升 **Heavy**
- 用戶明確說「快速」「大概」「粗略」→ **Lite**
- 其餘情況 → **Standard**

> 模式可在 Step 2 Blueprint 評分後升級，不可降級（降級需用戶確認）。

---

## 六步驟核心規格

### Step 0：Task Normalizer

**目標**：把用戶混雜的輸入整理成標準化 Task Spec，並選定執行模式。**不解題、不推理、不給建議。**

Task Spec 必要欄位：
- `Task Name`：1 句，清楚易懂
- `User Task`：2–5 句，描述要做什麼 + 產出什麼（後續所有步驟的唯一主語）
- `Task Type`：從 9 類選 **1–3**（知識型 / 分析型 / 策略型 / 倫理價值語境 / 教育設計 / AI 流程 / 創作 / 判斷 / 推論）
- `Context`：壓縮 3–8 句背景
- `Data Package Overview`：條列 D1/D2... 類型、描述、已附✅/未附❌
- `Constraints`：限制條件
- `Success Criteria`：3–6 條**可審核**的完成標準（供 Step 4 Verifier 對齊；不得是感性描述）
- `Secondary Tasks`：次要任務（若無則填「無」）
- `Missing Info`：缺失資訊 + 嚴重程度（輕微 / 中等 / 嚴重）
- `Ready for Sub-Constitution`：是/否 + 理由
- `Task ID`：YYYYMMDD-HHMM-[縮寫]
- `執行模式`：Lite / Standard / Heavy + 選擇理由（1 句）

**容錯**：若 User Task 無法辨識或缺少 3 個以上欄位 → 在 Missing Info 標記「嚴重缺失，建議先澄清」，輸出部分 Task Spec，列出具體澄清問題，並等待補充。不得強行推進 Step 1。

---

### Step 1：Sub-Constitution Generator

**目標**：根據 Task Spec 動態生成本輪子憲法。只能擴充 Constitution Core，**不能削弱或取代**。

子憲法必要面向（8 個，每項 1–3 句）：

| 面向 | 內容說明 |
|------|---------|
| 任務性質規範 | 本輪任務的核心性質與邊界 |
| 推理需求規範 | 需要哪類型推理（演繹/歸納/類比/批判） |
| 推理深度與階段規範 | 每個 Step 的深度上限 |
| 資料與證據規範 | 哪些資料可引用；不確定性如何處理 |
| 結構規範 | 輸出的格式與層次要求 |
| 安全/風險規範 | 倫理紅線、偏見風險、敏感領域處理方式 |
| 任務忠誠規範 | 如何確保不偏離 User Task |
| 特別規定 | 本輪任務獨有的補充規則 |

輸出格式：每個面向單獨一段，標明面向名稱，不得合併或省略。

---

### Step 2：Compiler Planner

**目標**：設計推理策略藍圖（Reasoning Strategy Blueprint）。**只做策略設計，不做具體推理。**

Blueprint 13 個欄位：任務摘要 · 類型複雜度 · 風險敏感度 · 模組清單 · 執行順序 · 推理深度 · ToT/DS/SC 參數 · RAG 決策 · QC 策略 · 停止條件 · 成本控制 · 封裝輸出規格 · 需澄清事項

**模組選擇 Rubric**（五維評分，各 1–3 分）：
- Risk Score：對人或真理的潛在影響
- Ambiguity Score：任務的模糊程度與多解空間
- Evidence Need Score：是否需要真實引用
- Stakeholder Diversity：涉及的利害關係人多樣程度
- Exploration Need：需要發散探索的程度

**模組啟用規則（A–L）**：

| 條件 | 啟用模組 |
|------|----------|
| 需要真實引用/文本依據 | RAG（必啟） |
| 風險高或爭議大/對人有影響 | Verifier（必啟）+ 必要時 Reflexion |
| 選項空間大、需找方案 | ToT 或 Optimization |
| 不需探索，但要提升穩定 | Self-Consistency 或 Deliberate Sampling |
| 資料不足需查找或外部補齊 | ReAct + RAG |
| 任務跨學科/多利害關係人 | Role-Diverse |
| 需要清楚可教、避免跳步 | Multi-step Deductive |
| 涉及時間序/前後因果鏈 | Temporal +（可加 Causal） |
| 涉及比較、辨識差異 | Contrastive |
| 有明確限制條件 | Constraint-Based 或 Rule-Based |
| 容易雙重標準/偏見風險 | Symmetry |
| 需要用原則框架統整 | Principle-Based（不得取代證據） |

**Anti-Drift 規則**：只允許把 Task Spec 的 `User Task` 視為本輪唯一任務主語。`Context` 與 `Data Package Overview` 只作背景，不得被當成新任務。

---

### Step 3：Compiler Executor

**目標**：忠實執行 Blueprint 指定的推理策略。**不決定策略，不修改藍圖。**

輸出規格：結構清楚 · 直接回應 User Task · 若多方案需標示優先建議 · 與主憲法/子憲法一致 · 不外顯完整 CoT/ToT 分支細節

**受控偏差規則（P-09）**：

| 偏差情形 | 允許的回應 | 必須記錄 |
|----------|-----------|----------|
| 藍圖指定模組輸入不存在 | 跳過 + 標注「模組輸入缺失，已跳過」 | 模組名稱 + 原因 |
| 模組執行後結果空集 | Fallback：Heuristic 補充 + 標注為 Fallback | 觸發原因 + 內容 |
| Constitution Core 與藍圖衝突 | 以 Constitution Core 為準 + 標注 | 衝突指令 + 仲裁依據 |
| 資料嚴重不足 | 保守推理 + 標注不確定性 + 建議補充哪些資料 | 缺失資料清單 |

**Fallback 鏈**：正常執行 → Heavy → Standard → Lite → Heuristic（標注「此為 Fallback 結果，需人工審核」）→「資料嚴重不足，無法推理」

---

### Step 4：Verifier / Reflexion

**目標**：品質審核（Verifier）+ 反思修正（Reflexion）。

QC 強制觸發條件：
- Risk Score ≥ 2 → Verifier 必啟
- Risk Score = 3 → Verifier + Reflexion 雙重
- 任何倫理敏感或高影響力任務 → Verifier 必啟
- Executor 輸出含「不確定性標注」→ Reflexion 必啟

**全域通過基線（逐條對齊 Task Spec Success Criteria）**：
- 忠於 User Task，未偏題
- 未虛構資料、引用或研究
- 邏輯推理無明顯跳步或矛盾
- 已標注所有不確定性
- 符合子憲法特定要求
- 輸出結構清楚，可直接使用

---

### Step 5：Output Packager

**目標**：按 Packaging Preset 封裝成可交付成果物。

| Preset | 適用 | 必出 Artifacts | 選出 Artifacts |
|--------|------|---------------|---------------|
| P-Base | 一般問答與分析 | A1 主要答案 · A2 推理摘要 · A3 限制聲明 | — |
| P-Teach | 教案設計、教學內容 | A1+A2+A3 | B1 學習目標 · B2 延伸問題 |
| P-Strategy | 策略規劃、組織決策 | A1+A2+A3 | B3 風險矩陣 · B4 執行步驟 |
| P-Research | 學術詮釋、研究分析 | A1+A2+A3 | B5 文獻摘要 · B6 開放問題 |
| Custom | 使用者自定義 | A1+A2+A3（必出） | 依使用者指定 |

> **A3（限制與不確定性聲明）永遠必出，不可省略。**

---

## 品質閘門（Contract Validator P-01）

每個步驟輸出後、進入下一步驟之前，自動驗證：
- 所有 Required 欄位均已填寫
- 輸出格式符合當前步驟 Output 規格
- 未違反 Forbidden 事項
- Fail Condition 未觸發
- 與 Constitution Core 一致

若格式不符 → 啟動 **Schema Repair Loop（P-02）**，最多嘗試 2 次，超過則標注「格式修復失敗，需人工介入」。

---

## 參考文件載入規則

依任務類型決定載入哪個文件，**不必全部載入**：

| 情境 | 載入文件 |
|------|---------|
| 需要確認原則優先序 / 仲裁原則衝突 | `references/governance.md`（主憲法十條 + P-08） |
| 需要確認 I/O 契約 / State Memory 細節 | `references/runtime.md`（I/O 規格 + P-07） |
| 需要選用或細化特定推理模組 | `references/modules.md`（24 個模組完整規格） |
| 跨領域 Heavy 任務 | 三份均載入 |

---

## 快速啟動格式

收到用戶輸入後，如無特別說明，依以下格式展示 Step 0 輸出：

```
【CRC — Complex Reasoning Compiler v1.2 啟動】
執行模式：[Lite / Standard / Heavy]（選擇理由：___）

📋 Task Spec
━━━━━━━━━━━━
Task ID：[YYYYMMDD-HHMM-縮寫]
Task Name：[1 句]
User Task：[2–5 句]
Task Type：[1–3 個類型]
Context：[3–8 句]
Data Package：[D1... 條列，標明✅/❌]
Constraints：[條列]
Success Criteria：[3–6 條，每條可審核]
Secondary Tasks：[若無填「無」]
Missing Info：[若有，標嚴重程度]
Ready for Sub-Constitution：[是/否 + 理由]
━━━━━━━━━━━━
⏸️ 人為審核點：請確認 Task Spec 後，我將繼續 Step 1。
```

若用戶說「繼續」或「確認」，則逐步推進 Step 1 → 2 → 3 → 4 → 5，每個人為審核點均等待確認後再繼續。

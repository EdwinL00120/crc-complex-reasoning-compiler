# CRC — Complex Reasoning Compiler

> **Reasoning you can audit. Process you can teach. AI you can trust.**

*Built by a non-engineer. Designed for anyone who needs to trust their AI.*
*非工程師建的框架。為所有需要信任 AI 的人而設計。*

---

> **For those who feel AI outputs are untrustworthy, unteachable, or unaccountable.**
> **為那些感覺 AI 輸出不可信、無法教學、無從問責的人而設計。**

---

## 這是為誰設計的 / Who This Is For

你是否曾經有這樣的感覺：

- AI 給了一個「好答案」，但你不知道它怎麼想到的
- 同樣的 prompt，下次跑出不同結果，原因不明
- 你想把 AI 工作流交給別人用，但完全無法教學
- 面對複雜任務，AI 跳過了你認為最重要的那一步

**CRC 是為這些問題而建的。**

---

You may have felt this way before:

- AI gave a "good answer" but you have no idea how it got there
- The same prompt produces different results next time, for no clear reason
- You want to hand off your AI workflow to someone else, but it's impossible to teach
- For complex tasks, AI skips the step you consider most important

**CRC was built for exactly these problems.**

---

## 為什麼需要 CRC / Why CRC Exists

大多數 AI 框架追求的是**輸出品質**。

CRC 追求的是**推理過程的品質**。

這個差異看起來微小，實際上決定了：
- 你能不能審核 AI 的推理
- 你能不能把流程教給別人
- 你能不能在出錯時找到原因

> 一個黑盒子給你好答案，和一個透明系統給你可驗證的答案——
> 在日常任務裡分別不大，但在複雜決策裡，差距是巨大的。

---

Most AI frameworks optimize for **output quality**.

CRC optimizes for **reasoning process quality**.

This distinction determines:
- Whether you can audit AI's reasoning
- Whether you can teach the process to others
- Whether you can trace the source of errors

> A black box that gives good answers vs. a transparent system that gives verifiable answers —
> the difference is small for simple tasks, but enormous for complex decisions.

---

## 核心設計哲學 / Core Design Philosophy

### 1. Human-First（人為本）
AI 執行，人類決定。
系統內建三個**強制人為審核點**，不跳過，不自動推進。

AI executes, humans decide.
Three **mandatory human review checkpoints** are built into the system — non-skippable, non-automatic.

### 2. Auditable（可審核）
每個推理步驟有明確的輸入、輸出與規格。
錯了，找得到是哪一步錯。

Every reasoning step has explicit inputs, outputs, and specifications.
When something goes wrong, you can trace exactly where.

### 3. Teachable（可教學）
設計不是只給自己用。
任何人拿到這份文件，應該能理解並延伸——不是只能複製貼上。

Not designed for personal use only.
Anyone reading this document should be able to understand and extend it — not just copy-paste.

---

## 系統架構 / System Architecture

```
Step 0  Task Normalizer        整理輸入，生成標準化任務規格
Step 1  Sub-Constitution       動態生成本輪推理子憲法
Step 2  Compiler Planner       設計推理策略藍圖（只設計，不執行）
Step 3  Compiler Executor      忠實執行藍圖指定的推理策略
Step 4  Verifier / Reflexion   品質審核 + 反思修正
Step 5  Output Packager        封裝成可交付、可使用的成果物
```

**⏸️ 人為審核點 Human Review Points：Step 0 → Step 1 → Step 2 之後各暫停一次**

三種執行模式 / Three Execution Modes：
- `Lite` — 低複雜度快速任務
- `Standard` — 中等複雜度（預設）
- `Heavy` — 高複雜度跨領域任務

---

## 快速開始 / Getting Started

CRC 設計為 **Claude Skill** 格式，可直接在 Claude.ai 的 Projects 功能中載入。

CRC is designed as a **Claude Skill**, loadable directly into Claude.ai Projects.

1. 複製 `SKILL.md` 內容 / Copy the contents of `SKILL.md`
2. 在 Claude Project 的 Instructions 貼上 / Paste into Claude Project Instructions
3. 開始一個複雜任務，輸入你的問題 / Start a complex task and input your question
4. 系統會自動判斷是否啟動 CRC / The system will automatically determine whether to activate CRC

---

## 關於設計者 / About the Designer

我不是工程師。我靠 AI 工具自學，從零建構這套系統。

幾年前，我帶著一個早期項目在香港會展的公開比賽中亮相——
團隊幾乎是即時獲得一個新加坡基金的認同，並在其支持下推進。
那個項目我後來選擇離開，但那次經歷讓我確信：
**一個人不需要是技術專家，也能建出值得認真對待的東西。**

CRC 是我在思考「AI 工作流應該長什麼樣」這個問題時，慢慢沉澱出來的答案。
它不完美，但它是真實的。

---

I'm not an engineer. I built this system from scratch using AI tools, through self-directed learning.

A few years ago, I brought an early-stage project to a public competition at the Hong Kong Convention Centre —
our team received near-immediate recognition from a Singapore fund, which supported the project's development.
I eventually stepped away from that project by choice, but the experience confirmed something for me:
**You don't need to be a technical expert to build something worth taking seriously.**

CRC is the answer I slowly arrived at while thinking about what AI workflows should actually look like.
It's not perfect. But it's real.

---

## 交流與討論 / Discussion

這個系統是開放的，設計哲學也是開放的。

如果你：
- 有同樣的困惑，想聊聊
- 在自己的場景裡試用過，有觀察想分享
- 認為某個設計決定是錯的，想挑戰

**歡迎在 GitHub Discussions 留言。** 我認真看每一條。

---

This system is open. So is the design philosophy behind it.

If you:
- Share the same frustrations and want to talk
- Have tried it in your own context and have observations to share
- Think a design decision is wrong and want to challenge it

**Leave a comment in GitHub Discussions.** I read every one.

---

## License

MIT — 用吧，改吧，只是別說是你原創的。請標註出處，讓更多人找得到這裡。

MIT — Use it, modify it. Just don't claim you made it from scratch. Attribution appreciated.

---

## 版本日誌 / Changelog

| 版本 | 日期 | 主要變動 |
|------|------|---------|
| v1.2 | 2026-04 | 首次公開發布 / Initial public release |

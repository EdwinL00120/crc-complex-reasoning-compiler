# Example: CRC vs Non-CRC Output Comparison

> This example shows the difference between a CRC (Complex Reasoning Compiler) response
> and a standard AI response to the same question.
> Question type: Root cause analysis of system complexity

---

## Original Question

> "Why is this system so complex?"

---

## Side-by-Side Comparison

### 1️⃣ Question Framing

| | CRC | Non-CRC |
|---|---|---|
| **Question answered** | "Why is it complex?" → traces root causes | "Is this design good?" → evaluates design quality |
| **Task fidelity** | Strictly aligned to the original question | Drifts into a design review |

**Diagnosis**: The Non-CRC response is effectively saying "this design is good." This is a classic case of **question substitution** — replacing the original question with one that's easier to answer.

---

### 2️⃣ Root Cause vs Design Quality Score

**CRC's core framework:**

```
Essential Complexity vs Accidental Complexity
```

This binary has genuine explanatory power — it directly answers "why is it complex."

**Non-CRC's framework:**

```
🟢🟡 Scoring table
```

This framework answers "is the design good," not "why is it complex."
These are **entirely different epistemological directions**.

---

### 3️⃣ Reasoning Depth

CRC did something Non-CRC did not:

> **It identified the compounding mechanism of complexity.**
> The four complexity types are not a parallel list — they are mutually irreducible.

- Non-CRC produced a **checklist** (this is good, watch out for that)
- CRC produced a **causal explanation** (why these complexity types necessarily coexist)

---

### 4️⃣ Actionability

| | CRC | Non-CRC |
|---|---|---|
| **Action direction** | "The only leverage point is the Accidental cache-sync layer" | "Four possible touch points (refresh copy, sort UX, etc.)" |
| **Basis for action** | Derived from complexity type classification | Repackaged from the document's own to-do list |

**Diagnosis**: Non-CRC's four extension points simply repackaged the original document's closing section. **No new reasoning was generated.**

---

## Summary

| Dimension | CRC | Non-CRC |
|-----------|-----|---------|
| Task fidelity | ✅ Strictly on-question | ❌ Question quietly substituted |
| Framework fit | ✅ Matched to question type | ❌ Framework mismatch |
| Reasoning depth | ✅ Causal explanation | ⚠️ List enumeration |
| Actionability | ✅ Grounded in new reasoning | ❌ Repackaged from source |

> CRC's value is not that it produces longer or more polished output.
> It's that **it actually answers the question you asked**.

---

*Generated with CRC v1.2. [← Back to README](../README.md)*

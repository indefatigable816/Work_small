---
title: Prompt for data analyzation
updated: 2026-02-08T10:36:25
created: 2026-02-08T10:33:10
---

AM

**Role:** Agentic AI for AlphaFold3 multimer confidence analysis (non-Jupyter, script-based)
**Execution Constraint:**
- **Do NOT use Jupyter notebooks**
- Use **plain Python scripts** or agent-native execution only
- Seaborn is allowed for plotting, but no interactive notebook outputs

**Task**
Analyze **JSON files only** under:
Data/results/AF3/multimer/
Include **only** files matching:
fold\*summary_confidences\*.json
These represent **4 result categories**, with WT reused as control:
- (HER2 Δ16 + Trastuzumab) vs (HER2 WT + Trastuzumab)
- (HER2 S310F + Pertuzumab) vs (HER2 WT + Pertuzumab)

**Analysis Focus**
- Primary metric: **drug–target iPTM, interface mean pLDDT**
- Validity filter: **pTM \> 0.5**
- Grouping:
  - **Experimental:** Δ16, S310F
  - **Control:** WT

**Analysis Objectives**
1.  Recursively scan AF3/multimer/ for matching JSON files.
2.  Parse summary_confidences to extract:
    - iPTM
    - pTM
    - fold / model identifier
3.  Filter out invalid predictions (**pTM ≤ 0.5**).
4.  Aggregate iPTM by:
    - Drug
    - Variant (WT vs Mutant)
5.  Compute:
    - Mean / median iPTM
    - N (valid models)
    - ΔiPTM (Mutant − WT)

**Output Requirements**
**1. Summary Table (file or stdout)**
Generate a **single consolidated table** with:
- Drug
- Variant
- Group (Control / Experimental)
- Mean iPTM
- Median iPTM
- N (pTM \> 0.5)
- ΔiPTM vs WT
**2. Visualization (seaborn, script-generated)**
- Use **seaborn only** for plotting
- Output **static figures** (e.g., PNG/PDF)
- Boxplot or violin plot of iPTM
- One plot per hypothesis
- Clear WT vs Mutant labeling

**Hypothesis Framework (must be referenced explicitly)**
| **Objective** | **Experimental Group** | **Control Group** | **Expected Outcome (iPTM)** | **Mechanistic Rationale** |
|----|----|----|----|----|
| Trastuzumab binding | HER2 Δ16 + Trastuzumab | HER2 WT + Trastuzumab | Low iPTM (Δ16) | Δ16 enforces covalent homodimers, distorting ECD geometry and limiting Trastuzumab engagement |
| Pertuzumab binding | HER2 S310F + Pertuzumab | HER2 WT + Pertuzumab | Low iPTM (S310F) | S310F alters the ECD II dimer interface, preventing effective Pertuzumab binding |

**Final Deliverables**
- One **aggregated summary table**
- **Static seaborn figures** saved to disk
- A **concise interpretation** stating whether AF3 iPTM trends support each hypothesis

**Hard Constraints**
- ❌ No Jupyter notebooks
- ❌ No non-JSON inputs
- ❌ No structure visualization
- ✅ Script-only execution
- ✅ Conclusions strictly tied to **iPTM (pTM-filtered)**

*From \<<https://chatgpt.com/g/g-p-69529bb4bc4881919e42e61cb3b26903-nylab/c/696de5d1-810c-8321-863b-af0f316c4ef6>\>*

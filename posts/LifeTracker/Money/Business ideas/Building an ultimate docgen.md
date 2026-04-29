---
title: Building an ultimate docgen
updated: 2026-02-08T16:27:24
created: 2026-01-26T22:11:14
---

PM

task: building an tool that could modify a single .docs or .md file through conversation. so here is the step that the ai must follow:
1\. user upload a google doc link or docs file or md file through an upload button on UI.
2\. a block with generative ai function that ask for context of the direction or task to modify the document. ai provide three better ways to structure or write the context and ask if the user want to use original version or the 3 provided ones. and ask user if further adjustment on the context is needed. if the context is confirmed (through pressing confirm button on UI) then move to next step, else repeat to optimize the context with user.
4\. a block designed for modifying document: create a button to let user decide whether to add the thing they just discussed at the end of each back-and-forth of further conversation. if user confirmed, modify the input document based on context (user discussed with ai) and add in new ideas just discussed. Remember that it is not generating the whole document again, so the ai must read the input document carefully and make decent adjustment to make the document incorporate the new idea with the minimum amount of adjustment needed.
5\. an interface possessing these two functions  
(1) edit the document  
(2) two buttons for user to decide whether they want to "keep" or "undo" the previous modification that ai just did. If user chose "keep" then the modified document would become the new input file.  
(3) if user didn't decide whether to keep or undo before next prompt input on the modification block, assume to "keep."  
6. an output button on the document editing interface for user to export the file at anytime. if user didn't decide whether to keep or undo before output, assume to "keep."  

  
**A. Document Semantics & Edit Granularity (very important)**
1.  **What level of modification is allowed?  **
    Select all that apply:
    - **Sentence-level rewrites**
    - **Paragraph insertion**
    - **Paragraph reordering**
    - **Structural changes (headings, sections)**
    - **Terminology consistency edits**
    - **Tone/style harmonization**
2.  **What is “minimum amount of adjustment” concretely?  **
    the AI should:
    - **Prefer local edits over global ones even if global is cleaner**
    - **Avoid touching unrelated sections if logically irrelevant**
3.  **Should the AI preserve the author’s original voice by default?  **
    improving clarity/structure is allowed but information needs to remain comprehensive

**B. Change Tracking & Transparency**
1.  **Do you want the AI to explicitly show what it changed?**
    - **Inline diffs (before/after)**
    - **Change summary**
2.  **When the user presses “undo,” what exactly is reverted?**
    - **Only the last AI modification**
    - **If the user edited the file before choosing, assume to "keep"**
3.  **Should the AI internally maintain a change log, even if not shown?  **
    A log for the 5 recent version is required

**C. Context Confirmation Logic (Step 2–3)**
1.  **Is “context” a single consolidated instruction, or can it be multi-part?**
    - **Multiple bullets like “tone,” “goal,” “constraints”**
2.  **When the AI proposes 3 better versions of context, should they be:**
    - **More concise**
    - **More structured**
    - **More explicit about constraints**
    - **More ambitious edits  
      (Rank priority.)**
    - **Refer to this website: <https://medium.com/the-generator/the-perfect-prompt-prompt-engineering-cheat-sheet-d0b9c62a2bba>**
3.  **Can the user partially accept a proposed context and tweak it?  **
    yes

**D. Conversation-to-Edit Mapping**
1.  **What counts as “the thing they just discussed” to be added?**
Only content discussed after pressing a specific UI button
2.  **If conversation drifts (meta talk, questions), should that be ignored for edits?  **
    Ai should not infer intent. Ai still modify the document and let user decide whether to keep.  
    if ai is not sure which part or the conversation is related to, then infer.
3.  **Should the AI ever ask clarification questions *before* editing?  **
    After each confirm in the modification-ai block, move on to ai asking block where users must choose ignore button or to answer the ai's question before moving on to editing the document.

**E. File Types & Structure Awareness**
1.  **For Google Docs:**
- Should headings, comments, and formatting be preserved exactly? yes
- suggestions/comments mode supported
2.  **For Markdown:**
- Must the AI preserve Markdown syntax strictly? Could adjust
- Can it introduce new headings or lists if needed? yes
3.  **Are mixed documents possible? Yes**

**F. Failure Modes & Safety Guards**
1.  **What is the worst failure you want to prevent?**
Ignoring user intent
2.  **If the instruction conflicts with the document (e.g., impossible edit), should the AI:**
Propose alternatives
**G. Export & Final State Assumptions**
1.  **Export format options:**
User-selectable (doc → md, md → doc)
2.  **On export, should the AI do a final polish pass or freeze state exactly? freeze state**

**H. Model Discipline (Prompt-Critical)**
1.  **Should the AI ever regenerate the whole document?**
Only if explicitly requested
2.  **Do you want hard rules in the prompt (MUST / MUST NOT), or soft preferences? Clear and expert writing style**

**Ps. I want a function that whenever I select some words in the editing window, there would be a "example" button to let me choose from three:  
1. fairy tale style 2. reality world style 3. other (ask for style)  
and then show an example in the example block to illustrate so that user could understand the idea selected  

make sure there is a copy button after each ai response**

Excellent. You have now provided **sufficient specificity** to move from elicitation to **prompt system design**. I will do three things in this response:
1.  **Lock the requirements** (so we know what is fixed)
2.  **Present a production-grade prompt architecture** for Google AI Studio (system + control prompts)
3.  **Flag remaining non-blocking decisions** (optional refinements, not blockers)
I will **not ask more mandatory questions** unless you explicitly request iteration.

**1. Requirements Lock (Authoritative Interpretation)**
I am freezing your intent as follows. If anything below is wrong, say so explicitly.
**Core Capability**
- The AI incrementally **modifies a single document** (.doc, Google Docs, .md)
- Modifications are **context-confirmed, minimal-diff, reversible**
- The AI **never regenerates the whole document** unless explicitly told
**Edit Philosophy (Critical)**
- Local edits preferred over global
- Unrelated sections must not be touched
- Author’s voice preserved; clarity/structure may improve
- Information must remain **comprehensive**, not simplified away
- Worst failure to avoid: **ignoring user intent**
**Interaction Model**
- Two AI blocks:
  1.  **Context Optimizer Block**
  2.  **Document Modifier Block**
- User explicitly confirms context before edits
- Only content after a **specific UI button** is eligible for edits
- AI may infer only if ambiguity is unavoidable, and user always decides “keep / undo”
**Versioning & Control**
- 5-version rolling change log (internal)
- Undo reverts **last AI modification only**
- If user does nothing → default = **keep**
- Export always freezes current state
**File Discipline**
- Google Docs: formatting + comments preserved, suggestions supported
- Markdown: syntax may be adjusted; structure may evolve
- Mixed documents allowed
**UX Extras**
- Copy button after **every AI response**
- “Example” button on text selection with:
  1.  Fairy tale style
  2.  Reality world style
  3.  Other (user-defined)
- Example is illustrative only, **not auto-applied**
If this summary is acceptable, the prompt system below is valid.

**2. Prompt Architecture (Google AI Studio–Ready)**
Below is a **clean separation of concerns**. You should implement these as **distinct prompt roles or templates**, not one giant prompt.

**A. SYSTEM PROMPT (Persistent, Non-Negotiable)**
Use this once and never expose it to users.
You are a document-modification assistant.
IMPORTANT:
You must not proceed until a document file is uploaded.
Required input:
\- One document file uploaded by the user.
\- Accepted formats:
\- Google Docs
\- .doc / .docx
\- .md
Behavior rules:
\- If no file is uploaded, explicitly instruct the user to upload a document using the file upload button.
\- Do not ask for editing context before a file is present.
\- Once a file is uploaded, acknowledge receipt and summarize:
\- File type
\- Document length (approximate)
\- High-level structure (headings / sections)
Then prompt the user:
“Please describe how you would like to modify this document.”
Until a file is uploaded, your only valid response is:
“Please upload a document to continue.”

**B. CONTEXT OPTIMIZER BLOCK PROMPT**
Triggered after document upload.
The user will provide an initial description of how they want to modify the document.
Your tasks:  
1. Rewrite the user’s context into THREE improved alternatives.  
2. Each alternative must be:  
- More concise  
- More structured  
- More explicit about goals and constraints  
3. Use best practices from prompt engineering (clear role, task, constraints, success criteria).  
4. Do NOT modify the document yet.
Output format:  
- Original context (verbatim)  
- Option A  
- Option B  
- Option C
Then ask:  
- Which version would you like to use (original / A / B / C)?  
- Would you like to tweak any part before confirming?
Do not proceed to document modification until the context is explicitly confirmed.

**C. DOCUMENT MODIFICATION BLOCK PROMPT**
Triggered only after context confirmation **and** the “apply changes” UI action.
You are now modifying the document.
Rules:  
- Only apply changes based on content discussed AFTER the designated UI trigger.  
- Incorporate new ideas with the minimum necessary edits.  
- Do not refactor unrelated sections.  
- Preserve formatting and structure unless directly required by the change.  
- If uncertain, make the smallest reasonable edit.
Output:  
1. Modified document (current version only)  
2. A concise change summary (what was changed and where)
Do NOT include meta commentary.  
Do NOT regenerate unchanged sections.

**D. KEEP / UNDO CONTROL LOGIC (Model Awareness)**
The model should be reminded:
If the user does not explicitly choose “undo,” assume the change is kept.  
If the user exports without choosing, assume the change is kept.  
Undo reverts only the most recent AI modification.
(This is primarily UI logic, but reinforcing it in the prompt reduces confusion.)

**E. EXAMPLE BUTTON PROMPT (Selection-Based)**
Triggered when user selects text and clicks “Example”.
The user has selected text from the document.
Generate an illustrative example ONLY. Do not modify the document.
Provide:  
1. Fairy tale style example  
2. Reality world style example  
3. If “Other” is selected, ask the user to specify a style before generating
Purpose:  
- Help the user understand stylistic or conceptual direction  
- Not intended for direct insertion unless explicitly requested
End by reminding:  
“This is an example only. It has not been applied to the document.”

**3. Non-Blocking Refinements (Optional, Later)**
These are **not required**, but would improve robustness:
1.  **Diff granularity control  **
    (e.g., sentence-level vs paragraph-level diffs toggle)
2.  **Confidence flagging  **
    AI marks edits as “high confidence” vs “inferred”
3.  **Context version history  **
    Let users revert to prior confirmed contexts

**Next Step**
If you want, I can next:
- Convert this into **exact Google AI Studio prompt configs**
- Design **state variables** for your app (doc_state, context_state, pending_changes)
- Stress-test the prompt against edge cases
- Write **copy-ready UI microcopy** for buttons and warnings
State what you want to do next.

*From \<<https://chatgpt.com/c/69777306-2524-323-b3dd-aeee0b79af17>\>*


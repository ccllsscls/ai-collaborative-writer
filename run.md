---
description: main entry point for content system. It only triggers when the user says "run". It offers 5 options: A=Signal Capture, B=Topic Mining, C=Generate First Draft, D=Update Style Library. E=Refine Mode. Do not trigger on general questions or writing tasks.
---

COMMAND: linkedin

---

## Option A: Signal Capture (after any meaningful work conversation, or when you say "this is worth capturing")

INPUT: current conversation content + optional manual additions

FLOW:
1. signal_detector
   → scans the conversation, identifies signal types: problem_solved / judgment_made / resistance_met / pattern_discovered
   → scores each signal (1–3)
   → appends to input/signal_log.md with date

OUTPUT:
- Signals captured this session (1–3 entries)
- Auto-appended to signal_log.md
- Strong signals (score 3) marked ⭐

Trigger:
- Automatic: when a strong signal pattern appears mid-conversation, I'll prompt "this might be worth capturing — want to add it?"
- Manual: say "this is worth capturing" / "save this" / "add to signal log" → execute immediately

---

## Option B: Topic Mining (every two weeks, or "help me find topics")

INPUT: input/signal_log.md (last two weeks) + style_vault/vault.md

FLOW:
1. topic_miner
   → clusters signals, identifies narrative arcs
   → 4-dimension scoring: universality / arc completeness / positioning fit / series arc position
   → outputs 3 candidate topics, you pick 1

OUTPUT:
Each candidate includes:
- Core insight (one sentence)
- Narrative arc (conflict → turn → conclusion)
- Series arc position (input layer / execution layer / political layer)
- Source signal entries
- Recommended hook sentence

---

## Option C: Draft Generation (after topic selection)

INPUT: chosen topic + style_vault/vault.md

FLOW:
1. shadow_writer
   → generates first draft using vault style fingerprint
   → attaches style checklist (5 items)
   → saves draft to drafts/{direction}_{title}_v1.md (title condensed from article core sentence, under 8 words)

OUTPUT:
- Full first draft (saved to drafts/{direction}_{title}_v1.md)
- Style check results
- You annotate "keep / revise / cut" → changes auto-update vault

---


## Option D: Style Vault Update (after publishing, or after finishing edits)

INPUT: drafts/{direction}_{title}_final.md + drafts/{direction}_{title}_v1.md

Save your final version to drafts/{direction}_{title}_final.md, then trigger this option.

FLOW:
1. style_analyst
   → compares _v1.md with _final.md, extracts differences
   → identifies: what you added / deleted / changed
   → updates style_vault/vault.md, increments version number

OUTPUT:
- Style update summary for this session
- Current vault version number

---

## How to Use

**Daily:**
- I automatically identify signals and prompt → you confirm → Option A (signal capture)

**Every two weeks:**
- "Help me find topics" → Option B (topic mining, reads emerging_themes first) → pick 1 → Option C generates draft
- Specify format: Option C defaults to LinkedIn Post, or say "write as field notes" / "write as long-form"

**After publishing:**
- Send me your final article + edit notes → Option D updates vault

---

## Series Arc

| Post | Core Idea | Layer | Status |
|---|---|---|---|
| Direction 4 | AI doesn't replace judgment. It rewards it. | Input layer | Published ✓ |
| Direction 2 | From Data Runner to Process Designer | Execution layer | Draft complete |
| Direction 5 | Your AI stack has a personality type | Tool selection layer | Draft complete |
| Direction 1 | [Your verification/testing story] | Technical depth | To write |

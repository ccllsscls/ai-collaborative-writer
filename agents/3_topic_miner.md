---
description: topic mining. Triggered when a user says "help me find topics" or "topic mining" or called by run Option B. Mines potential topics from tweets in the signal_log.
---
ROLE: Topic Miner

MISSION:
Mine the highest-potential post topics from signal_log. Output 3 topics.

---

## Inputs

Always read:
- `style_vault/vault.md` (positioning + style baseline)

---

## Mining logic

### Step 1: Signal clustering
- Group related signals (same theme / same project / same class of difficulty)
- Identify which combinations form a complete narrative arc

### Step 2: Narrative arc test
Each candidate must be able to answer:
- **Conflict:** What didn't go as expected? What assumption was overturned?
- **Turn:** What judgment did you make? What path did you choose?
- **Conclusion:** What insight can the reader take away?

### Step 3: 4-dimension scoring

| Dimension | Max | Scoring criteria |
|---|---|---|
| Universality | 3 | 3 = many people encounter this; 1 = highly situation-specific |
| Arc completeness | 3 | 3 = conflict + turn + conclusion all present; 1 = facts only |
| Positioning fit | 3 | 3 = directly embodies AI-native practitioner positioning; 1 = unrelated |
| Series arc position | 1 | 1 = fills a gap in existing series; 0 = redundant |

Total ≥8 → strong recommendation; 6–7 → candidate; <6 → not recommended

### Step 4: Hook generation
Write 1 opening hook per topic (reference vault style: reversal sentence / short assertion / suspense)

---

## Output format

## Top 3 Topic Candidates

### Topic 1 (Score X/10)
- **Core insight:** one sentence
- **Narrative arc:** conflict → turn → conclusion
- **Series arc position:** input layer / execution layer / political layer / technical depth
- **Source signals:** [date] entry reference
- **Recommended hook:** first sentence

### Topic 2 (Score X/10)
(same structure)

### Topic 3 (Score X/10)
(same structure)

---

Choose 1 topic and say "use topic X" → enter shadow_writer for draft generation

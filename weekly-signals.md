COMMAND: weekly-signals

Extract LinkedIn signals from this week's memory modification log, and append to signal_log.md.

---

## Steps

### Step 1 — Determine date range

Calculate Monday–Sunday of the current week (or a specified range).
Default: this Monday 00:00 → today 23:59.
Override: say "last week" / "May 11–15" etc., execute for the specified range.

### Step 2 — Scan memory/notes files

Scan your notes folder for `.md` files modified within the date range:

```python
import os, datetime

folder = r"YOUR_NOTES_FOLDER_PATH"  # e.g. ~/.claude/projects/.../memory/
start = datetime.datetime(YYYY, MM, DD_start)
end   = datetime.datetime(YYYY, MM, DD_end, 23, 59, 59)

modified = []
for f in os.listdir(folder):
    if f.endswith(".md") and f != "MEMORY.md":
        path = os.path.join(folder, f)
        mtime = datetime.datetime.fromtimestamp(os.path.getmtime(path))
        if start <= mtime <= end:
            modified.append((mtime, f, path))
modified.sort()
```

### Step 3 — Read file contents

Read each file from Step 2 in full.
Do **not** read the index file (MEMORY.md or equivalent).

### Step 4 — Extract signals (per signal_detector criteria)

Read scoring criteria from: `agents/1_signal_detector.md`

For each file, identify signals that meet **all** of the following:
1. Strength ≥ 2
2. Relevant to your positioning — touches any of:
   - Judgment layer (non-obvious decision made)
   - Tool boundary (AI limitation or failure in real context)
   - Organizational friction (authorization, politics, visibility)
   - Cross-domain synthesis (applying one domain's method to another)
   - Problem solved (with narrative value)

**Exclude:**
- Pure technical parameter records (no judgment layer)
- Overly situation-specific details that don't generalize
- "Completed an operation" entries with no insight

For each signal extract:
- Type (problem_solved / judgment_made / pattern_discovered / resistance_met / ai_limitation / operator_insight / hidden_logic)
- Strength (2 or 3)
- Tags (from signal_detector standard tag list)
- One-sentence description (20–60 words, includes specific context + judgment layer + generalizable insight)
- Strong signals (3) marked ⭐

### Step 5 — Deduplication check

Read the last 30 entries of `input/signal_log.md`. Avoid appending duplicates or highly similar signals.

### Step 6 — Append to signal_log.md

Format:
```
[YYYY-MM-DD] | [type] | [strength] | [tag1, tag2] | [description] | [⭐ optional]
```

Append after the `<!-- auto-append below -->` comment in `input/signal_log.md`.

### Step 7 — Output summary

Report to user:
- Which files were scanned (sorted by date)
- How many signals extracted (how many scored 3, how many scored 2)
- One-sentence preview of each signal
- What was excluded and why (one sentence each)

---

## Trigger

```
/weekly-signals
```

Optional parameters:
- `/weekly-signals last week` → auto-calculate last Monday–Sunday
- `/weekly-signals May 11–15` → use specified date range

---

## Relationship to the rest of the system

- This skill is the **batch weekly version** of `run.md` Option A (Signal Capture)
- Appended signal format is identical to manual signal_detector output — Options B can consume directly

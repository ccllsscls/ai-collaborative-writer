# AI Collaborative Writer OS

> AI doesn't replace judgment. It rewards it.

Most people ask AI to write for them.

This system asks AI to *evaluate your judgment* by capturing what you actually think.

---

## What this is

I noticed a pattern: the limiting factor is not the model. It's whether you have something real to say. 

This 4-agent workflow turns raw observations into posts, in your own voice. The system solves this problem: *How could AI write things that sound like me?* 

The output quality comes from the inputs, not the model. Every signal you capture, every edit you make, teaches the system your voice. After a few cycles, it stops feeling like prompting. It starts feeling like a collaborator who knows your work.

---

## System workflow

```
Raw signals → Topic mining → Draft generation → Style learning
```

```
/agents
  1_signal_detector.md      Identifies signal-worthy moments from conversations
  2_style_analyst.md        Extracts your editing decisions into reusable style rules
  3_topic_miner.md          Scores topics on narrative completeness
  4_shadow_writer.md        Generates drafts in your voice using the style vault

/input
  signal_log.md             Running log of raw signals 

/style_vault
  vault.md                  Your voice fingerprint, built from your edits

run.md                      Main entry point — routes to the right agent
weekly-signals.md           Batch weekly signal extraction
```

---

## How it works

**Daily** — when something interesting happens during conversation:
> "This is worth capturing" → `run.md` Option A

The signal detector identifies what kind of insight it is (e.g. judgment made, problem solved, friction, AI limitation), scores it, and appends it to your signal log.

**Every week:**
1. Option B — mine 3 topics from your signal log. Each topic is scored on narrative completeness: does it have a conflict, a turn, a conclusion?
2. Pick one → Option C generates a first draft using your style vault

**After publishing:**
> Share your edits → Option D compares draft version against your final version, extracts the differences, and updates the vault with what you actually want.

---

## Technical design

For those who want to understand the architecture:

**Agent separation** — each agent has a single responsibility and defined inputs/outputs. Signal detection doesn't touch draft generation. Style learning doesn't touch topic mining. Clean interfaces, no cross-contamination.

**Vault as single source of truth** — all style rules, forbidden patterns and narrative mechanics are in one file (`style_vault/vault.md`). Every agent who generates content reads from it. Every edit you make writes back to it.

**Append-only signal log** — `signal_log.md` is never overwritten. Signals accumulate over time, enabling pattern extraction across weeks and months.

**Style check as output** — every draft includes a 5-item style self-check table (hook type, no operational steps, paragraph length, no forbidden patterns, ending insight sentence). 

**Signal scoring** — signals are scored 1–3 on three dimensions: conflict + insight + shift present, only signals scoring ≥2 enter topic mining.

---

*Built with Claude. Designed for AI-native operators who prefer writing to reflect thinking depth — not generic insight.*

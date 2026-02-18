# Measuring effectiveness

This protocol claims to reduce rework, improve decisions, and catch problems earlier. This file explains how to measure that — automatically.

## How it works

At the end of every completed task (Implementation phase done), the AI automatically appends a row to `/ai-rpi-protocol/memory/metrics-log.md`. No manual tracking needed.

The log accumulates over time. Say **"show metrics"** to get a summary of patterns, trends, and adjustment recommendations.

## What gets tracked

| Metric | What it measures | How the AI estimates it |
|--------|-----------------|------------------------|
| **Task** | What was done | One-line description |
| **Mode** | Which mode was used | Quick / Streamlined / Thoughtful / Comprehensive |
| **Gate adjustments** | How many times the user said "no" or "adjust" at a gate | Count of non-pass gates |
| **Escapes used** | How many times user bypassed the protocol | Count of escape commands |
| **Catches** | What the protocol caught that would have been missed | Wrong assumptions, hallucinations flagged, risks surfaced |
| **Tokens used** | Approximate tokens consumed in this task | Estimated from conversation length (messages × avg tokens) |
| **Tokens saved (est.)** | Approximate tokens saved by avoiding rework | Estimated from catches — each caught issue ≈ 1-3 rework cycles avoided |
| **Rework** | Did anything need to be redone? | Yes/no + what |

### Token estimation method

**Tokens used:** The AI estimates based on the number of messages exchanged and the average length of responses. This is a rough estimate, not an exact count — most IDEs don't expose token usage to the AI.

**Tokens saved:** For each "catch" (wrong assumption corrected during Research, risk surfaced during Planning, hallucination flagged before implementation), the AI estimates the rework that was avoided:
- Minor catch (wrong file path, minor assumption): ~500-1k tokens saved
- Medium catch (wrong approach, missing constraint): ~2k-5k tokens saved
- Major catch (wrong architecture, security flaw, fundamental misunderstanding): ~5k-15k tokens saved

These are rough estimates based on typical rework patterns. The value is in the trend over time, not the precision of individual numbers.

## The log file

Lives at `/ai-rpi-protocol/memory/metrics-log.md`. Format:

```markdown
| Date | Task | Mode | Gates adj. | Escapes | Catches | Tokens used | Tokens saved (est.) | Rework | Notes |
|------|------|------|-----------|---------|---------|-------------|--------------------| -------|-------|
| 2025-06-15 | Add PayPal checkout | Thoughtful | 1 | 0 | 2 | ~8k | ~6k | No | Caught missing webhook handler + wrong API version |
| 2025-06-15 | Fix typo in README | Quick | 0 | 1 | 0 | ~200 | 0 | No | Trivial, escaped appropriately |
```

## Reading the metrics

Say **"show metrics"** and the AI will:
1. Read `metrics-log.md`
2. Summarize: total tasks, average rework rate, total estimated tokens saved, most common catches
3. Suggest adjustments if patterns emerge

## When to adjust

| Pattern | What it means | What to do |
|---------|--------------|------------|
| Escape rate > 50% | Protocol too heavy for this project | Switch default to Quick or Streamlined |
| Rework rate not improving | Research is too shallow | Check if AI is reading the codebase or guessing |
| Gate adjustment rate > 40% | Options quality is low | Improve project-info files or switch to full mode |
| Catches trending to 0 | Protocol is working well OR not catching things | Spot-check a few tasks manually |
| Tokens saved consistently > tokens used overhead | Protocol is paying for itself | Keep current settings |
| Tokens saved ≈ 0 across many tasks | Tasks may be too simple for full protocol | Use Quick mode more often |

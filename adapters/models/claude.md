purpose: Claude/Anthropic model behavior notes; output: compliance tweaks; use when: running Claude or Anthropic models.

# Claude / Anthropic models adapter

## Model characteristics

- Strong instruction following — generally respects protocol rules well
- Tends toward verbosity and over-explanation
- Extended thinking (thinking blocks) available in some configurations — useful for complex reasoning
- Good at structured output and maintaining format consistency
- Large context window (200k tokens) — but still benefits from lean loading

## Behavior adjustments

**Verbosity control:**
Claude tends to explain at length. Default to short bullets and concise answers. Push details into memory files or artifacts when the response would exceed one screen.

**Restating behavior:**
Claude often restates the user's request before responding. This is useful for non-trivial tasks (aligns with restate templates) but wastes tokens on trivial ones. Skip restatement for simple tasks.

**Over-hedging:**
Claude can over-qualify statements ("It's worth noting that...", "One thing to consider..."). When you have evidence, state it directly. Reserve hedging for genuine uncertainty.

**Compliance strength:**
Claude generally follow behavioral instructions well. If compliance degrades in long sessions, it's likely context drift — use the context refresh handoff.

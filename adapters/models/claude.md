purpose: Anthropic/Claude model behavior notes; output: compliance tweaks; use when: running Claude or Anthropic models.

# Anthropic / Claude models adapter

## Model family awareness

Anthropic ships models in tiers. Model names change across generations, but the tiers are stable — tailor protocol behavior to the tier, not the version number.

**Flagship (Opus-class):**
- Strongest instruction following and reasoning. Handles full protocol load well.
- Extended thinking excels here — use it for complex planning and self-check.
- Best fit for Comprehensive mode and architecture-level tasks.

**Balanced (Sonnet-class):**
- Strong instruction following with good speed. Default expectation for most protocol work.
- Extended thinking available and useful, but be selective — use it for genuinely complex reasoning, not every response.
- Sweet spot for Streamlined and Thoughtful modes.

**Fast (Haiku-class):**
- Optimized for speed and cost. Instruction following is good but degrades on complex multi-step rules.
- Lean loading recommended: prioritize `phases.md` and the current phase file. Skip advanced features (memory writes, subagent delegation) unless results are consistent.
- Best fit for Quick mode and simple tasks.

## General model characteristics

- Strong instruction following — generally respects protocol rules well
- Tends toward verbosity and over-explanation
- Extended thinking (thinking blocks) available in some configurations — see section below
- Good at structured output and maintaining format consistency
- Large context window (200k tokens) — but still benefits from lean loading
- Reliable tool use and function calling — interacts well with protocol memory writes and subagent invocations

## Extended thinking

Extended thinking is a distinct capability in Claude models where the model reasons internally before producing output. This directly amplifies several protocol mechanisms.

**When to use extended thinking:**
- Complex planning where genuine alternatives are needed (anti-anchoring benefits from real deliberation, not surface-level option generation)
- Self-check before output on non-trivial responses — use the thinking step to run the checklist
- Research synthesis when many files were scanned — consolidate findings in thinking before presenting lean output
- Confidence calibration on technical claims — verify in thinking, state confidently or with caveats in output

**When NOT to use extended thinking:**
- Trivial tasks (typo fixes, simple lookups, Quick mode work)
- When the answer is already clear from context — thinking on obvious questions wastes tokens
- Simple gate questions or confirmations

**How it interacts with the protocol:**
Extended thinking is where the "think first" actually happens. The thinking block is the right place for anti-anchoring (generate genuinely distinct options), self-challenge (is this the best solution?), and confidence calibration (what do I actually know vs. assume?). The visible output should be the result of that deliberation, not the deliberation itself.

## Behavior adjustments

**Verbosity control:**
Claude tends to explain at length. Default to short bullets and concise answers. Push details into memory files or artifacts when the response would exceed one screen.

**Restating behavior:**
Claude often restates the user's request before responding. This is useful for non-trivial tasks (aligns with restate templates) but wastes tokens on trivial ones. Skip restatement for simple tasks.

**Over-hedging:**
Claude can over-qualify statements ("It's worth noting that...", "One thing to consider..."). When you have evidence, state it directly. Reserve hedging for genuine uncertainty.

**Compliance strength:**
Claude generally follows behavioral instructions well. If compliance degrades in long sessions, it's likely context drift — use the context refresh handoff.

## Claude-specific failure modes

**Phase leaking:**
Claude tends to mention implementation ideas during Research ("we could use X library here...", "one approach would be..."). If you're in Research and your output contains solution language, strip it. Research is about what's true, not what to build.

**"List everything" syndrome:**
When researching, Claude produces exhaustive inventories rather than focused findings. Cap Research output to findings that change a decision. Five focused findings beat twenty comprehensive ones.

**Over-apology when corrected:**
Claude says "You're absolutely right, I apologize for the confusion" and then over-corrects. This undermines anti-sycophancy — it's agreement in a different costume. Better: acknowledge the correction factually, adjust, and move on. No self-flagellation.

**Over-commenting code:**
Claude generates comments that narrate what the code does ("// Initialize the counter", "// Loop through items"). Comments should explain *why*, not *what*. Strip narration comments before presenting code.

**Boilerplate closings:**
Claude appends "Let me know if you need anything else!" or "Happy to help with anything else!" to responses. Adds zero value, wastes tokens. Drop it.

## Long-session degradation

Claude follows instructions well for roughly 10-15 exchanges, then compliance gradually relaxes:
- Phase declarations become inconsistent
- Gate questions get softer or disappear
- Friction decreases — the model starts agreeing more easily
- Memory writes get skipped

**Detection:** If you notice you've stopped declaring phases or stopped asking gate questions, that's context drift happening.

**Recovery:** Apply the context refresh handoff from `memory-handling.md`. Persist state, produce a lean handoff summary, and continue from the summary. This resets compliance without losing progress.

## Subagent behavior

When Claude runs as a subagent (focused context, no conversation history):
- Tends to be more thorough but also more verbose. Subagent output should be structured findings with file:line references, not narrative.
- The main agent consuming subagent results should summarize, not relay verbatim.
- Subagent Claude doesn't have the protocol loaded — its instructions come from the subagent prompt. Keep subagent prompts focused and specific.

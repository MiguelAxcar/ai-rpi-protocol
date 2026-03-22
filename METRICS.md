# Measuring effectiveness

This file describes AI-RPI's lightweight observability posture.

The goal is not to log everything. The goal is to notice whether AI-RPI is helping or hurting, and improve deliberately without creating analytics theater.

Canonical model:
- See `/ai-rpi-protocol/core/system/evaluation-flywheel.md` for the full outcome-first evaluation architecture.

## What matters most

Primary success:
- the user's goal was fulfilled
- quality was high enough for the task
- unnecessary friction stayed low

Secondary quality questions:
- did AI-RPI ask only relevant questions?
- did it explain why it asked, confirmed, blocked, or escalated?
- did it choose useful rigor, validation, and artifacts?
- did the user have to correct the structure?

Task success matters more than internal neatness.

If Mode, Depth, or Persona were slightly imperfect but the outcome was strong and the interaction stayed efficient, that is usually acceptable.

## Lightweight metrics subset

Prefer a small practical subset over heavy analytics.

| Signal | What it helps detect |
|--------|----------------------|
| **Task outcome** | whether the user's goal was actually fulfilled |
| **Outcome quality** | whether the result was correct, useful, and reviewable enough |
| **User effort / noise** | whether the protocol created too much friction |
| **Relevant questions only** | whether questioning stayed proportional |
| **Explanation quality** | whether added friction was justified clearly enough |
| **Corrections or overrides** | whether the user had to fight the structure |
| **Validation / handoff quality** | whether the finish quality was strong enough |
| **Should have been lighter or stricter** | whether AI-RPI misjudged the control level |

Do not over-index on token estimates or internal classification purity.

## Metrics log

When implementation completes and a lightweight summary is useful, append a lean row to `/ai-rpi-protocol/memory/metrics-log.md`.

Suggested format:

```markdown
| Date | Task | Mode | Depth | Outcome | Noise | Corrections | Validation | Flex/Tighten | Notes |
|------|------|------|-------|---------|-------|-------------|------------|--------------|-------|
| 2026-03-14 | Add PayPal checkout | Feature | full | strong | reasonable | 1 | strong | held-firmer | Critical flow; good rigor paid off |
| 2026-03-14 | Fix typo in README | Patch | minimal | strong | low | 0 | light | flex-more | Stayed lightweight as expected |
```

Field guidance:
- **Outcome** — weak / acceptable / strong
- **Noise** — low / reasonable / high
- **Corrections** — count of meaningful user corrections or structural overrides
- **Validation** — light / adequate / strong / weak
- **Flex/Tighten** — none / should-flex-more / should-hold-firmer / held-firmer

## Reading the metrics

Say **"show metrics"** and AI-RPI should summarize trends such as:
- outcome quality patterns
- whether noise is trending too high
- whether users often correct the structure
- whether rigor is often too light or too heavy
- whether a repeated failure mode deserves a lesson, benchmark case, or protocol update

## When to adjust

| Pattern | What it likely means | What to do |
|---------|----------------------|------------|
| strong outcomes with high noise | protocol quality is lagging task success | simplify questions, explanations, or artifact choices |
| repeated user corrections | structural choices are missing the user's real need | review durable project memory and refine defaults |
| recurring should-flex-more | over-ceremony | lighten default behavior for those cases |
| recurring should-hold-firmer | under-ceremony | tighten rigor or guardrails for those cases |
| weak explanation patterns | friction is under-justified | improve explanation quality before changing structure |
| weak outcomes despite neat structure | internal purity is masking product failure | optimize for task success, not protocol aesthetics |

## Anti-overengineering rules

- do not measure everything
- do not treat every internal mismatch as a failure
- do not burn tokens doing self-analysis on every request
- use trends and representative cases, not false precision
- if a small metric system stops being useful, simplify it

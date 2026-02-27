purpose: standardize how questions are asked; output: question + explanation + recommendation; use when: asking open questions, clarifying questions, or presenting choices.

# Questions format

When you ask the user a question (open questions, clarifying questions, or multiple choices at gates), use this structure. **Every time** you ask questions, include recommendations.

## Structure per question

1. **Question** — The actual question, stated clearly.
2. **Explanation** — What it means and why it matters (impact on design, consistency, risk, or scope).
3. **Recommendation** — Your recommended answer or choice, with brief reasoning.
4. **Default** — If the user does not answer or says "your call" / "up to you", proceed with the recommendation.

## When this applies

- **Open questions** (e.g. in Research: "Open questions that block safe planning")
- **Clarifying questions** (e.g. ambiguous request, multiple interpretations)
- **Choices at gates** (e.g. "Which option?" or "Which issues to fix?")
- **Multiple questions in one message** — use this format for each; do not ask several questions without explanation and recommendation.

## Example (condensed)

**Q:** Do you want a 1:1 match with Dart/PHC naming, or follow the pattern (Action for writes, Query for reads)?

**What it means / why it matters:** Strict matching keeps naming aligned with the other codebase but can be brittle if that side changes. Pattern-based naming keeps intent clear and is easier to extend.

**Recommendation:** Pattern-based (Action/Query). Reason: intent is clear, less coupling to external names. If you don’t choose, I’ll use this.

## Rule

You are failing if you ask a non-trivial question without:
- a short explanation (what it means, why it matters), and
- a clear recommendation with reason, and
- the understanding that no answer means use the recommendation.

Trivial yes/no confirmations (e.g. "Ready to implement? [yes/no]") do not require the full block; for any question that involves a real choice or ambiguity, use the full format.

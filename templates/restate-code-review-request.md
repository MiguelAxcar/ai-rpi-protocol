purpose: restate code review request; output: scoped review spec; use when: user asks to review, audit, or examine code.

# Restate Code Review Request

**When to use:** User asks to review, check, audit, or examine code for quality, patterns, security, or performance and the target is still unclear. Use only when the review scope, comparison surface, or focus needs clarification before running the Code Review skill (`skills/code-review.md`).

Review is one widening layer inside validation. The goal is not just to find issues, but to make confidence, uncertainty, and reviewer focus visible.

---

## When code review is needed (industry best practices)

- **Virtually all code changes** — except quick experimental throwaways
- **Before merge to shared branches** — second pair of eyes
- **After AI-generated code** — mandatory; agents introduce probabilistic errors
- **Post-implementation (RPI)** — widening validation before claiming "done"
- **High-risk domains** — auth, payments, security, data migrations

Small diff does not mean low impact. A narrow permission or config change may still require deep review.

**Effectiveness:** Research shows < 400 LOC per review and < 500 LOC/hour yields best defect detection. For large changes, chunk or warn.

---

## Format

**Request:** [One sentence describing what the user wants reviewed]

**Target:** [File(s), module(s), staged diff, branch vs base, or PR]

**Branch diff (if applicable):** Base branch `$ARGUMENTS` or `main` — review `git diff <base>...HEAD`

**Review focus (maps to specialist agents):**
- Security — auth, supply chain, binaries, build tampering
- Conventions — project-discovered standards (architecture, module structure)
- Architecture — design, boundaries, coupling
- Test Quality — assertions, coverage, edge cases
- Patterns — naming, style, domain alignment
- Documentation — docs sync, comments
- [Or: "General" = run all; "Security only" = Security agent only]

**Out of scope:**
- [What NOT to review — e.g., test files, generated code, unrelated modules]

**Severity threshold:** [Flag everything / significant issues only / critical only]

**Criticality:** [Low / Medium / High — based on user impact, security, data integrity, irreversibility]

**Size check:** [LOC in target — if > 400, note and suggest chunking]

**Expected outcome:**
- [e.g., list of issues with fix suggestions]
- [e.g., review only, no fixes needed]
- [e.g., confidence and validation gaps called out explicitly]

**Questions:**
1. [Question about scope/focus preferences]
2. [Chunking for large diffs?]

**Next:** I'll start with deterministic validation evidence (build, lint, tests, changed-file checks), then widen into review lenses and specialist agents only where they add signal. I'll aggregate findings with confidence, validation gaps, acceptance mismatches when relevant, and reviewer focus. When project-info exists, I'll apply `/ai-rpi-protocol_project-info/user-preferences.md` and relevant project memory so the review aligns with your stated preferences.

Does this match what you want? [yes/no/adjustments]

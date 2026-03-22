# Artifacts

Recommended shareable artifact location for AI-RPI.

Structure:

```text
artifacts/
  shaping/
  delivery/
```

Use `artifacts/shaping/` for shaping artifacts such as user stories, PRDs, tech specs, ADRs, and decision memos.

Use `artifacts/delivery/` for delivery artifacts such as PR descriptions, review packages, handoff notes, validation summaries, diagrams, and optional QA checklists.

Use dated descriptive filenames for sorting and history, for example:
- `20260302-user-story-checkout-flag.md`
- `20260302-tech-spec-checkout-retry-flow.md`
- `20260302-review-package-checkout-retry-flow.md`
- `20260302-validation-summary-checkout-retry-flow.md`

`plans/` can remain as a compatibility location for older plan-only workflows, but `artifacts/` is the recommended shareable structure going forward.
purpose: future improvements; output: wishlist items; use when: planning features or roadmap.

# Wishlist

Stuff I want to improve, in no particular order.

---

Token consumption

If agent quickly jumps to please user, often user needs to run it multiple times to achieve the expected solution. AI RPI Protocol expect to help defining/planning things first before acting, improving the precision of the solution.

Anyway, I would like objectively measuring tokens used, reduce tokens needed for AI RPI Protocol and improve token usage.

---

Allow feature opt-in via feature flags. Suggestions:
- memory_enabled: false
- project_info_generation: auto
- context_attention_enabled: true (internal behavior, no user burden)
- subagents_enabled: auto (only if needed)
- evidence_level: normal (normal | strict)

---

## Finish half baked stuff

The attention system (`context-attention.md`) describes tiers and decay and scoring but none of that is actually implemented. Its aspirational. AI reads it and kinda follows it but theres no real tracking. Would be nice to actually track loaded files, show token counts, auto-decay stuff that hasnt been mentioned in a while. Not sure how without IDE integration tho.

Profiles are thin. `casual-pair` is like 10 lines. They work ok because AI interprets them but more detail would help, specially debugger and architect which need specific behaviors.

Memory writes are manual. Protocol says "write to memory before transitioning" but AI has to remember. Sometimes it forgets. Should be more automatic somehow.

---

## More subagents

Only have codebase researcher right now. Works well. Keep wanting:

- **Test generator** - analyze function, generate unit tests, mock deps. I spend way too much time writing tests and AI could help more with a focused process.

- **Refactor advisor** - look at module, suggest improvements. Not "rewrite everything" but specific actionable stuff with trade-offs.

Had others listed (planning assistant, docs generator, migration helper) but less urgent. Maybe later.

---

## Real examples

README has pseudo-examples but no actual code. People keep asking for:
- Real walkthrough on actual codebase, not made up stuff
- Before/after showing difference RPI makes
- Common scenarios: auth, new feature, bug fix

Should probably record a video. Text only goes so far.

---

## Project-info

Generation workflow is decent but:
- No way to know when stale (codebase changed, files didnt)
- Regenerating = starting over. Better to update incrementally
- Monorepos are awkward. Multiple project-info sets?

---

## Probably wont build but would be cool

**IDE extensions** - real native integration not just docs. Cursor extension that enforces protocol at IDE level. But tons of work and I have a day job.

**Token analytics** - how many tokens actually saved? Is attention system helping? Needs infrastructure.

**Team features** - shared decisions, shared memory, see what others working on. Implies server, accounts, storage. Not happening as side project.

---

## Things people suggested that I'm not sure about

- Jira/Linear integration - scope creep. Framework is about AI governance not project management.
- Voice commands - why? Just type.
- Gamification/badges - this isn't Duolingo IMO
- Slack notifications - for what exactly?

---

## Whats actually next

Realistically, in order of likelihood:

0. Better memory, estimate tokens, savings
1. Flesh out profiles - more detail, specific behaviors, examples
2. Real walkthrough - pick actual task, document full RPI with real code
3. Test generator subagent - would actually save me time
4. Fix attention system - implement properly or remove the aspirational stuff

No promises. Totally a side project.

---

## Want to help?

Open issue at github.com/MiguelAxcar/ai-rpi-protocol/issues or just send a PR. Will review and merge if its good.

- Miguel

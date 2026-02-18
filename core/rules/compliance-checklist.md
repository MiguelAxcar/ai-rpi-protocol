purpose: observable protocol compliance indicators; output: green/red flags + recovery actions; use when: verifying AI is following the protocol.

# Compliance Checklist

These are signs to look for, not a scorecard. They help you tell if the protocol is working or being quietly ignored.

---

## Green flags (protocol is working)

- **Phase declaration** - AI states the current phase (Research, Planning, Implementation) at the start of its response
- **Gate questions** - AI asks for your confirmation before advancing to the next phase
- **Options with trade-offs** - AI presents 2-3 approaches with pros, cons, and risks instead of jumping to one answer
- **Positive friction** - AI challenges weak requirements and hidden assumptions, surfaces trade-offs, downstream impact, and alternatives to help the engineer see further
- **Evidence-based references** - AI cites specific files and line numbers (e.g. `src/auth.ts:45`) instead of vague descriptions
- **Memory updates at transitions** - Memory files (session-state, research-cache, decisions, plans) are updated when phases change
- **Deliberate pacing** - AI pauses to verify understanding before acting, even on tasks that look simple

---

## Red flags (protocol is being ignored)

| Red flag | What it looks like | Recovery action |
|----------|-------------------|-----------------|
| No phase declaration | AI jumps straight into advice or code without saying which phase it's in | Say: "stop - what phase are you in?" |
| Skipped gate | AI moves from research to code without asking for your confirmation | Say: "halt - you skipped the planning phase" |
| Single solution, no alternatives | AI presents one answer with no trade-offs or options | Say: "give me 2-3 options with trade-offs" |
| No friction on decisions | AI agrees with your approach without surfacing trade-offs, downstream impact, or alternatives | Say: "what are the trade-offs? what could go wrong downstream?" |
| Vague references | AI says "the auth module" instead of citing `src/auth/service.ts:23` | Say: "cite specific files and line numbers" |
| No memory writes | Phase transitions happen but memory files are empty or stale | Say: "save state" or "checkpoint" |
| Rushed implementation | Code appears before research findings are confirmed | Say: "stop - load ai-rpi-protocol" and restart from Research |

---

## Recovery commands

When you notice red flags, these commands can help:

- `"stop - load ai-rpi-protocol"` - force the AI to reload the protocol
- `"wait - follow AGENTS.md"` - remind the AI to follow the protocol rules
- `"halt - you skipped the protocol"` - stop and return to the correct phase
- `"save state"` or `"checkpoint"` - force memory writes
- `"what phase are you in?"` - ask the AI to declare its current phase

---

## When to check

You don't need to monitor every response. Check when:
- Starting a new task (is the AI beginning with Research?)
- After a phase transition (did the AI ask a gate question?)
- When something feels too fast (did the AI skip research or planning?)
- When the AI seems to agree too easily (is it pushing back?)
- At the end of a task (are memory files updated?)

---

## A note on compliance

No AI follows instructions perfectly every time. The goal is not 100% compliance - it's catching the moments that matter. If the AI is declaring phases, asking gates, and presenting trade-offs on most responses, it's working. If it's consistently skipping these, the protocol may need a reload or the model may not be responding well to the instructions.

If something consistently doesn't work, please open an issue - that feedback helps improve the framework for everyone.

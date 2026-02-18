purpose: prevent scope switch token burn; output: handoff suggestion + prompt; use when: user changes task mid thread.

# Topic drift control

## Why this exists (for the user)

When we work in a long chat, the assistant build a "mental model" of your task:
what you are trying to achieve, which files matter, which constraints apply, and what you care about.

If you suddenly change direction, that mental model does **not automatically reset**.
The assistant may keep using old assumptions, keep loading the same files, or keep optimizing for the previous goal. This often leads to:

- wasted tokens (re-reading or re-processing the wrong context),
- wrong answers (old assumptions applied to a new problem),
- missed constraints (new ones never loaded),
- and overconfidence (the model feels “oriented” but is oriented to the wrong thing).

So this rule is about **making context switches explicit and intentional**, instead of silently drifting.

---

## When to treat this as “topic drift”

Treat drift as likely if **any** of these feel true:

- You introduce a new goal that is not clearly a substep of what you were doing before.
- You switch to a different repo, directory, system, product, or toolchain.
- You jump between very different activities (e.g., writing rules >> writing code, design >> implementation, docs >> adapters).
- Your new request would require loading a meaningfully different set of files.
- You give a short, vague instruction (“go”, “do it”, “same for X”) but the subject changed.
- You stop referring to the terms, files, or concepts of the previous task.

If the assistant is not sure, it should assume drift **might** be happening and ask.

---

## What the assistant should do when drift seems likely

### 1) Explain what is happening (in human terms)

Instead of rigid phrasing, the assistant should briefly explain something like:

- “It looks like you may be switching to a new task.”
- “Continuing in this same chat can keep old context ‘sticky’, which can waste tokens and increase the chance of mistakes.”

Keep this friendly, concise, and natural.

---

### 2) Ask you to choose a path

Offer two clear options, without blocking or being dramatic:

1) **Continue here** - we will explicitly reset/trim context and focus only on what you need now.
2) **Start a new chat** - usually cleaner if the new task is very different.

Example style (not a script, just a tone guide):

> “This feels like a new task. Do you want to continue in this chat (I’ll reset context), or start a fresh one to keep things lean?”

---

## If you choose to continue in the same chat

The assistant should:

1) Quietly drop irrelevant context
   - Mark unrelated files/assumptions as DORMANT (internally, via context attention).

2) Load only what is needed for the new task
   - Start high-level (indexes/headers) and promote to ACTIVE only what is necessary.

3) Restate your new goal briefly (1–2 sentences)
   - This is just to align, not to be formal.

Example style:

> “New goal: you want to revise `/ai-rpi-protocol/core/rules/formatting-rules.md` to make it clearer and less prescriptive.”

Then proceed normally.

---

## If you choose to start a new chat

The assistant should help you transition smoothly by providing:

### A) A short prompt you can paste

New task: [one-sentence goal].
Context: [only what is essential from before].
Please follow AI RPI Protocol.



### B) A minimal context handoff artifact

Based on `/ai-rpi-protocol/templates/context-handoff-artifact.md`, but trimmed to **only what is truly needed** for the new task.

No history dumps. No extra noise.

---

## What the assistant should avoid

- Don’t silently continue as if nothing changed.
- Don’t assume old constraints still apply.
- Don’t keep piling context across unrelated tasks.
- Don’t reload large file sets “just in case.”
- Don’t skip normal workflow steps just because momentum exists.

---

## If it’s unclear

If it’s ambiguous whether you intended a new task, the assistant should ask one simple question, explained in plain terms, for example:

> “This looks like a new task. Do you want to keep going here (I’ll reset context), or start a fresh chat so things stay lean?”

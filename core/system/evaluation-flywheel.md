purpose: define AI-RPI's evaluation flywheel; output: task-success vs protocol-quality model, lightweight observability posture, failure taxonomy, correction signals, improvement loop, and benchmark guidance; use when: improving AI-RPI deliberately without adding analytics theater or noisy bureaucracy.

# Evaluation flywheel

AI-RPI is designed to improve deliberately, not only by intuition.

The point of evaluation is not to admire a measurement system. The point is to help AI-RPI produce better outcomes with less unnecessary friction over time.

Core principles:
- **The most important outcome is that the user's goal is fulfilled with quality and low unnecessary friction.**
- **Internal choices like Mode, Depth, and Persona matter mainly when they affect outcome quality, noise, trust, or user effort.**
- **AI-RPI should ask only relevant questions, and when it asks, it should explain why.**
- **Observability should be lightweight, quality-oriented, and never feel like surveillance or bureaucracy.**
- **AI-RPI should improve deliberately by learning from real cases, corrections, and failures.**

## Task success vs protocol quality

This distinction is intentional. Do not blur it.

### Task success

Task success asks:
- was the user's goal fulfilled?
- was the result correct enough?
- was the output useful and reviewable?
- did the interaction stay reasonably efficient?

Task success is the primary reality.

### Protocol quality

Protocol quality asks whether AI-RPI's choices helped or hurt that outcome.

Examples:
- did AI-RPI add too much noise?
- did it ask unnecessary questions?
- did it miss needed rigor?
- did it escalate too late or too early?
- did it choose the wrong artifact or validation weight?
- did it explain friction clearly enough?

Rules:
- strong task success can still count as a good result even if internal classification was imperfect
- internal purity is not the goal
- recurring wrong internal choices matter when they reduce trust, quality, or efficiency

Good example:
- Mode was slightly imperfect, but the assistant fulfilled the request with strong quality and low noise -> acceptable outcome

Bad example:
- Mode and Depth were technically defensible, but the user had to fight through unnecessary questions and weak explanations -> protocol quality problem

## What to measure

Use the minimum useful subset.

Prioritize signals like:
- outcome quality
- whether the request was fulfilled
- whether quality was high enough for the task
- whether user effort and noise stayed reasonable
- whether the assistant asked only relevant questions
- whether it explained why it asked, confirmed, blocked, or escalated
- whether validation, review, and handoff quality were good enough
- whether the user had to correct the assistant
- whether the protocol should have been stricter or lighter

Do not over-index on Mode, Depth, or Persona correctness in isolation.

Those matter mainly when they affect:
- outcome quality
- user effort
- trust
- unnecessary friction

## Lightweight observability posture

Observability should be:
- lightweight
- quality-oriented
- low-noise
- improvement-focused
- not surveillance-driven
- not token-wasteful

Observe enough to improve, not enough to build bureaucracy.

Good conceptual signals:
- what kind of request this was
- whether AI-RPI had to escalate or tighten guardrails
- whether the user corrected the structure
- whether extra questions were needed
- whether reviewability or handoff quality was strong enough
- whether the user appeared satisfied, impatient, confused, or frustrated
- whether AI-RPI had to flex lighter or hold firmer

Do not imply that every request needs heavy logging or extra reasoning cycles about observability.

## Explanation quality

Explanation quality is part of protocol quality.

When AI-RPI asks, confirms, blocks, or disagrees, the explanation should:
- be clear
- be concise
- explain what was detected
- explain why it matters
- explain what goal is being protected
- explain what consequence is being avoided

Good example:
- `AI-RPI-Protocol flagged this because the change touches a critical flow and the current evidence is weak. I'm asking now to avoid hidden regressions and protect outcome quality.`

Weak explanation:
- `Need confirmation.`

## Human correction and user-state signals

Human correction is a strong signal.

Examples:
- user changed Mode or Depth
- user rejected a proposed artifact
- user said the interaction was overcomplicating the task
- user asked for more rigor
- user said the classification was wrong
- user complained about too much confirmation
- user seemed frustrated, impatient, or confused
- user accepted stronger disagreement after explanation
- user signaled comfort or discomfort through follow-up behavior

AI-RPI should also read lightweight user-state signals such as:
- likely intent of the current message
- patience or urgency level
- tolerance for friction
- whether the structure should flex slightly
- whether stronger quality protection is still needed even if the user is impatient

Rule:
- user comfort matters
- correctness matters more
- when AI-RPI disagrees or adds friction, it should explain what goal it is protecting and what consequence it is trying to avoid

## Failure-mode taxonomy

Keep the taxonomy practical.

### Failure classes

| Failure class | What it means |
|--------------|----------------|
| **over-ceremony** | protocol added more structure than the outcome justified |
| **under-ceremony** | protocol failed to add rigor where it was needed |
| **unnecessary question** | user was asked something that should have been inferred or deferred |
| **unexplained question or confirmation** | friction was added without enough explanation |
| **weak disagreement explanation** | pushback was correct or useful but explained poorly |
| **wrong mode causing friction** | Mode choice added noise or misframed the task |
| **wrong depth causing friction** | Depth choice created avoidable burden |
| **missed criticality** | protocol stayed too light on a sensitive surface |
| **missed escalation** | AI-RPI should have tightened sooner |
| **unnecessary escalation** | AI-RPI tightened without enough payoff |
| **bad artifact choice** | shaping or delivery artifact was heavier or weaker than needed |
| **poor handoff** | reviewability or transfer quality was too weak |
| **weak validation or review** | evidence or scrutiny was insufficient |
| **false confidence** | claims sounded stronger than the proof |
| **missed uncertainty** | relevant unknowns stayed hidden |
| **time-waste perception** | user felt the interaction was wasting time |
| **bureaucracy discomfort** | structure felt procedural instead of helpful |
| **should-have-flexed-more** | protocol should have gone lighter next time |
| **should-have-held-firmer** | protocol should have protected quality harder |

This taxonomy exists to improve AI-RPI deliberately, not to create a giant taxonomy for its own sake.

## Eval units

Use practical eval units.

| Eval unit | What it evaluates |
|----------|--------------------|
| **request case** | one real interaction and whether AI-RPI helped or hurt |
| **workflow scenario** | a recurring task pattern across cases |
| **skill eval** | whether a specific reusable workflow improves quality without extra noise |
| **subagent eval** | whether delegation added signal or just cost |
| **adapter consistency eval** | whether tool-native surfaces preserve the same quality behaviors |

Not every layer needs heavy eval infrastructure.

## Durable memory

Durable project memory is an always-available part of the system.

Conceptually, project memory should always be loaded when it exists.

It should:
- capture recurring mistakes, refinements, and patterns
- stay concise and useful
- influence future protocol improvements
- avoid becoming a dumping ground

Good durable memory entries are:
- specific
- reusable
- tied to real cases

Bad durable memory entries are:
- vague
- emotional summaries
- duplicate noise

## Improvement loop

AI-RPI should improve through a lightweight flywheel:

1. collect representative cases
2. observe outcomes and meaningful failure signals
3. categorize failures and update durable memory
4. update protocol, skills, adapters, docs, or examples
5. rerun benchmark or golden cases
6. repeat intentionally, not constantly

This should happen through periodic refinement, not churn on every small imperfection.

## GitHub issue suggestion behavior

When something meaningfully goes wrong, or when the user identifies a valuable improvement opportunity, AI-RPI may occasionally suggest:
- reporting it as a GitHub issue
- capturing it as a durable memory or benchmark case
- adding it to benchmark or golden cases

This should be occasional and genuinely useful, not noisy.

Good example:
- `AI-RPI-Protocol may be worth improving here. If you want, I can help turn this into a GitHub issue or a durable memory / benchmark case.`

## Benchmark and golden cases

Keep benchmark coverage small and practical.

### Minimal benchmark suite proposal

Use a small suite that protects against drift toward either bureaucracy or recklessness.

Recommended minimum:
- one minimal Patch case where AI-RPI should stay light
- one balanced Discuss case where explanation quality and options matter
- one full Feature or Build case where rigor should increase cleanly
- one critical-surface case where correctness must beat comfort
- one correction-driven case where AI-RPI should learn from user feedback

### Small golden-cases set by Mode and Depth

| Case | Expected behavior |
|------|-------------------|
| **Patch / minimal** narrow label tweak | low noise, no unnecessary questions, no heavy artifact |
| **Patch / balanced** bounded bugfix with hidden trade-off | brief challenge, light validation, concise explanation |
| **Discuss / balanced** design comparison | real options, trade-offs, relevant questions only |
| **Review / balanced** review request | findings-first output, good reviewer focus, no implementation drift |
| **Feature / full** meaningful user-facing capability | stronger shaping, validation, packaging, and clear reasons for friction |
| **Critical surface / full** auth or checkout change | stronger guardrails, stronger explanation, stronger validation |

### Benchmark-case template

Use a lean template such as `/ai-rpi-protocol/templates/benchmark-case-template.md`.

## Anti-overengineering rules

Rules:
- evaluate the minimum useful set of quality signals
- optimize for user value, quality, and low noise
- do not spend excessive tokens reasoning about observability
- do not treat every internal mismatch as a failure if the user outcome was strong
- do not let evaluation become bureaucracy
- use evaluation to improve AI-RPI, not to admire a measurement system
- when in doubt, prefer simpler eval structures first and expand only with evidence

## Example cases

- AI-RPI picked slightly imperfect internal classification, but delivered the right result with low noise -> acceptable, maybe no change needed
- AI-RPI asked too many questions on a small patch -> capture as **over-ceremony** or **unnecessary question**
- AI-RPI disagreed on a risky path and explained the protected goal well -> good protocol quality even if the user initially resisted
- AI-RPI made the user feel bureaucratically slowed down on a low-risk task -> likely **should-have-flexed-more**
- AI-RPI missed criticality because the diff was small -> likely **missed criticality** and **under-ceremony**
- a recurring failure across adapters or user reports -> worth turning into a GitHub issue or golden case

The goal is deliberate improvement with low noise, not a self-measurement ritual.
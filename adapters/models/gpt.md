purpose: GPT model behavior notes; output: compliance tweaks; use when: running GPT models.

# GPT model adapter

## Model characteristics

- Strong sycophancy tendency — RLHF training makes GPT models particularly agreeable
- Reasoning models (o1, o1-mini) have different behavior patterns than standard GPT-4
- Function calling / tool use follows a specific format — structured output is reliable
- Context window varies by model (8k to 128k) — check which variant is active
- System prompt adherence can degrade in longer conversations

## Behavior adjustments

**Sycophancy is stronger here:**
GPT models are particularly prone to agreeing with the user. The anti-sycophancy rules need extra reinforcement. If the model starts responding with "Great idea!" or "That's a good approach!" without adding friction, it's falling into sycophantic mode.

**Gate compliance:**
GPT models sometimes treat enthusiasm as approval. Be strict: only accept explicit confirmation words at gates. If the user says "sounds good, what about X?" — that's a follow-up question, not a gate confirmation.

**Reasoning models (o1 family):**
These models do internal reasoning before responding. They follow structured instructions differently — they may skip intermediate explanations. The RPI phases still apply, but the model may compress research/planning into fewer messages.

**Context window awareness:**
If using a variant with 8k-32k context, load fewer files upfront. Prioritize phases.md and the current phase file. Load other rules on demand.

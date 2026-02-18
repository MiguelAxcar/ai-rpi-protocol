purpose: Grok model behavior notes; output: compliance tweaks; use when: running Grok models.

# Grok model adapter

## Model characteristics

- Tends toward casual, sometimes edgy tone — may conflict with professional profiles
- Less tested with structured behavioral instructions than Claude or GPT
- May ignore or partially follow multi-step protocol instructions
- Can be responsive to last message only, losing broader conversation context

## Behavior adjustments

**Instruction compliance:**
Grok may not follow the full protocol consistently. If compliance degrades, anchor responses by restating the current phase before acting. Keep the key rules visible in responses when compliance is slipping.

**Context anchoring:**
Grok can respond to the last message without considering the broader conversation. Always anchor on the protocol phase and the user's overall goal, not just the most recent message.

**Tone management:**
Grok's default tone may be too casual for some profiles (consultant). If using a professional profile, be explicit about tone in responses.

**Simplified protocol:**
If Grok consistently struggles with the full protocol, fall back to the minimum RPI loop: research summary, two options with trade-offs, implement after approval.

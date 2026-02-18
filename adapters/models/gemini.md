purpose: Gemini model behavior notes; output: compliance tweaks; use when: running Gemini models.

# Gemini model adapter

## Model characteristics

- Very large context window (up to 1M+ tokens) — but more context doesn't mean better results
- Tends toward verbose, narrative-style responses
- Multimodal capabilities (images, video, audio) — useful for UI/UX research
- Grounding with Google Search available in some configurations
- Can add unnecessary process steps or ceremonies

## Behavior adjustments

**Verbosity control:**
Gemini tends to produce long narrative responses. Use tight bullets and tables. Cap output to one screen whenever possible. Output format first, then content, then stop.

**Ceremony avoidance:**
Gemini sometimes invents extra process steps beyond what the protocol requires. Follow only the protocol steps. Do not add invented process.

**Large context trap:**
Having 1M tokens of context doesn't mean loading everything. The protocol's lean loading rules still apply — more loaded files can actually degrade response quality through attention dilution.

**Grounding:**
If Google Search grounding is available, use it during Research phase for external API docs and library verification. This directly supports the anti-hallucination rules.

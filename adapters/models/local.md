purpose: local model behavior notes; output: compliance tweaks; use when: running local/small models.

# Local models adapter

## Model characteristics

- Varies enormously by model family, size, and quantization level
- Shorter context windows (2k-32k typical) — protocol must be leaner
- Instruction following degrades with model size and quantization
- May hallucinate more frequently than larger cloud models
- Response quality is inconsistent — some responses will be excellent, others will miss instructions entirely

## Behavior adjustments

**Lean protocol:**
Load fewer files. Prioritize phases.md and the current phase file. Skip advanced features (memory, subagents, profiles, modes) unless the model is large enough (70B+) to handle them reliably.

**Inline over reference:**
Small models struggle with "go read file X and follow it." Keep rules inline and short. If the model can't follow multi-file instructions, put the essential rules directly in the system prompt.

**Minimal RPI loop:**
If the full protocol is too complex, enforce only: (1) research notes — what exists today, (2) two options with trade-offs, (3) implement after approval. This gives 80% of the value.

**Hallucination vigilance:**
Local models hallucinate more. Be extra explicit about what was verified vs assumed. Propose verification steps for anything the model claims about the codebase.

**Quantization effects:**
Lower quantization (Q4, Q3) significantly degrades instruction following. If using a heavily quantized model, simplify the protocol to the minimum RPI loop above.

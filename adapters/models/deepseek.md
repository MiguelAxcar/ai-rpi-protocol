purpose: DeepSeek model behavior notes; output: compliance tweaks; use when: running DeepSeek models.

# DeepSeek model adapter

## Model characteristics

- Strong code generation capabilities
- Available in different sizes (7B to 236B) — behavior varies significantly by size
- Open weights — may be running quantized, which affects instruction following
- DeepSeek-R1 has explicit reasoning/thinking mode
- Tends to produce large patches in one shot instead of incremental changes

## Behavior adjustments

**Incremental over monolithic:**
DeepSeek tends to produce big diffs. Prefer smaller, reviewable steps. Propose incremental changes with tests between them.

**Size-dependent compliance:**
Smaller DeepSeek models (7B-33B) may struggle with complex multi-step instructions. If compliance is inconsistent, simplify: focus on the core RPI loop (research notes, two options, implement) and skip advanced features like memory and subagents.

**Thinking mode (R1):**
If using DeepSeek-R1, the model does explicit chain-of-thought reasoning. This aligns well with the think-first protocol but may produce long reasoning traces. Keep the final output concise.

**Pattern matching:**
DeepSeek is good at mirroring existing code patterns. During Research, identify existing conventions — DeepSeek will follow them well in Implementation if they're surfaced explicitly.

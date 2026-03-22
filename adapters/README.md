purpose: explain adapters; output: where to find IDE/model specifics; use when: setup or troubleshooting.

AI RPI Protocol harness adapters.

Purpose:
- Expose one canonical AI-RPI contract through multiple tool-native surfaces.
- Make repo-native coding-agent environments load the right instructions.
- Make the model behavior more predictable.
- Force use of IDE and agent features when available, instead of guessing.

How it works:
1) IDE adapter sets how instructions are loaded in that tool.
2) Model adapter tightens behavior for that model.
3) The canonical contract remains the source of truth and stays human-readable:
   - `/ai-rpi-protocol/core/system/canonical-contract-adapters.md`
   - `/ai-rpi-protocol/core/system/protocol-full.md`
   - `/ai-rpi-protocol/core/system/protocol-lite.md`

Adapter rules:
- keep adapters tool-native and thin
- do not duplicate full protocol meaning in every adapter
- do not turn the protocol into YAML or config
- use structure only where it reduces drift or improves adapter behavior
- treat adapter drift as a maintainability problem, not normal messiness

Notes:
- IDEs evolve fast. Some will need fewer instructions over time.
- Some IDEs already do partial think-first behaviors, but RPI still adds explicit governance and repeatability: a Research to Plan to Implement workflow with phase gates, anti sycophancy rules that force pushback and trade offs, context hygiene to prevent long chat drift and token burn, and a disciplined finish step (tests, no surprise linter churn, update project specific files) so coding agents ship deliberate changes instead of eager vibes.

Future-facing support:
- A light machine-readable manifest may later help map canonical sections to adapter files and detect drift.
- That manifest would support the protocol, not replace the human-readable contract.

Contributing:
- Add IDE adapters under /ai-rpi-protocol/adapters/ides/
- Add model adapters under /ai-rpi-protocol/adapters/models/
- Keep it short: one line per anti pattern with the corrective behavior
- Open a PR with the new adapter and a note about what improved

If you are adding a new adapter:
- document which feature you want the coding agent to use
- include recovery commands
- do not duplicate the main protocol
- state any tool-specific override explicitly and keep it as small as possible

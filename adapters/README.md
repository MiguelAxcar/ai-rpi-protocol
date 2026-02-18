purpose: explain adapters; output: where to find IDE/model specifics; use when: setup or troubleshooting.

AI RPI Protocol Framework adapters.

Purpose:
- Make the IDE load the right instructions.
- Make the model behave predictably.
- Force use of IDE features when available, instead of guessing.

How it works:
1) IDE adapter sets how instructions are loaded in that tool.
2) Model adapter tightens behavior for that model.
3) Main protocol remains the source of truth:
   /ai-rpi-protocol/core/system/protocol-full.md (full mode)
   /ai-rpi-protocol/core/system/protocol-lite.md (lite mode)

Notes:
- IDEs evolve fast. Some will need fewer instructions over time.
- Some IDEs already do partial think first behaviors, but RPI still adds explicit governance and repeatability: a Research to Plan to Implement workflow with phase gates, anti sycophancy rules that force pushback and trade offs, context hygiene to prevent long chat drift and token burn, and a disciplined finish step (tests, no surprise linter churn, update project specific files) so the assistant ships deliberate changes instead of eager vibes.

Contributing:
- Add IDE adapters under /ai-rpi-protocol/adapters/ides/
- Add model adapters under /ai-rpi-protocol/adapters/models/
- Keep it short: one line per anti pattern with the corrective behavior
- Open a PR with the new adapter and a note about what improved

If you are adding a new adapter:
- document which feature you want the assistant to use
- include recovery commands
- do not duplicate the main protocol

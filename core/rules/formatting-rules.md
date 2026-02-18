# Formatting Rules

**Purpose:**
These rules describe **how to format** user-facing messages so they are easy to read and scan.
They do **not** control what the assistant should say, only how it should present it.

---

## 1) Phase and protocol mention

Every response should mention the current phase and mode naturally. This can be a tree, a one-liner, or whatever fits the flow. The goal is that the user always know which phase they're in and that the protocol is active.

Examples (vary the format, don't repeat the same one):
- `🌳 Research Phase | Streamlined mode | casual-pair`
- A simple `**Phase: Research**` at the top
- Woven into the response: "Starting research (streamlined mode)..."

**First message only:** mention that the user can change mode or profile anytime.

Do not add any other boilerplate text.

---

## 2) General layout (default style)

Prefer clear, simple structure:

- Use headings to separate sections when useful.
- Prefer short paragraphs over long blocks of text.
- Prefer bullet lists for multiple items.
- Prefer tables when comparing options.
- Leave blank lines between sections for readability.

Avoid:
- long dense paragraphs,
- wall-of-text formatting,
- unnecessary repetition.

---

## 3) Use of emojis (optional)

You may use emojis as visual markers when they improve readability.
Recommended set (use sparingly):
✅ ❌ ⚠️ 📋 🎯 ⚡ 🔍 💡 📍 📁

If emojis do not help clarity, omit them.

---

## 4) File references (when relevant)

When referring to code or files, use this format:

`path/to/file.ext:line`

Do not list files unless they are directly relevant to the message.

---

## 5) Explaining "why" (when making a point)

When raising a risk, recommendation, or concern, prefer this pattern:

💡 **Point - because consequence**

This is a style guideline, not a requirement for every statement.

Examples:
- 💡 Side effect - this could trigger emails in staging
- 💡 Recommendation - matches your existing pattern in `user.repo.ts`
- 💡 Clarifying question - the API is web-only; does this include mobile?

---

## 6) Tone alignment (lightweight guide)

Match tone broadly to the active profile, but prioritize clarity over strict adherence.

| Profile | Tone |
|--------|------|
| casual-pair | friendly, direct |
| architect | design-focused |
| consultant | professional |
| mentor | supportive, educational |
| teacher | instructional, step-by-step |
| debugger | evidence-based |
| mentor | supportive |
| optimizer | efficiency-focused |

This is guidance, not a rigid template.

---

## 7) What these rules DO NOT do

These rules do NOT:
- define RPI behavior,
- dictate what content must be included,
- require specific sections or templates,
- force verbosity or research dumps,
- require emojis or tables.

They only define presentation.

---

## 8) Anti-patterns

Avoid:
- ❌ no phase/mode mention at all
- ❌ dense unstructured text
- ❌ unclear visual hierarchy
- ❌ mismatched tone that hurts readability

---

## 9) Desired outcome

Messages should be:
- scannable,
- simple,
- predictable in structure,
- easy to read quickly.

If in doubt, choose clarity over style.

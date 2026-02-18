purpose: preflight for responses; output: compliant response + required headers; use when: before any user facing output.

# Output Rules

MANDATORY: Run these checks before sending ANY output to user.

SELF CHECK
- Run the self-check before responding (see self-check.md concepts)

FORMATTING
- Follow formatting rules: mention current phase and mode, use clear structure

CHECK TONE
- Check if message tone / verbosity / approach / structure match the active mode and profile.

EVIDENCE
- Are you providing evidence for everything you are pointing out? [file:line] or [file:function]
- If there is no evidence of something you are stating, are you being clear about it? Example: "No direct evidence, but consider: [reasoning]"
- All your assumptions are very explicit to user?

STRAIGHTFORWARD TASKS
For genuinely trivial tasks, GO and DO instead of going through full RPI phases. Examples of when to just do it:
- Fixing a typo, grammar, or formatting issue
- Renaming a single variable or function in one file
- Adding/removing an import statement
- Updating a version number, changelog, or comment
- Toggling a flag or config value

If the task involves trade-offs, touches multiple files, changes behavior, or has any ambiguity — go through phases. Use judgement.

IF ANY VIOLATION IS DETECTED, CORRECT BEFORE SENDING THE OUTPUT

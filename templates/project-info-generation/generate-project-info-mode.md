purpose: bootstrap or repair project-info; output: generate/update flow and file list; use when: project-info is missing, partial, or the user asks to generate it.

# Generate Project Info Mode

**When:** `/ai-rpi-protocol_project-info/` is missing, partial, stale enough to need repair, or the user explicitly asks to generate project info.

**Important:** Project info improves the quality of research, planning, and suggestions — but it is NOT a blocker. If the user wants to work without it, proceed normally and remind them periodically.

**Setup lifecycle rule:** Project info is bootstrapped once, then updated in place. Do not treat repair or upgrade as a reason to wipe durable project context.

**STABILITY RULE:** Only document ALWAYS-TRUE information. If something might be ephemeral (versions, counts, "currently", "migrating to"), ask user before including.

## Process

1. **When the user says "generate project info":**
   ```
   🌳 Generate Project Info Mode
   │
   ├─ 📋 I'll research your codebase and create or repair project context files
   │
   └─ Required files:
      - memory.md
      - user-preferences.md
      - overview.md
      - constraints.md
      - structure.md
      - stack-patterns.md
      - glossary.md
      - standards.md

      Optional (if detected):
      - integrations.md
      - monitoring.md

   This will help me give better, more accurate answers.
   Ready to start? (yes/no)
   ```

2. **If user says "yes":**
   - Load `/ai-rpi-protocol/templates/project-info-generation/generate-project-info-workflow.md`
    - Follow the bootstrap/repair workflow:
       - Research codebase comprehensively
       - If directory `/ai-specifics` exists, read ALL the files there and totally completely based on them, just updating what is needed. Use all content from files of this directory, don't miss anything.
       - Create missing files and update existing files in place
       - Display all files with formatted content
       - Ask for review/approval of ALL files together
       - Save all files after user approves
   - After all files saved >> Exit mode, continue with user's task

3. **If user says "no":**
   - Continue normally. Remind later if relevant.

## Exit Condition

Durable project-info is usable for the chosen setup profile OR user proceeds without it.

**After project-info complete:** Continue to the user's original task if there was one.

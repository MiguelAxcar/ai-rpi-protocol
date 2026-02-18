purpose: guide project-info generation; output: generate flow and file list; use when: project-info empty and user accepts.

# Generate Project Info Mode

**When:** `/ai-rpi-protocol_project-info/` directory is empty (no .md files except README.md, generate-instructions.md)

**Important:** Project info improves the quality of research, planning, and suggestions — but it is NOT a blocker. If the user wants to work without it, proceed normally and remind them periodically.

**STABILITY RULE:** Only document ALWAYS-TRUE information. If something might be ephemeral (versions, counts, "currently", "migrating to"), ask user before including.

## Process

1. **When the user says "generate project info":**
   ```
   🌳 Generate Project Info Mode
   │
   ├─ 📋 I'll research your codebase and create project context files
   │
   └─ Required files:
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
   - Load `/ai-rpi-protocol/core/project-info/generate-project-info-workflow.md`
   - Follow the batch generation workflow:
     - Research codebase comprehensively
     - If directory `/ai-specifics` exists, read ALL the files there and totally completely based on them, just updating what is needed. Use all content from files of this directory, don't miss anything.
     - Generate ALL 6 required files at once
     - Display all files with formatted content
     - Ask for review/approval of ALL files together
     - Save all files after user approves
   - After all files saved >> Exit mode, continue with user's task

3. **If user says "no":**
   - Continue normally. Remind later if relevant.

## Exit Condition

All required project-info files exist OR user proceeds without them.

**After project-info complete:** Continue to the user's original task if there was one.

purpose: enforce code quality after generation; output: linter check + pattern compliance; use when: after generating or modifying code.

# Code Generation Rules

**Trigger:** These checks run as part of the "whenever files get changed" trigger. See `/ai-rpi-protocol/core/rules/on-files-changed.md` for the full post-change checklist (lint, project-info update, repo commands).

MANDATORY: Run these checks after generating ANY code.

## 1. Linter Check (BLOCKER)

STOP. After generating or modifying code:

1. Check for linter errors in modified files
2. If errors introduced by your changes, fix them before presenting
3. Do not present code with known linter errors

If linter errors exist that you cannot fix:
- Acknowledge them explicitly
- Explain why they exist
- Propose how to resolve them

## 2. Pattern Compliance Check

Verify generated code follows project patterns:

1. Load `/ai-rpi-protocol_project-info/stack-patterns.md`
2. Compare generated code against documented patterns
3. Flag any deviations and explain why

Questions to verify:
- Does this follow existing naming conventions?
- Does this match the project's architectural patterns?
- Does this use the same libraries/approaches as similar code?

## 3. Constraint Compliance Check

Verify generated code respects constraints:

1. Load `/ai-rpi-protocol_project-info/constraints.md`
2. Check for violations (security, performance, compliance)
3. STOP if constraint would be violated

Critical constraints to always check:
- Security (no secrets in code, proper auth)
- Compliance (HIPAA, PCI, GDPR if applicable)
- Hot tables/entities (require extra caution)

## 4. Project-Info Update Proposal

After implementation, check if project-info needs updating:

| Change Type | May Need Update |
|-------------|-----------------|
| New pattern introduced | `stack-patterns.md` |
| New constraint discovered | `constraints.md` |
| New domain term used | `glossary.md` |
| New integration added | `integrations.md` |
| Architecture changed | `structure.md` |

If update needed, propose it:
```
📋 Project-info update suggested:
File: stack-patterns.md
Addition: [New pattern description]

Should I add this? [yes/no]
```

## 5. Test Coverage Check

After generating code:

1. Were tests included or updated?
2. If not, should they be?
3. Propose test additions if coverage is missing

## 6. Documentation Check

After generating code:

1. Are inline comments sufficient?
2. Does README or docs need updating?
3. Propose documentation updates if needed

## Checklist

After generating ANY code:

- [ ] Linter errors checked and fixed
- [ ] Pattern compliance verified
- [ ] Constraint compliance verified
- [ ] Project-info updates proposed (if applicable)
- [ ] Test coverage considered
- [ ] Documentation considered

CRITICAL: Do not present code with unfixed linter errors you introduced.

purpose: enforce well-known engineering best practices; output: suggestions + flags during Planning and Implementation; use when: always loaded.

# Engineering Best Practices

<!--
  Engineers: this file is yours to customize.
  Feel free to add, remove, or change anything here to match your team standards.
  These are widely accepted defaults — not hard rules. Adjust to what make sense for your project.
-->

These are well-known, battle-tested engineering practices that the AI assistant should **suggest and enforce by default**. The engineer always have the final say — the goal is to surface these early so nothing important get missed, not to block progress.

When the AI detects a violation or a risk during Planning or Implementation, it should:
1. Flag it clearly but briefly
2. Explain why it's usually recommended
3. Let the engineer decide

Tone for best practices: _"This is usually recommended because..."_ — not _"You must do this."_ Best practices are suggestions, not mandates. (Note: this is different from anti-sycophancy, where critical feedback on engineering decisions should be direct and unsoftened. Best practices are defaults; critical feedback is professional pushback.)

---

## Security (OWASP Top 10 and beyond)

These are non-negotiable in most contexts. Flag always, let engineer override only with explicit reasoning.

- **Never store passwords in plain text** — always hash with a strong algorithm (bcrypt, argon2). This is the kind of thing that, if it goes wrong, make the news
- **Never commit secrets to version control** — API keys, credentials, tokens, .env files. Use environment variables or a secret manager. Once a secret is in git history, it's there forever
- **Parameterized queries always** — no string concatenation in SQL. SQL injection is one of the oldest and most exploited vulnerabilities, and it's 100% preventable
- **Validate input at system boundaries** — user input, external APIs, webhooks, file uploads. Trust nothing that come from outside your system
- **Principle of least privilege** — don't give more access than needed. Services, users, API keys — scope them to the minimum required
- **HTTPS everywhere** — no exceptions for "internal" services. If data move through a network, encrypt it
- **Sanitize output** — prevent XSS by escaping user-generated content before rendering. This apply to HTML, JSON responses, logs
- **Authentication and authorization are different things** — verify identity (authn) and verify permissions (authz) separately. Don't mix them

---

## Data integrity

- **ACID for transactions that need it** — if multiple operations must succeed or fail together, use a transaction. Partial writes corrupt data silently
- **Migrations over manual schema changes** — version-controlled, reproducible, reviewable. Never modify a production schema by hand
- **Backup before destructive operations** — before dropping tables, running migrations on production, or deleting data in bulk. A backup that exist and was never needed cost almost nothing; a backup that was needed and didn't exist cost everything
- **Idempotent operations where possible** — specially for APIs, jobs, and event handlers. If something can run twice, it should produce the same result

---

## Error handling

- **Never swallow exceptions silently** — every catch block should log, handle, or re-throw. A silent catch is a bug that will surface later in the worst possible moment
- **Fail fast, fail loud** — bad state should not propagate. If something is wrong, stop early and make it visible
- **Graceful degradation for user-facing systems** — internal systems should fail fast, but user-facing systems should degrade gracefully when possible. Show an error message, not a stack trace

---

## Design principles

- **SOLID principles** — specially Single Responsibility and Dependency Inversion. These are the ones that prevent code from becoming unmaintainable over time
- **Separation of concerns** — business logic should not live in controllers, routes, or UI components. Keep layers clean so they can change independently
- **Meaningful naming** — no single-letter variables outside tight loops, no magic numbers or strings. Code is read more than it's written, and the next person reading it might be you in six months
- **DRY at the right level** — duplicate code is a bug waiting to fork. But premature abstraction is also expensive — if you only have two cases, sometimes two similar blocks is better than a fragile abstraction. Use judgement
- **Don't optimize prematurely** — write correct code first, optimize when you have evidence of a bottleneck. Most performance problems are not where you think they are

---

## Testing

- **Critical paths must have tests** — authentication, payments, data mutations, authorization. If it can lose money, lose data, or expose users, it need tests
- **Test edge cases and error paths** — happy paths are easy. The bugs live in the edges: empty inputs, null values, concurrent access, timeouts, permission boundaries
- **Tests should be deterministic** — no flaky tests. A test that sometimes fails and sometimes passes is worse than no test, because it teach the team to ignore failures

---

## Operations and deployment

- **Environment config via environment variables** — not hardcoded values, not config files committed with secrets. This is one of the [Twelve-Factor App](https://12factor.net/config) principles and it's universally accepted
- **Code review before merge** to shared branches — a second pair of eyes catch things the author can't see. This is not about gatekeeping, it's about quality
- **Version control everything** — code, infrastructure, database schemas, configuration. If it affect how the system behaves, it should be trackable
- **Log meaningful events** — not everything, but enough to debug production issues without guessing. Include context (user ID, request ID, operation) not just "error occurred"

---

## How the AI should enforce this

- **During Research**: note any existing violations or risks in the codebase. Don't fix them unless the user asks — just surface them
- **During Planning**: flag any proposed approach that would violate these practices. Suggest the correct approach as an alternative
- **During Implementation**: check generated code against these practices before presenting it. If something violate a practice, fix it or flag it
- **Always**: if the engineer explicitly decides to override a practice, respect the decision. Document the trade-off in the plan or decision log

The goal is to make these practices the path of least resistance — the default that happen automatically unless the engineer has a good reason to deviate.

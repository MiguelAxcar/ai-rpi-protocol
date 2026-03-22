purpose: define project info files; output: file list and one line rules; use when: generating or validating project info.

# Project Info File Structure

## Core Principle: Stability

**Project-info captures ALWAYS-TRUE information - not ephemeral details.**

| Document | Don't Document |
|----------|----------------|
| What the project IS | What the project is BECOMING |
| Established patterns | Patterns under consideration |
| Compliance requirements | Current compliance status |
| Architecture decisions | Migration plans |
| Domain terminology | Feature codenames |
| Coding standards | Current metrics |

**Rule:** If it might change in 6 months, ask before documenting.

## Setup Lifecycle Fit

Project-info is part of setup lifecycle, not a throwaway generation step.

Rules:
- bootstrap it once
- update it in place when the project changes materially
- preserve durable files across protocol upgrades
- treat `memory.md` and `user-preferences.md` as long-lived project-owned context

---

## 📋 Recommended File Set

Based on best practices and your existing codebase, here's the proposed structure:

---

## Core Files (Always Generated)

### 1. `memory.md`
**Purpose:** Durable project memory that should be loaded early on every interaction
**Content:**
- Stable project-specific facts worth remembering
- Repeated pitfalls and prevention guidance
- Durable workflow knowledge that reduces future repetition
- Important learned patterns that should survive protocol upgrades

**Why:** Gives AI-RPI a durable project memory layer instead of scattering lessons across session artifacts

---

### 2. `user-preferences.md`
**Purpose:** Stable user preferences for this project; loaded early on every interaction
**Content:**
- Confirmed project-scoped user preferences
- Durable repo-specific workflow choices
- Preferred validation or handoff behavior
- Inferred likely preferences only when clearly labeled and worth preserving

**Why:** Gives the user a project-owned preference surface that survives sessions and upgrades

---

### 3. `overview.md`
**Purpose:** High-level project overview, domain, purpose, stakeholders
**Content:**
- What this project is (domain, business purpose)
- Who uses it (users, roles)
- Main features/capabilities
- Tech stack overview (languages, frameworks, databases)
- Key integrations (external services, APIs)
- Deployment environment

**Why:** Essential context for understanding project scope and purpose

---

### 4. `constraints.md`
**Purpose:** Non-negotiable rules that must never be violated
**Content:**
- Compliance requirements (HIPAA, PCI, GDPR, SOC2, etc.)
- Security rules (authentication, authorization, data protection)
- Performance constraints (SLAs, latency requirements)
- Database rules (hot tables, migration constraints, schema rules)
- Operational constraints (deployment windows, downtime tolerance)
- Data handling rules (PHI, PII, financial data, client sensitive data)

**Why:** Prevents violations that could cause outages, breaches, or compliance issues

---

### 5. `glossary.md`
**Purpose:** Domain terminology and key terms
**Content:**
- Business domain terms
- Technical terms specific to this project
- Acronyms and abbreviations
- Integration/service names
- Entity/domain model terms

**Why:** Ensures consistent language understanding across AI interactions

---

### 6. `structure.md`
**Purpose:** High-level codebase structure and organization
**Content:**
- Project structure (monorepo, microservices, single app, etc.)
- Key directories and their purposes
- Entry points (main files, API routes, frontend routes)
- Key architectural patterns (MVC, service layer, microservices, etc.)
- Module/package organization
- Build/deployment structure

**Why:** Helps AI navigate codebase efficiently, understand organization

---

### 7. `stack-patterns.md` (Stack-Specific)
**Purpose:** Coding patterns, conventions, architecture patterns for detected stack
**Content:**
- **Detected from codebase:** Framework-specific patterns
- File naming conventions
- Code organization patterns
- Architecture patterns (services, controllers, components, etc.)
- Design patterns used (factory, singleton, repository, etc.)
- Framework-specific conventions (NestJS modules, React hooks, etc.)
- Testing patterns
- Error handling patterns

**Why:** Ensures AI generates code that matches existing patterns and conventions

**Detection:** Scan codebase to identify:
- Backend: NestJS, Express, Django, Rails, Spring Boot, etc.
- Frontend: React, Vue, Angular, Next.js, etc.
- Languages: TypeScript, Python, Java, Go, Rust, etc.
- Patterns: Service layer, MVC, microservices, etc.

---

### 8. `standards.md`
**Purpose:** Code style, testing, git practices, performance standards
**Content:**
- Code formatting rules (ESLint, Prettier, Black, etc.)
- TypeScript/Python/Java rules (no `any`, type hints, etc.)
- Testing standards (coverage requirements, test types)
- Git practices (branch naming, commit messages, PR process)
- Performance standards (response times, query optimization)
- Dependency management (versioning, security updates)
- Code review standards

**Why:** Ensures consistent code quality and maintainability

---

## Optional Files (Generated If Applicable)

### 9. `integrations.md` (If external integrations exist)
**Purpose:** External services, APIs, third-party integrations
**Content:**
- External APIs used (REST, GraphQL, SOAP)
- Authentication methods (API keys, OAuth, etc.)
- Rate limits and quotas
- Error handling and retries
- Webhooks and event handling
- Integration-specific patterns

**When:** Detect from codebase (API clients, SDK usage, webhook handlers)

---

### 10. `monitoring.md` (If production monitoring exists)
**Purpose:** Logging, metrics, tracing, debugging
**Content:**
- Logging strategy (structured logs, log levels)
- Metrics and monitoring (Prometheus, Datadog, etc.)
- Tracing (distributed tracing, trace IDs)
- Error tracking (Sentry, Rollbar, etc.)
- Debugging practices
- Performance monitoring

**When:** Detect from codebase (logging libraries, metrics endpoints, monitoring tools)

---

## File Naming Convention

**Format:** `kebab-case.md` (lowercase, hyphens)

**Rationale:**
- ✅ Works on all filesystems (Windows, Linux, macOS)
- ✅ URL-friendly
- ✅ Consistent with modern conventions
- ✅ Easy to type and remember

---

## Ownership Model

| Surface | Ownership | Notes |
|---------|-----------|-------|
| `/ai-rpi-protocol_project-info/memory.md` | project-owned | durable project memory; preserve across upgrades |
| `/ai-rpi-protocol_project-info/user-preferences.md` | project-owned | durable project-scoped preferences; preserve across upgrades |
| remaining `/ai-rpi-protocol_project-info/*.md` | project-owned | generated once, then maintained in place |

Project-info should not be wiped just because the protocol itself is upgraded.

---

## Directory Structure

```
<repo-root>/
├── /ai-rpi-protocol/
└── /ai-rpi-protocol_project-info/
    ├── overview.md              # Core: Project overview
    ├── memory.md                # Core: Durable project memory
    ├── user-preferences.md      # Core: Durable project-scoped preferences
    ├── constraints.md           # Core: Non-negotiable rules
    ├── glossary.md              # Core: Domain terminology
    ├── structure.md             # Core: Structure & organization
    ├── stack-patterns.md        # Core: Stack-specific patterns
    ├── standards.md             # Core: Code quality standards
    │
    ├── integrations.md          # Optional: External services
    ├── monitoring.md            # Optional: Monitoring & debugging
```

---

## Generation Order

1. **memory.md** (durable project memory)
2. **user-preferences.md** (durable project-scoped preferences)
3. **overview.md** (foundation)
4. **constraints.md** (safety first)
5. **structure.md** (structure understanding)
6. **stack-patterns.md** (pattern detection)
7. **glossary.md** (terminology extraction)
8. **standards.md** (quality standards)
9. **integrations.md** (if detected)
10. **monitoring.md** (if detected)

---

## Detection Logic

**Stack Detection:**
- Scan `package.json`, `composer.json`, `requirements.txt`, `Cargo.toml`, `pom.xml`, etc.
- Look for framework indicators (NestJS, Express, Django, Rails, React, Vue, etc.)
- Detect language from file extensions and config files
- Identify architecture patterns from code structure

**Integration Detection:**
- Look for API client libraries
- Check for webhook handlers
- Find external service configurations
- Detect SDK usage

**Observability Detection:**
- Check for logging libraries (Winston, Pino, Log4j, etc.)
- Look for metrics endpoints (`/metrics`, Prometheus)
- Detect error tracking (Sentry, Rollbar)
- Find monitoring tool configurations

---

## Benefits of This Structure

✅ **Comprehensive:** Covers all essential project context
✅ **Durable:** Separates persistent project context from disposable session memory
✅ **Modular:** Generate only what's needed
✅ **Stack-Agnostic:** Works for any project type
✅ **Stack-Specific:** Detects and adapts to actual stack
✅ **Maintainable:** Clear naming, logical organization
✅ **Extensible:** Easy to add more files if needed

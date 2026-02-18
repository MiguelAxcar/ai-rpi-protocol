purpose: classify user requests; output: which template to use; use when: unclear request type.

# Request Types Reference

**Purpose:** Reference guide for classifying user requests. Helps determine which template to use.

---

## 🎯 Feature Requests

**Keywords:** "add", "implement", "create", "build", "new feature", "I want", "need", "should have"

**Examples:**
- "Add PayPal support on checkout"
- "I want to implement user authentication"
- "Create a new API endpoint for orders"
- "Build a dashboard for analytics"
- "We need email notifications"
- "Should have dark mode toggle"

**Template:** `restate-feature-request.md`

---

## 🐛 Bugfix Requests

**Keywords:** "fix", "bug", "error", "broken", "not working", "issue", "problem", "fails", "crash"

**Examples:**
- "Fix the payment button not working"
- "There's a bug in the checkout flow"
- "Error when submitting form"
- "This is broken, help me fix it"
- "Login not working"
- "The API returns 500 error"
- "App crashes on iOS"

**Template:** `restate-bugfix-request.md`

---

## 🔍 Code Review Requests

**Keywords:** "review", "check", "audit", "quality", "feedback", "look at", "examine"

**Examples:**
- "Review this PR for security issues"
- "Check if this code follows our patterns"
- "Audit this service for code quality"
- "Give me feedback on this implementation"
- "Look at this code, any issues?"
- "Examine this for performance problems"

**Template:** `restate-other-request.md` (Code Review type)

---

## 🔧 Refactoring Requests

**Keywords:** "refactor", "improve", "clean up", "restructure", "reorganize", "simplify"

**Examples:**
- "Refactor this service to follow SOLID"
- "Improve the code structure"
- "Clean up this messy function"
- "Restructure the components"
- "Simplify this logic"
- "Reorganize the file structure"

**Template:** `restate-other-request.md` (Refactoring type)

---

## 📚 Explanation Requests

**Keywords:** "explain", "how does", "why", "understand", "what does", "tell me about", "walk me through"

**Examples:**
- "Explain how the payment flow works"
- "How does authentication work here?"
- "Why is this code structured this way?"
- "Help me understand this function"
- "What does this service do?"
- "Tell me about the architecture"
- "Walk me through the checkout process"

**Template:** `restate-other-request.md` (Explanation type)

---

## ⚡ Optimization Requests

**Keywords:** "optimize", "performance", "faster", "slow", "bottleneck", "improve speed", "reduce cost"

**Examples:**
- "Optimize this query, it's too slow"
- "Improve performance of this endpoint"
- "Make this faster"
- "Find the bottleneck in this code"
- "Reduce database queries"
- "Optimize memory usage"

**Template:** `restate-other-request.md` (Optimization type)

---

## 🧪 Testing Requests

**Keywords:** "test", "coverage", "unit test", "integration test", "add tests", "test this"

**Examples:**
- "Add unit tests for this service"
- "Improve test coverage"
- "Write tests for this function"
- "Fix flaky tests"
- "Test the payment flow"
- "Add integration tests"

**Template:** `restate-other-request.md` (Testing type)

---

## 📖 Documentation Requests

**Keywords:** "document", "documentation", "README", "comment", "docs", "write docs"

**Examples:**
- "Document this API"
- "Add comments to this code"
- "Update the README"
- "Write documentation for this service"
- "Create a guide for this feature"

**Template:** `restate-other-request.md` (Documentation type)

---

## 🗑️ Cleanup Requests

**Keywords:** "remove", "delete", "clean up", "dead code", "unused", "deprecated", "tech debt"

**Examples:**
- "Remove unused imports"
- "Delete dead code"
- "Clean up deprecated functions"
- "Remove tech debt"
- "Delete unused dependencies"

**Template:** `restate-other-request.md` (Cleanup type)

---

## 🔄 Migration Requests

**Keywords:** "migrate", "upgrade", "convert", "move", "port", "update version"

**Examples:**
- "Migrate from jQuery to vanilla JS"
- "Upgrade React to version 18"
- "Convert this to TypeScript"
- "Move this to a new service"
- "Port this to Python"

**Template:** `restate-other-request.md` (Migration type)

---

## 🎨 Design/Architecture Requests

**Keywords:** "design", "architecture", "how should", "what's the best", "choose", "decide"

**Examples:**
- "Design a caching system"
- "What's the best architecture for this?"
- "How should I structure this feature?"
- "Choose between these two approaches"
- "Decide on the database schema"

**Template:** `restate-other-request.md` (Design/Architecture type)

---

## 🚀 Quick Tasks (Trivial)

**Keywords:** "typo", "rename", "comment", "format", "indent", "syntax"

**Examples:**
- "Fix typo in variable name"
- "Rename this function"
- "Add a comment here"
- "Format this code"
- "Fix indentation"

**Template:** Usually Quick mode, skip templates, execute directly

---

## Classification Tips

1. **Multiple keywords:** Use the primary intent (what user wants to achieve)
2. **Ambiguous:** Ask clarifying question: "Are you asking me to [interpretation 1] or [interpretation 2]?"
3. **Combined requests:** Break into separate requests or use the most complex one
4. **Context matters:** Same keywords can mean different things in different contexts

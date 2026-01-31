# Example: Bug Fix with RPI

This example shows using RPI for debugging and fixing issues.

## Research Phase

### Objective
Investigate and understand the root cause of users reporting slow API response times.

### Questions to Answer
- [x] What is the core problem to solve?
  - /api/users endpoint taking 5-8 seconds to respond
  - Only affects endpoints returning user lists
- [x] What are the technical constraints?
  - Production database, can't take offline
  - Need to maintain backward compatibility
- [x] What existing solutions or patterns apply?
  - Database indexing
  - Query optimization
  - Caching strategies
- [x] What are the dependencies and prerequisites?
  - Access to production logs
  - Database query profiling tools

### Findings
- Query performs full table scan on users table (500k+ rows)
- No index on frequently queried 'department' column
- N+1 query problem loading user roles

### Key Insights
- Adding composite index will significantly improve performance
- Eager loading relationships eliminates N+1 queries
- Estimated improvement: 5-8s → 100-200ms

---

## Plan Phase

### Goal
Reduce /api/users endpoint response time to under 500ms.

### Approach
1. Add database index on department column
2. Optimize ORM queries with eager loading
3. Verify performance improvement

### Tasks
- [x] Create migration for new index
- [x] Update User query to eager load roles
- [x] Add query performance logging
- [x] Test with production data volume
- [x] Deploy during maintenance window

### Success Criteria
- [ ] Response time < 500ms (currently 5-8s)
- [ ] No increase in database CPU usage
- [ ] All existing tests pass
- [ ] Backward compatible API response

### Risks and Mitigations
| Risk | Mitigation |
|------|------------|
| Index creation locks table | Run migration during low-traffic window |
| Increased disk usage | Monitor and acceptable tradeoff |
| Query regression | Load test before deployment |

---

## Implement Phase

### Implementation Checklist
- [x] Code changes completed
- [x] Tests written and passing
- [x] Documentation updated
- [x] Code reviewed
- [x] Performance verified

### Changes Made
- `migrations/add_department_index.sql` - New index
- `models/User.js` - Eager load roles relationship
- `tests/performance/users.test.js` - Performance tests

### Testing
- [x] Unit tests (all passing)
- [x] Performance test: avg 150ms response time ✓
- [x] Load test: 100 concurrent users, no degradation

### Completion
- [x] 97% improvement in response time (5s → 150ms)
- [x] No security issues introduced
- [x] Deployed successfully

# Example: Adding User Authentication

This example demonstrates using the RPI protocol for a typical feature addition.

## Research Phase (research.md)

### Objective
Understand requirements and constraints for adding user authentication to our API.

### Questions to Answer
- [x] What is the core problem to solve?
  - Need to secure API endpoints with JWT-based authentication
- [x] What are the technical constraints?
  - Must use existing Express.js framework
  - Token expiration: 24 hours
  - Refresh tokens: 30 days
- [x] What existing solutions or patterns apply?
  - passport-jwt middleware
  - bcrypt for password hashing
- [x] What are the dependencies and prerequisites?
  - Database schema for users table
  - Environment variables for JWT secret

### Key Insights
- JWT provides stateless authentication
- Need both access and refresh token flow
- Password requirements: min 8 chars, 1 uppercase, 1 number

### Next Steps
- [x] Move to Plan phase

---

## Plan Phase (plan.md)

### Goal
Implement JWT-based authentication with login, refresh, and protected routes.

### Approach
1. Create User model with password hashing
2. Implement login endpoint generating JWT tokens
3. Add authentication middleware for protected routes
4. Create token refresh endpoint

### Tasks
- [x] Install dependencies (jsonwebtoken, bcrypt, passport-jwt)
- [ ] Create User model with password validation
- [ ] Implement /auth/login endpoint
- [ ] Create JWT verification middleware
- [ ] Add /auth/refresh endpoint
- [ ] Protect existing API routes
- [ ] Write tests for auth flows

### Success Criteria
- [ ] Users can register and login
- [ ] JWT tokens are validated on protected routes
- [ ] Tokens can be refreshed before expiry
- [ ] Passwords are properly hashed
- [ ] 90%+ test coverage for auth code

### Risks and Mitigations
| Risk | Mitigation |
|------|------------|
| JWT secret leaked | Use environment variables, never commit |
| Weak passwords | Implement validation rules |
| Token theft | Short expiration, HTTPS only |

---

## Implement Phase (implement.md)

### Implementation Checklist
- [x] Code changes completed
- [x] Tests written and passing
- [x] Documentation updated
- [x] Code reviewed
- [x] Security scan completed

### Changes Made
- `models/User.js` - User model with bcrypt
- `routes/auth.js` - Login and refresh endpoints
- `middleware/auth.js` - JWT verification
- `routes/api.js` - Protected routes
- `tests/auth.test.js` - Authentication tests

### Testing
- [x] Unit tests for User model (5 tests)
- [x] Integration tests for auth endpoints (8 tests)
- [x] Manual verification with Postman

### Completion
- [x] All success criteria met
- [x] No security vulnerabilities (CodeQL clean)
- [x] Ready for deployment

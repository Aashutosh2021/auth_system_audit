---
name: auth-system-audit
description: "Perform a complete end-to-end audit and, when explicitly authorized, safe remediation of an application's authentication system. Analyze login, signup, sessions, tokens, OAuth, password reset, verification, authorization, routing, database policies, configuration, security, race conditions, UX, and production behavior. Inspect before modifying, trace every issue to root cause, never expose secrets, and verify every applied fix."
---

# Authentication System Audit & Bug Fix

## 1. Objective

Act as a senior:

- Authentication engineer
- Security engineer
- Backend engineer
- Frontend engineer
- QA engineer
- Production-debugging engineer

Perform a complete end-to-end investigation of the application's authentication system.

The objective is not merely to make the login button work.

Determine whether authentication is:

- Functionally correct
- Secure
- Reliable
- Consistent
- Correctly configured
- Resilient to failures and race conditions
- Safe for production
- Correct across frontend/backend/database/auth-provider boundaries

Find meaningful, evidence-backed bugs and trace them to root cause.

When the user explicitly requests fixes, apply the smallest safe remediation, then verify the original issue and related authentication flows.

---

## 2. Investigation-First Rule

Do not immediately modify code.

First:

1. Inspect the complete project.
2. Understand the authentication architecture.
3. Map every authentication flow.
4. Trace the actual code paths.
5. Identify failure points.
6. Determine root causes.
7. Separate symptoms from causes.
8. Build a prioritized fix plan.
9. Only then modify code if the user has authorized fixing.
10. Verify every change.

Never assume the current implementation is correct.

Never stop at the first bug.

---

## 3. Scope

Audit all relevant authentication functionality:

- Login
- Logout
- Signup
- Email verification
- Password reset
- Session creation
- Session persistence
- Session expiration
- Access tokens
- Refresh tokens
- Token rotation
- Cookies
- OAuth/social login
- Account linking
- Protected routes
- Middleware
- Authorization
- Roles
- Permissions
- User/profile synchronization
- Authentication database structures
- RLS/database policies
- Auth-provider configuration
- CORS
- CSP
- Redirect URLs
- HTTPS
- Environment configuration
- Production configuration
- Error handling
- Authentication UX
- Mobile/browser behavior
- Race conditions
- Multi-tab behavior
- Multi-device behavior
- Security boundaries
- Observability and logging

---

# 4. Full System Understanding

Before auditing individual bugs, understand:

## Frontend

Identify:

- Framework
- Entry points
- Login pages
- Signup pages
- Auth components
- Forms
- Validation
- Auth hooks
- Context/providers
- State stores
- API clients
- Token/session consumers
- Route guards
- Redirect logic
- Loading/error states

## Backend

Identify:

- Framework
- API routes
- Controllers
- Middleware
- Server actions
- Authentication services
- Authorization middleware
- Session handling
- Token validation
- Refresh handling
- Error handling

## Database

Identify:

- User tables
- Profile tables
- Auth tables
- Role tables
- Permission tables
- Foreign keys
- Unique constraints
- Triggers
- Functions
- RLS policies
- Service-role access
- Privileged queries

## External authentication

Identify:

- Authentication providers
- OAuth providers
- Email providers
- SMS/OTP providers
- Identity providers
- SDKs
- Redirect/callback configuration

## Configuration

Inspect:

- Environment variables
- Build-time variables
- Runtime variables
- Development config
- Staging config
- Production config
- Domain configuration
- CORS
- Cookies
- HTTPS
- Redirect URLs
- Secrets management

Never reproduce secret values.

---

# 5. Authentication Architecture Map

Build a complete map:

```text
User
 ↓
Login UI
 ↓
Validation
 ↓
Authentication Request
 ↓
Backend / Auth Provider
 ↓
Credential / Identity Validation
 ↓
Database
 ↓
Session / Token Creation
 ↓
Token / Cookie Storage
 ↓
Auth State
 ↓
Application State
 ↓
Protected Route
 ↓
Profile / Permissions
 ↓
Dashboard
```

Also map:

```text
Logout
 → session invalidation
 → token cleanup
 → client auth state
 → redirect
```

```text
Refresh
 → access-token expiry
 → refresh request
 → token rotation
 → storage update
 → pending request retry
```

```text
Signup
 → validation
 → account creation
 → profile creation
 → verification
 → initial session
```

```text
Password Reset
 → request
 → reset token
 → email
 → callback
 → password update
 → session invalidation
```

```text
OAuth
 → provider authorization
 → state/PKCE
 → callback
 → identity validation
 → account linking
 → session creation
 → redirect
```

---

# 6. Authentication Component Inventory

Identify every:

- Login page
- Signup page
- Logout handler
- Auth function
- API endpoint
- Server action
- Auth hook
- Context/provider
- Middleware
- Protected route
- Redirect
- Token handler
- Session handler
- Refresh handler
- OAuth callback
- Password-reset handler
- Verification handler
- User/profile query
- Role/permission query
- Auth-related DB table
- RLS policy
- Trigger/function
- Edge/server function
- Environment variable
- External dependency

For each important component explain:

1. What it does
2. Who calls it
3. What it calls
4. Inputs
5. Outputs
6. Failure behavior
7. Security boundary
8. State it changes
9. Whether it can create inconsistent state

---

# 7. Login Flow Audit

Check:

- Empty email
- Invalid email
- Leading/trailing whitespace
- Email casing
- Empty password
- Wrong password
- Correct credentials
- Unverified user
- Disabled user
- Deleted user
- Locked user
- Rate-limited user
- Network failure
- Timeout
- Server error
- Provider error
- Database error
- Invalid response
- Expired session
- Existing session
- Multiple login attempts
- Double-click submission
- Concurrent login requests
- Slow network
- Offline mode
- Browser refresh during login
- Multiple tabs
- Multiple devices
- Redirect after login
- Redirect loops
- Invalid redirect destination
- Auth state not updating
- UI logged in while backend is logged out
- Backend authenticated while UI is stale
- Session not persisting
- Session disappearing after refresh
- Dashboard failure after successful login
- Profile loading failure
- Permission loading failure

For each real issue identify the root cause, not just the visible symptom.

---

# 8. Session & Token Audit

Trace the entire session lifecycle.

Check:

- Access-token creation
- Access-token expiry
- Refresh-token creation
- Refresh-token expiry
- Refresh-token rotation
- Token revocation
- Token storage
- Cookie configuration
- HttpOnly
- Secure
- SameSite
- Domain
- Path
- Token exposure in URLs
- Token exposure in browser storage
- Token exposure in logs
- Token exposure in errors
- Token exposure in frontend state
- Concurrent refresh
- Refresh race conditions
- Expired tokens
- Invalid tokens
- Revoked tokens
- Logout invalidation
- Multi-device sessions
- Browser restart
- Incognito/private mode
- Cross-tab synchronization
- Stale sessions

Verify whether old sessions can remain valid unexpectedly.

---

# 9. Security Audit

Check for:

- Authentication bypass
- Authorization bypass
- Broken access control
- IDOR
- Privilege escalation
- Session fixation
- Session hijacking
- CSRF
- XSS affecting authentication
- Open redirects
- Token theft
- Credential leakage
- Password leakage
- Sensitive data leakage
- User enumeration
- Brute-force exposure
- Missing rate limiting
- Weak password handling
- Insecure password reset
- Insecure verification
- OAuth account takeover
- Missing OAuth state validation
- Missing/incorrect PKCE
- Redirect URI vulnerabilities
- CORS misconfiguration
- Cookie misconfiguration
- JWT validation problems
- Algorithm confusion/misconfiguration
- Incorrect issuer validation
- Incorrect audience validation
- Expiration validation failures
- Client/server trust-boundary mistakes
- Client-side-only authorization
- Frontend secrets
- Environment variable exposure
- Production debug leakage
- Sensitive authentication logs

### Secret handling

Never output:

- Passwords
- Access tokens
- Refresh tokens
- API keys
- Private keys
- Client secrets
- Session cookies
- Credential values

If a secret is discovered:

1. Identify only the file/location.
2. State that sensitive material was found.
3. Recommend secure rotation/remediation.
4. Do not reproduce the value.

---

# 10. Database & Authentication Data Audit

Inspect:

- User records
- Profile records
- Auth records
- Roles
- Permissions
- Foreign keys
- Unique constraints
- Nullability
- Defaults
- Triggers
- Functions
- RLS
- RLS policies
- Insert policies
- Select policies
- Update policies
- Delete policies
- Service-role access
- Anonymous access
- Privileged queries
- User/profile synchronization
- Orphaned users
- Duplicate profiles
- Profile-creation races
- Missing records
- Deleted records
- Soft-deleted accounts

Determine whether an authenticated user reliably receives the correct profile and permissions.

---

# 11. Signup & Verification Audit

Check:

- Signup validation
- Duplicate accounts
- Email verification
- Verification expiry
- Resend behavior
- Unverified login
- Password creation
- Weak password handling
- Account creation failure
- Partial account creation
- Profile creation failure
- Trigger failure
- Email delivery failure
- Verification redirect
- Already-verified account
- Expired verification links
- Duplicate verification requests

---

# 12. Password Reset Audit

Check:

- Forgot-password request
- Reset email
- Reset token
- Token expiration
- Token reuse
- Token invalidation
- Password update
- Session invalidation
- Existing sessions
- Enumeration protection
- Expired links
- Multiple reset requests
- Reset races
- Redirect handling

---

# 13. OAuth / Social Login Audit

If OAuth exists, inspect every configured provider.

Audit:

- Initialization
- State
- PKCE
- Callback validation
- Redirect URI
- Account linking
- Existing account collision
- Email collision
- Provider identity collision
- Provider email verification
- Callback failures
- Popup failures
- Mobile browser behavior
- In-app browser behavior
- User cancellation
- Retry behavior
- Multiple accounts
- Logout behavior

Never assume provider configuration is correct merely because the OAuth UI appears.

---

# 14. Frontend / UX Audit

Inspect:

- Loading state
- Disabled state
- Double submission
- Validation
- Error messages
- Error persistence
- Password visibility
- Form reset
- Autofill
- Password-manager compatibility
- Mobile keyboard behavior
- Mobile viewport
- Accessibility
- Keyboard navigation
- Screen readers
- Focus management
- Redirects
- Stale auth state
- Flash of protected content
- Flash of login page
- Logout state
- Race conditions

Verify that user-visible behavior matches backend authentication state.

---

# 15. Routing & Middleware Audit

Trace every protected route.

Check:

- Middleware
- Server-side guards
- Client-side guards
- Nested routes
- Dynamic routes
- API routes
- Admin routes
- Unauthorized access
- Redirect loops
- Return URLs
- Deep links
- Direct protected URLs
- Refreshing protected pages
- Browser back/forward
- Logged-out access
- Logged-in access
- Wrong-role access

Security must not depend solely on frontend route protection.

---

# 16. Error Handling Audit

For each authentication error identify:

- Exact source
- Trigger
- User-visible behavior
- Internal behavior
- Handling
- Logging
- Message correctness
- Security leakage
- Recovery path

Check:

- 400
- 401
- 403
- 404
- 409
- 422
- 429
- 500
- 502
- 503
- Network failures
- Timeouts
- Provider errors
- Database errors
- Unexpected exceptions

Avoid both extremes:

- Do not leak sensitive internal details.
- Do not hide recoverable failures behind useless generic errors.

---

# 17. Production Audit

Inspect:

- Production environment variables
- Missing variables
- Wrong variables
- Localhost references
- Development URLs
- Production callback URLs
- Production domains
- HTTPS
- CORS
- Cookies
- CDN/proxy behavior
- Reverse proxy behavior
- Serverless cold starts
- Timeouts
- Provider limits
- Database limits
- Logging
- Monitoring
- Error tracking
- Observability
- Deployment configuration
- Build-time vs runtime variables
- Secret management
- Production-only assumptions
- Browser compatibility
- Mobile compatibility

Search the entire repository for development-only assumptions.

---

# 18. Race Conditions & Edge Cases

Analyze:

- Concurrent login requests
- Login + logout
- Login + refresh
- Refresh + API request
- Multiple tabs
- Multiple devices
- Token expiry during request
- Refresh during authentication
- Browser close
- Network disconnect
- Network reconnect
- Slow provider
- Duplicate clicks
- Rapid navigation
- Session expiry while active
- Profile request before session initialization
- Profile request after logout
- Refresh-token rotation during concurrent requests

Explain ordering and state transitions where a race exists.

---

# 19. Test Matrix

Build a test matrix covering:

## Valid

- Login
- Signup
- Verification
- Password reset
- Logout

## Invalid

- Invalid email
- Invalid password
- Missing fields
- Expired token
- Invalid token
- Invalid verification
- Invalid reset token
- Unauthorized user
- Forbidden user

## Environment

- Development
- Staging
- Production
- Mobile
- Desktop
- Slow network
- Offline
- Multiple tabs

## Security

- Brute force
- Rate limiting
- Session theft
- CSRF
- XSS
- IDOR
- Privilege escalation
- Open redirect
- Token leakage

Clearly distinguish:

- Tested
- Confirmed
- Unverified
- Requires manual verification

Do not claim runtime tests were performed if they were not.

---

# 20. Code-Level Audit

Inspect relevant authentication code deeply for:

- Dead authentication code
- Duplicate auth logic
- Incorrect async/await
- Missing await
- Unhandled promises
- Incorrect try/catch
- Incorrect error propagation
- Null/undefined problems
- Type mismatches
- Incorrect state updates
- Stale closures
- Incorrect hook dependencies
- Memory leaks
- Infinite loops
- Incorrect redirects
- Wrong environment variables
- Incorrect imports
- Dependency issues
- Deprecated APIs
- Incorrect SDK usage
- Auth-provider integration mistakes
- Server/client boundary errors

---

# 21. Root-Cause Chain

Never stop at the first symptom.

Example:

```text
Login fails
 ↓
Session is not created
 ↓
Profile query receives no authenticated context
 ↓
Profile lookup fails
 ↓
Middleware redirects
 ↓
Login page reappears
 ↓
User sees "login failed"
```

Report the full causal chain when evidence supports it.

Separate:

- Primary root cause
- Secondary symptoms
- Cascading effects
- Independent issues

---

# 22. Finding Format

For every finding provide:

```text
Bug ID:
Category:
Severity:
Status:
File:
Component:
Exact Location:
Problem:
Root Cause:
Trigger:
Impact:
Expected Behavior:
Actual Behavior:
Reproduction:
Related Components:
Security Impact:
Recommended Fix:
Regression Risk:
Verification/Test:
Evidence:
Confidence:
```

### Status values

Use factual statuses:

- Confirmed working
- Confirmed broken
- Fixed
- Requires configuration
- Requires manual verification
- Unable to verify

Never claim `Fixed` unless the change was actually applied and verified.

---

# 23. Severity

Use:

### CRITICAL

Examples:

- Authentication bypass
- Account takeover
- Severe authorization bypass
- Complete production authentication failure

### HIGH

Examples:

- Major login failure
- Session vulnerability
- Authorization vulnerability
- Serious production issue

### MEDIUM

Examples:

- Important functional bug
- Significant edge-case failure
- Meaningful UX/auth-state inconsistency

### LOW

Examples:

- Minor UX issue
- Maintainability issue
- Low-impact edge case

Do not inflate severity.

---

# 24. Fixing Protocol

Only perform modifications when the user has explicitly authorized fixing.

Before editing:

1. Identify the root cause.
2. Identify affected files.
3. Identify dependencies and side effects.
4. Choose the smallest safe change.
5. Preserve existing security controls.

Never "fix" authentication by:

- Disabling authentication
- Disabling authorization
- Disabling RLS
- Disabling CORS protections
- Disabling HTTPS
- Removing validation
- Hardcoding credentials
- Trusting client-provided roles
- Bypassing token validation
- Removing security middleware
- Exposing secrets
- Making insecure redirects

After a change:

1. Re-run the original failing flow.
2. Verify the root cause is addressed.
3. Test login.
4. Test logout.
5. Test refresh.
6. Test protected routes.
7. Test invalid credentials.
8. Test expired sessions.
9. Test relevant security controls.
10. Test related flows.
11. Check regressions.
12. Report exactly what was changed.

---

# 25. Regression Checklist

After remediation, verify as applicable:

- [ ] Valid login
- [ ] Invalid login
- [ ] Logout
- [ ] Session persistence
- [ ] Session expiration
- [ ] Token refresh
- [ ] Protected routes
- [ ] Wrong-role access
- [ ] Signup
- [ ] Verification
- [ ] Password reset
- [ ] OAuth
- [ ] Multiple tabs
- [ ] Network failure
- [ ] Slow network
- [ ] Refresh/reload
- [ ] Mobile behavior
- [ ] Security controls
- [ ] Error handling
- [ ] Production configuration

---

# 26. Final Audit Report

Produce:

## A. Executive Summary

- Authentication architecture
- Current state
- Main failure points
- Major risks
- Verification limitations

## B. Authentication Architecture

Show complete flow diagrams.

## C. Findings

Detailed evidence-backed findings.

## D. Security Findings

Separate security vulnerabilities from functional bugs.

## E. Production Findings

Production-specific issues.

## F. Edge Cases

Relevant timing and lifecycle problems.

## G. Test Matrix

Tested vs unverified.

## H. Fix Plan

Order remediation by dependency and severity.

## I. Regression Checklist

What must pass after remediation.

## J. Final Status

Use factual statuses only.

---

# 27. No-Hallucination Rules

Never:

- Invent a bug
- Invent a configuration value
- Invent a route
- Invent an endpoint
- Invent runtime behavior
- Invent test results
- Invent line numbers
- Claim a fix was applied when it was not
- Claim a security vulnerability without evidence

If the repository is insufficient:

> **Unable to verify from the available code/configuration.**

Explain exactly what evidence is missing.

---

# 28. Final Objective

The job is not simply:

> "Make login work."

The job is:

> Determine whether the entire authentication system is functionally correct, secure, reliable, consistent, and production-ready; identify every meaningful issue that can be substantiated; trace each issue to its root cause; and, when explicitly authorized, apply the smallest safe remediation and verify the result through regression testing.

Authentication is a security-critical system.

Inspect first.
Trace deeply.
Fix carefully.
Verify everything.
Never guess.

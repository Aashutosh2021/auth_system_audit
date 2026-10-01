# Authentication Audit Examples

## Example 1 — Root-Cause Login Failure

```text
Bug ID: AUTH-001
Category: Login
Severity: HIGH
Status: Confirmed broken

Problem:
Valid credentials are accepted, but the application returns to the login page.

Root Cause:
The authentication request creates a session, but the client does not
persist the updated session state before the protected-route check runs.

Trigger:
Login on a fresh browser session.

Impact:
Users cannot reach the dashboard despite valid credentials.

Recommended Fix:
Synchronize session initialization with the protected-route guard.

Verification:
Login → session exists → protected route loads → refresh → session persists.

Confidence: High
```

---

## Example 2 — Configuration Issue

```text
Bug ID: AUTH-002
Category: Production Configuration
Severity: HIGH
Status: Requires configuration

Problem:
OAuth callback succeeds in development but fails in production.

Evidence:
Production callback URL differs from the configured provider redirect URI.

Recommended Fix:
Align the production callback configuration with the deployed domain.

Verification:
Perform the OAuth flow from the production domain.

Confidence: High
```

---

## Example 3 — Potential Race

```text
Bug ID: AUTH-003
Category: Session Refresh
Severity: MEDIUM
Status: Requires manual verification

Problem:
Multiple API requests can attempt token refresh simultaneously.

Evidence:
The client has no visible refresh-request coordination.

Impact:
Concurrent refresh requests may race during token rotation.

Missing Evidence:
Runtime provider behavior and refresh-token rotation policy.

Confidence: Medium
```

---

## Example 4 — Secret Exposure

```text
Bug ID: AUTH-004
Category: Security
Severity: CRITICAL
Status: Confirmed broken

Problem:
A credential is present in a client-exposed configuration path.

Evidence:
Sensitive configuration is bundled into frontend code.

Secret:
NOT REPRODUCED.

Recommended Fix:
Remove the credential from client-exposed configuration,
rotate the affected credential, and move secret-dependent
operations to a trusted server boundary.
```

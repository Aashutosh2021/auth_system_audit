# Authentication Audit Methodology

## Phase 1 — Architecture Discovery

Map:

```text
Frontend
 ↓
Auth Client
 ↓
Backend/Auth Provider
 ↓
Database
 ↓
Session/Token
 ↓
Application State
 ↓
Protected Routes
```

Also map signup, logout, refresh, verification, password reset and OAuth.

---

## Phase 2 — Component Inventory

Locate:

- Auth pages
- Auth components
- Hooks/providers
- Auth APIs
- Middleware
- Session handlers
- Token handlers
- Database structures
- Policies
- Triggers
- OAuth callbacks
- Configuration

---

## Phase 3 — Lifecycle Tracing

For each flow trace:

```text
Input
 ↓
Validation
 ↓
Request
 ↓
Authentication
 ↓
Persistence
 ↓
Session
 ↓
State
 ↓
Routing
 ↓
Profile
 ↓
Permissions
```

---

## Phase 4 — Failure Analysis

Inspect:

- Invalid credentials
- Network failure
- Timeout
- Provider failure
- Database failure
- Expiration
- Cancellation
- Concurrent requests
- Duplicate requests
- Partial failures

---

## Phase 5 — Security Analysis

Inspect the trust boundary:

```text
Untrusted Client
       ↓
Validation
       ↓
Server/Auth Provider
       ↓
Authorization
       ↓
Database
```

Never assume client-side state is authoritative for security decisions.

---

## Phase 6 — Root Cause

Separate:

```text
Symptom
 ↓
Immediate Failure
 ↓
Underlying Cause
 ↓
Configuration/Architecture Cause
```

Report the deepest evidence-backed cause available.

---

## Phase 7 — Remediation

Only after investigation and explicit authorization:

1. Choose the smallest safe change.
2. Preserve security controls.
3. Apply change.
4. Test original failure.
5. Test related flows.
6. Run regression checks.
7. Report exact result.

---

## Phase 8 — Verification

Never call a bug fixed merely because code was changed.

A fix is:

```text
Applied
  +
Original failure reproduced before fix
  +
Original failure no longer occurs
  +
Related authentication flows pass
```

If runtime verification is unavailable, use:

**Requires manual verification**

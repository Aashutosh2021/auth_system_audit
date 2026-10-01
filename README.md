# 🔐 Authentication System Audit

A deep, evidence-based AI coding-agent skill for auditing and fixing application authentication systems.

Designed for:

- Claude Code
- Google Antigravity
- Other AI coding agents that support `SKILL.md`

The skill covers the complete authentication lifecycle rather than only the visible login page.

> **Inspect first → Find root cause → Fix only when authorized → Verify**

---

## What It Audits

### Authentication

- Login
- Logout
- Signup
- Email verification
- Password reset
- Session lifecycle
- Access tokens
- Refresh tokens
- OAuth/social login

### Security

- Authentication bypass
- Authorization bypass
- IDOR
- Privilege escalation
- Session fixation
- Session hijacking
- CSRF
- XSS
- Open redirects
- Token leakage
- Credential leakage
- JWT validation
- Cookie security
- CORS
- Client/server trust boundaries
- Secrets exposure

### Database

- User/profile synchronization
- Roles
- Permissions
- RLS
- Policies
- Triggers
- Functions
- Constraints
- Race conditions
- Orphaned records

### Frontend

- Auth state
- Loading states
- Double submission
- Validation
- Redirects
- Protected routes
- Accessibility
- Mobile behavior
- Stale state
- UI/backend inconsistencies

### Production

- Environment variables
- Production URLs
- Callback URLs
- HTTPS
- Cookies
- CORS
- Proxies/CDNs
- Serverless behavior
- Rate limits
- Logging
- Monitoring
- Deployment configuration

### Edge Cases

- Concurrent login
- Login/logout races
- Refresh races
- Multiple tabs
- Multiple devices
- Expired sessions
- Network failures
- Slow providers
- Rapid navigation
- Profile/session races

---

## Core Principle

The skill does not stop at the first visible error.

For example:

```text
Login Error
    ↓
Session Creation Failure
    ↓
Profile Query Failure
    ↓
Middleware Redirect
    ↓
Redirect Loop
    ↓
User Sees "Login Failed"
```

The goal is to identify the **root cause and complete failure chain**, not merely the first symptom.

---

## Investigation First

The agent must first understand:

```text
Frontend
   ↓
Auth Request
   ↓
Backend / Auth Provider
   ↓
Database
   ↓
Session / Token
   ↓
Storage
   ↓
Auth State
   ↓
Protected Route
   ↓
Profile
   ↓
Permissions
   ↓
Application
```

The same depth is applied to:

```text
Signup
Verification
Logout
Refresh
Password Reset
OAuth
Session Expiration
```

---

## Fixing Behavior

Unlike a purely read-only audit skill, this skill supports remediation **when the user explicitly asks the agent to fix the discovered problems**.

The workflow is:

```text
Inspect
  ↓
Understand
  ↓
Audit
  ↓
Find Root Cause
  ↓
Plan Minimal Fix
  ↓
Apply Fix
  ↓
Test Original Failure
  ↓
Regression Test
  ↓
Security Verification
```

If the user only asks for an audit, do not modify the project.

---

## Security Rule

Never fix authentication by weakening security.

The agent must never use shortcuts such as:

- Disabling authentication
- Disabling authorization
- Disabling RLS
- Removing validation
- Disabling HTTPS
- Weakening CORS protections
- Trusting frontend roles
- Bypassing token validation
- Hardcoding credentials
- Exposing secrets
- Removing security middleware

---

## Finding Format

Every issue uses:

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

---

## Severity

| Severity | Meaning |
|---|---|
| **CRITICAL** | Authentication bypass, account takeover, severe authorization issue, complete production auth failure |
| **HIGH** | Major login/session/security/production issue |
| **MEDIUM** | Important functional or edge-case issue |
| **LOW** | Minor UX, maintainability or low-impact issue |

Severity must be evidence-based.

---

## Status

Only use factual statuses:

- Confirmed working
- Confirmed broken
- Fixed
- Requires configuration
- Requires manual verification
- Unable to verify

`Fixed` means the change was actually made and verified.

---

## Installation

### Claude Code — Project Skill

From the project root:

```bash
mkdir -p .claude/skills/auth-system-audit

curl -L https://raw.githubusercontent.com/Aashutosh2021/auth-system-audit/main/SKILL.md \
  -o .claude/skills/auth-system-audit/SKILL.md
```

Result:

```text
your-project/
└── .claude/
    └── skills/
        └── auth-system-audit/
            └── SKILL.md
```

Then start Claude Code:

```bash
claude
```

Invoke:

```text
/auth-system-audit
```

Or ask naturally:

```text
Audit the complete authentication system and find the root cause of the login issue.
```

---

### Claude Code — Global Skill

```bash
mkdir -p ~/.claude/skills/auth-system-audit

curl -L https://raw.githubusercontent.com/Aashutosh2021/auth-system-audit/main/SKILL.md \
  -o ~/.claude/skills/auth-system-audit/SKILL.md
```

---

### Google Antigravity — Workspace

```bash
mkdir -p .agents/skills/auth-system-audit

curl -L https://raw.githubusercontent.com/Aashutosh2021/auth-system-audit/main/SKILL.md \
  -o .agents/skills/auth-system-audit/SKILL.md
```

Then invoke:

```text
/auth-system-audit
```

---

### Google Antigravity — Global

```bash
mkdir -p ~/.gemini/config/skills/auth-system-audit

curl -L https://raw.githubusercontent.com/Aashutosh2021/auth-system-audit/main/SKILL.md \
  -o ~/.gemini/config/skills/auth-system-audit/SKILL.md
```

---

## Example Prompts

### Full authentication audit

```text
Run /auth-system-audit.

First understand the complete authentication architecture.

Audit login, signup, logout, sessions, tokens,
protected routes, database policies, OAuth,
password reset, configuration, security and race conditions.

Do not modify anything yet.
Give me the complete root-cause report first.
```

### Audit + fix

```text
Run /auth-system-audit.

First perform the complete audit.

After identifying the root causes, fix the confirmed
authentication bugs using the smallest safe changes.

Then test the original login failure and run the
authentication regression checklist.

Do not weaken any security control.
```

### Login-specific investigation

```text
My login is failing.

Run /auth-system-audit and trace the complete flow
from the login UI to the auth provider/database/session,
then identify the exact root cause.

Do not stop at the first error.
```

### Production issue

```text
Audit the authentication system specifically for
production-only failures.

Check environment variables, domains, HTTPS,
cookies, CORS, callback URLs, proxies, deployment
configuration and auth-provider settings.
```

### Security audit

```text
Run /auth-system-audit as a security-focused review.

Check authentication bypass, authorization,
session security, JWT validation, cookies, CSRF,
XSS, OAuth, IDOR, privilege escalation,
rate limiting and secret exposure.

Do not expose any secrets found.
```

---

## Repository Structure

```text
auth-system-audit/
│
├── SKILL.md
├── README.md
├── LICENSE
├── .gitignore
│
├── docs/
│   ├── methodology.md
│   ├── severity-and-status.md
│   └── examples.md
│
└── examples/
    └── sample-audit.md
```

---

## Relation to Your Other Audit Skills

This skill can be part of a broader software audit toolkit:

```text
dead-code-audit
       │
       ├── unused / legacy code
       │
resource-leak-audit
       │
       ├── resource lifecycle
       │
auth-system-audit
       │
       └── authentication / security / login
```

Each skill focuses on a different failure class.

---

## Important Limitations

Some authentication behavior cannot be conclusively verified from repository source alone.

Examples:

- External identity-provider configuration
- Production environment values
- Reverse-proxy behavior
- DNS/domain configuration
- Provider-side policies
- Native SDK internals
- Infrastructure configuration
- Production-only runtime behavior

These must be marked:

**Unable to verify**

The agent must explain what additional evidence is required.

---

## Secret Safety

If secrets are encountered:

- Never reproduce them.
- Never put them in the final report.
- Identify only the location/type.
- Recommend rotation/remediation.

---

## License

MIT License.

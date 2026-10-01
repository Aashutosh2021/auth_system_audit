# Severity and Status Guide

## Severity

### CRITICAL

- Authentication bypass
- Account takeover
- Severe authorization bypass
- Complete production authentication outage

### HIGH

- Major login failure
- Session vulnerability
- Serious authorization problem
- Production-wide authentication issue

### MEDIUM

- Important functional failure
- Significant edge case
- Authentication-state inconsistency

### LOW

- Minor UX problem
- Maintainability problem
- Low-impact edge case

Do not inflate severity.

---

# Status

## Confirmed working

The behavior was actually verified.

## Confirmed broken

The issue was reproduced or directly established from evidence.

## Fixed

The change was applied and verification confirmed the issue is resolved.

## Requires configuration

Code may be correct but environment/provider/deployment configuration must be changed.

## Requires manual verification

Source analysis is insufficient to prove runtime behavior.

## Unable to verify

Required evidence is unavailable.

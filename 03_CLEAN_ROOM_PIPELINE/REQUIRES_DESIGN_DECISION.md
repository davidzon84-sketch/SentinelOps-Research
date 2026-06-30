# REQUIRES_DESIGN_DECISION â€” Blocking State Reference

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Clean-Room Pipeline â€” Design Decision Gate  
**Date:** 2026-06-30  
**Current status:** **ACTIVE** â€” whitelist pending; OQ-1 OPEN

---

## 1. Definition

`REQUIRES_DESIGN_DECISION` is a **first-class blocking state** in the CEB state machine. It indicates that automated or operational progress must halt because a required human design input cannot be derived from policy, tooling, or inference.

This state is **not an error**. It is the mechanism by which the boundary model prevents silent scope expansion.

---

## 2. Entry Triggers

| Trigger | Description | Current |
|---------|-------------|---------|
| **Whitelist absent/pending** | File-level enumeration not finalized | **ACTIVE** |
| **Scope ambiguous** | Option A vs Option B unresolved | Resolved (Option A) |
| **Identity conflict** | Conflicting version or product naming | **ACTIVE** (OQ-1) |
| **Build inputs undefined** | Option B selected but no compile source list | N/A (Option A) |
| **Binary pipeline undefined** | Compile expected but BS-4 not documented | N/A (Option A) |
| **Plugin policy unset** | Partner requires plugins but no sandbox audit | Possible (OQ-5) |

---

## 3. Valid Behaviors While Blocked

| Behavior | Valid? |
|----------|--------|
| Remain blocked indefinitely | **Yes** |
| Execute recursive repo copy to "unblock" | **No â€” prohibited** |
| Infer compile inputs from proprietary trust-layer implementation/ tree | **No â€” prohibited** |
| Ship legacy blocked artifact as workaround | **No — prohibited** |
| Document research-only package (Option A) | **Yes â€” permitted** |
| Execute Phase 1 clean-room preparation | **Yes â€” executed 2026-06-30** |
| Request SRO decision on open questions | **Yes â€” required** |

---

## 4. Exit Requirements

Exit requires **documented human decision** with:

1. Named authority (SRO or IP Owner)
2. UTC timestamp
3. Decision text recorded in governance artifact
4. Finalized whitelist with per-file enumeration
5. OQ-1 closed (identity alignment)

---

## 5. Phase 1 Case Study (2026-06-30)

### 5.1 Initial Blocking Condition

Phase 1 exploration found:
- No pre-compiled evaluation binaries in repository
- Whitelist not yet finalized for full documental assembly
- OQ-1 (identity) unresolved

Program entered `REQUIRES_DESIGN_DECISION`.

### 5.2 Partial Resolution

| Decision | Authority | Date | Status |
|----------|-----------|------|--------|
| Option A â€” Pure Documentation/Research Review | David Baldizon (SRO) | 2026-06-30 | OQ-6 **CLOSED** |
| Phase 1 clean-room preparation | Security Release Engineer | 2026-06-30 | **EXECUTED** |
| 26-route whitelist proposed | Security Release Architect | 2026-06-30 | **PENDING** SRO confirmation |
| OQ-1 identity supersession | â€” | â€” | **OPEN** |

### 5.3 Current Posture

```
STATE:                    REQUIRES_DESIGN_DECISION (ACTIVE)
CONCURRENT:               AUTHORIZATION_READY_FOR_BUILD
PHASE_1:                  EXECUTED
WHITELIST:                PENDING
NON_EXECUTION:            VALID SECURITY STATE
```

Phase 1 execution **does not** exit `REQUIRES_DESIGN_DECISION`. Whitelist finalization and OQ-1 closure are required.

---

## 6. Whitelist Absence as Valid Block

Before whitelist finalization, **the absence of an authoritative file enumeration is the correct blocking reason**. Operators must not copy development repository content beyond Phase 1 contractual skeleton without explicit per-file authorization.

**Key principle:** Pending whitelist â†’ do not expand assembly scope. Do not default to full tree or recursive subtree.

---

## 7. Relationship to Open Questions

| OQ | Can block REQUIRES_DESIGN_DECISION? | Status |
|----|-------------------------------------|--------|
| OQ-1 (identity) | Yes | **OPEN** |
| OQ-2 (SRO) | Yes | **CLOSED** |
| OQ-6 (scope) | Yes | **CLOSED** |
| OQ-3 (IP) | Blocks Option B only | OPEN |
| OQ-4 (signature) | No | OPEN |
| OQ-5 (plugins) | Can block if partner mandates plugins | OPEN |

---

## 8. Semantic Distinction

| State | Meaning |
|-------|---------|
| `REQUIRES_DESIGN_DECISION` | Human design input needed **before** full assembly progress |
| `BLOCKED_PENDING_REMEDIATION` | Control failure **after** progress attempted |
| `AUTHORIZATION_READY_FOR_BUILD` | Authorization model complete; does not imply whitelist finalized |

---

## 9. Non-Execution Principle

Remaining in `REQUIRES_DESIGN_DECISION` after Phase 1 execution is **preferable** to:

- Executing unauthorized full assembly
- Exposing productive source code
- Delivering non-whitelisted content
- Closing OQ-1 by inference

**Non-execution is a valid terminal posture** until design gates close.

---

## 10. Current Status

```
REQUIRES_DESIGN_DECISION: ACTIVE
WHITELIST:                PENDING (26 routes proposed, not finalized)
OQ-1:                     OPEN
PHASE_1:                  EXECUTED
V2_REVIEW:                COMPLETED
DELIVERY:                 NOT AUTHORIZED
```

---

_REQUIRES_DESIGN_DECISION Reference â€” CEB v1 â€” 2026-06-30_

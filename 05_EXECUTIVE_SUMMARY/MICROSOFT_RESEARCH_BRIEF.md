# Microsoft Research Brief â€” CEB v1 Governance Architecture

**Audience:** Microsoft Research â€” systems, security, and programming languages groups  
**Classification:** Internal-style research brief (partner evaluation documentation)  
**Date:** 2026-06-30  
**Author:** David Baldizon

---

## Executive Summary

SentriOps CEB v1 externalizes defensive operational security **research** under a governance-first clean-room model. The contribution is architectural: a reproducible pattern for sharing falsifiable trust-continuity research without transferring productive implementation or assuming build artifact availability.

---

## Problem Framing

Autonomous systems increasingly require evidential grounding for trust decisions beyond functional correctness. External research review traditionally assumes code availability or reproducible builds. CEB v1 addresses the case where **IP boundaries prohibit source transfer** yet governance and research framing must remain auditable.

---

## Technical Contribution

1. **Controlled Evaluation Boundary (CEB)** â€” file-level whitelist as sole ingress primitive
2. **Three-layer integrity model** â€” hash (integrity), signature (provenance, optional), human approval (authorization)
3. **Open Question gates** â€” explicit human decision points that block state transitions
4. **Non-execution as valid state** â€” deliberate abstention from build/delivery when preconditions unmet

---

## Governance Reduces Execution Risk

| Risk | CEB mitigation |
|------|----------------|
| Accidental source leakage | Whitelist + denylist; no recursive copy |
| Unauthorized delivery | SRO sign-off required; gate â‰  approval |
| Scope creep | REQUIRES_DESIGN_DECISION blocking state |
| Supply-chain ambiguity | SHA256 manifest + BUILD_RECORD trace chain |
| Legacy artifact reuse | v1.22.0 explicitly blocked; new identity line |

Microsoft Research relevance: parallels trustworthy computing release governance, SLSA provenance separation, and fail-closed authorization in autonomous agent systems â€” applied to research externalization under IP constraints.

---

## Build Integrity Posture

- Phase 1 **executed**: contractual skeleton (6 files) in isolated clean-room
- Full 26-route assembly **not executed** â€” whitelist pending; valid non-execution posture
- Zero compilation; zero binaries for v1.0 Option A
- Adversarial Audit V2 **review completed** (2026-06-30)
- Manifest generation and automated gate: pending whitelist finalization

Integrity verification is **independent of build execution**: evaluators can verify governance documentation without trusting the author's development environment.

---

## Supply-Chain Protection Properties

1. **Provenance separation** â€” clean-room workspace outside dev repo
2. **Explicit enumeration** â€” 26 proposed routes; absence is valid block
3. **Human gate chain** â€” OQ â†’ design â†’ assembly â†’ manifest â†’ gate â†’ audit â†’ approval
4. **No binary assumption** â€” Option A avoids shipping unverified executables
5. **Retroactive hash prohibition** â€” new Release ID on remediation

---

## Current State (Honest Disclosure)

| Field | Value |
|-------|-------|
| CEB v1 cycle | **CLOSED** |
| Operational states | `AUTHORIZATION_READY_FOR_BUILD` + `REQUIRES_DESIGN_DECISION` |
| Phase 1 | **EXECUTED** |
| V2 review | **COMPLETED** |
| Delivery | Not authorized |
| Open gates | OQ-1, OQ-3, OQ-4, OQ-5 |
| SRO | David Baldizon |

---

## Limitations for Reviewers

- No productive code in package
- STF empirical evidence (300 tests) exists in separate PR #43 scope
- extended governance evaluation model (theoretical) theoretical; not validated by PR #43 closure
- Does not claim regulatory certification or absolute security

---

## Suggested Review Focus

1. Is the state machine complete for research externalization?
2. Are OQ gates sufficient to prevent silent scope expansion?
3. Does non-execution semantics avoid false readiness signals?
4. How does CEB compare to confidential computing and SLSA in complementary (not competitive) framing?

---

_Microsoft Research Brief â€” CEB v1 â€” 2026-06-30_

# Sovereign Trust Fabric and the Controlled Evaluation Boundary: A Governance-First Model for External Research Review

**Document type:** Research Paper (CEB v1 Package)  
**Version:** partner-eval-1.0.0  
**Date:** 2026-06-30  
**Author:** David Baldizon  
**Classification:** Partner Evaluation — Research Framework

---

## Abstract

See [`ABSTRACT.md`](./ABSTRACT.md).

---

## 1. Introduction

See [`INTRODUCTION.md`](./INTRODUCTION.md).

---

## 2. Problem Statement

Autonomous systems increasingly operate under adversarial degradation of initial trust assumptions. Conventional verification—functional testing, perimeter controls, artifact signing—addresses operational correctness but provides insufficient epistemic grounding when trust in the verification mechanism itself is challenged.

SentinelOps research proposes the **Sovereign Trust Fabric (STF)**, a framework in which autonomous systems evaluate not only whether decisions are operationally correct, but whether the **evidential conditions** required to justify trust in those decisions remain satisfied under degradation.

The **Controlled Evaluation Boundary (CEB) v1** is the operational envelope through which this research may be shared with external evaluators without transferring productive source code, unpublished research, or operational infrastructure.

---

## 3. The CEB Model

### 3.1 Boundary Definition

CEB v1 defines a hard separation between:

| Side | Contents |
|------|----------|
| **Private (development)** | `backend/`, `frontend/`, `trust-fabric/` source; unpublished research; operational secrets |
| **Evaluation (partner-facing)** | Curated documentation, declarative JSON schemas, contractual placeholders, integrity manifests |

The boundary is enforced by **explicit whitelist enumeration**, not by directory-level trust or recursive copy.

### 3.2 Release Identity

- **Human name:** SentriOps Partner Evaluation v1.0
- **Semantic version:** `partner-eval-1.0.0`
- **Scope (v1.0):** Option A — Pure Documentation/Research Review (26 authorized origin paths)

### 3.3 Three-Layer Integrity Model

1. **Integrity (SHA-256):** Detects post-packaging modification.
2. **Provenance (optional signature):** Attributes manifest generation to a cryptographic identity.
3. **Authorization (human):** Records that an authorized Security Release Owner permitted delivery.

These layers are **orthogonal**. Hash match does not imply approval; approval does not substitute for hash verification.

---

## 4. Clean-Room Execution Model

External evaluation artifacts are assembled in an **isolated clean-room workspace** physically separated from the development repository. Phase 1.1 (2026-06-30) demonstrated documental assembly of 26 whitelisted files with zero compilation, zero binaries, and zero modification of productive source trees.

**Recursive repository copy is forbidden** because:

1. It cannot guarantee denylist compliance at file granularity.
2. It exposes IP beyond the evaluated research surface.
3. It conflates development provenance with evaluation provenance.
4. It bypasses the `REQUIRES_DESIGN_DECISION` gate that forces explicit scope declaration.

**Absence from the whitelist is a valid block**, not a defect to override. When no binary pipeline is defined, the governance-correct action is Option A documental delivery—not inference of compile inputs from the development tree.

---

## 5. Open Question (OQ) Gates

Human decision gates (OQ-1 through OQ-6) control state transitions. As of 2026-06-30:

- **Closed:** OQ-1 (identity), OQ-2 (SRO), OQ-6 (Option A scope)
- **Open:** OQ-3 (IP co-approval), OQ-4 (signature), OQ-5 (plugin acceptance)

Unresolved OQ gates permit the program to remain in non-delivery states without failure. See [`../00_GOVERNANCE_MODEL/OQ_GATES_MODEL.md`](../00_GOVERNANCE_MODEL/OQ_GATES_MODEL.md).

---

## 6. State Machine and Governance-First Execution

The CEB state machine prioritizes **governance completeness over execution velocity**:

```
DESIGN_READY_FOR_BUILD → AUTHORIZATION_READY_FOR_BUILD
  → READY_FOR_PACKAGE_ASSEMBLY → BUILD_VALIDATED
  → READY_FOR_EXTERNAL_REVIEW → APPROVED_FOR_DELIVERY
```

Blocking states (`REQUIRES_DESIGN_DECISION`, `BLOCKED_PENDING_REMEDIATION`) are first-class citizens. As of 2026-06-30, the program occupies concurrent `AUTHORIZATION_READY_FOR_BUILD` and `REQUIRES_DESIGN_DECISION` following Phase 1 execution with whitelist pending.

**Governance-first execution** means: no build, no ZIP, and no delivery occur until the corresponding gate evidence exists. Automated tooling (release gate, adversarial audit) is necessary but not sufficient.

See [`../00_GOVERNANCE_MODEL/STATE_MACHINE.md`](../00_GOVERNANCE_MODEL/STATE_MACHINE.md).

---

## 7. Research Framework (STF Summary)

The Sovereign Trust Fabric proposes:

- **Trust Decision Unit (TDU):** Atomic unit pairing a critical decision with minimum evidence package.
- **`DecisionTrust(D,t)`:** Composition of eight falsifiable predicates with fail-closed semantics.
- **SARP protocol:** Sovereign Adversary Resilience Protocol — meta-audit layer for trust continuity.
- **SARP-OMEGA v1.0:** Theoretical extension (frozen 2026-06-29); not validated by PR #43 empirical scope.

Empirical evidence (PR #43, SHA `50969f5`, 300 pytest) covers sandbox-modeled vectors. SARP-OMEGA theoretical work (340 additional pytest locally) is documented as exploratory and **not** included in formal closure claims.

See [`ARCHITECTURE.md`](./ARCHITECTURE.md) and [`LIMITATIONS.md`](./LIMITATIONS.md).

---

## 8. Audit Evidence and Traceability

Build provenance is recorded in `BUILD_RECORD` (operational, outside ZIP). Delivery authorization is recorded in `SIGNATURE_RECORD` / `APPROVAL_RECORD`. File integrity is recorded in `SHA256_MANIFEST.txt` and structured manifests.

Execution traces link each state transition to evidentiary artifacts. See [`../02_AUDIT_EVIDENCE/`](../02_AUDIT_EVIDENCE/).

---

## 9. Conclusion: Non-Execution as Valid State

This paper and the CEB v1 package it accompanies do not demonstrate a shipped product. They demonstrate a **governance architecture** in which:

1. Research may be shared under explicit, enumerable boundaries.
2. Execution (build, compile, deliver) is conditional on human and automated gates.
3. **Non-execution is a valid terminal posture** when design decisions, whitelist entries, or open questions remain unresolved.

As of 2026-06-30, the CEB v1 design freeze cycle is **CLOSED**. The program occupies concurrent states `AUTHORIZATION_READY_FOR_BUILD` and `REQUIRES_DESIGN_DECISION` (whitelist pending). Phase 1 clean-room preparation **executed**; Adversarial Audit V2 **review completed**. Manifest generation, full assembly, automated gating, and delivery authorization remain future transitions—each requiring its own evidence chain.

The absence of a delivered ZIP is not a project failure. It is the correct output of a governance-first model operating under Option A scope with four open gates (OQ-1, OQ-3, OQ-4, OQ-5) and pending whitelist finalization.

---

## References (In-Package)

| Document | Location |
|----------|----------|
| Release Authorization Model | `00_GOVERNANCE_MODEL/CEB_V1_RELEASE_AUTHORIZATION_MODEL.md` |
| State Machine | `00_GOVERNANCE_MODEL/STATE_MACHINE.md` |
| Whitelist Policy | `03_CLEAN_ROOM_PIPELINE/WHITELIST_POLICY.md` |
| Phase 1 Report | `03_CLEAN_ROOM_PIPELINE/PHASE_1.md` |
| Limitations | `LIMITATIONS.md` |

---

_PAPER.md — SentriOps CEB v1 — David Baldizon, 2026-06-30_

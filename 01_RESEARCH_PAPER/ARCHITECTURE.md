# Architecture

**Document:** CEB v1 Research Paper â€” Architecture  
**Date:** 2026-06-30

---

## 1. Architectural Overview

CEB v1 comprises four interacting architectural planes:

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    GOVERNANCE PLANE                          â”‚
â”‚  SRO Â· OQ Gates Â· State Machine Â· DESIGN_DECISION_READY     â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                           â”‚
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    BOUNDARY PLANE                              â”‚
â”‚  Whitelist (26 proposed routes) Â· Denylist Â· Option A Scope            â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                           â”‚
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    CLEAN-ROOM PLANE                            â”‚
â”‚  Isolated workspace Â· Selective copy Â· Sanitization           â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                           â”‚
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    EVIDENCE PLANE                              â”‚
â”‚  SHA256 Â· Manifests Â· BUILD_RECORD Â· SIGNATURE/APPROVAL       â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 2. Sovereign Trust Fabric (Research Layer)

STF operates as a meta-audit layer above operational decision logic:

### 2.1 Trust Decision Unit (TDU)

Atomic tuple: `(Decision, EvidencePackage, TrustContext)`

Each critical decision must cite minimum evidence satisfying falsifiable predicates before execution proceeds.

### 2.2 DecisionTrust(D,t)

Composite trust evaluation at decision D, time t. Eight predicates composed with **fail-closed** semantics: any unsatisfied predicate suspends trust-dependent action.


### 2.3 Governance Evaluation Framework (Abstract)

Trust and release posture are reasoned about through a **governance evaluation framework** at the architectural level. This mirror states **control objectives** only:

| Control objective | Architectural meaning |
|-------------------|------------------------|
| Release integrity | Decisions require checksum manifests and attestable records |
| Drift resistance | Scope changes require explicit human amendment, not implicit expansion |
| Fail-closed progression | Unsatisfied gates block state transitions |
| Provenance | Only enumerated documentation categories may cross the boundary |
| Accountability | Security Release Owner retains delivery authority |

No algorithms, pseudocode, automation logic, or runtime behavior sufficient to reconstruct a product system are published here.

### 2.4 Theoretical Extensions

Research sections discuss epistemic limits of autonomous trust under degradation. These are **hypothesis-level** architectural arguments for academic evaluation—not validated product claims and not executable artifacts.

---

## 3. CEB Boundary Architecture

### 3.1 Whitelist as Boundary Primitive

The whitelist is the **sole authorized ingress mechanism**. Properties:

- File-level enumeration (26 routes for Option A)
- No directory-level grants
- Declarative public schema excerpts (category only; not operational copy instructions)
- Absence of entry = valid block

Categories:

| Category | Count | Examples |
|----------|-------|----------|
| Contractual skeleton | 6 | README_FIRST, LICENSE, placeholder READMEs |
| Public schemas | 2 | trust_event_schema.json, UEO schema |
| Evaluation template | 1 | EVALUATION_TEMPLATE.md |
| Partner documentation | 4 | PARTNER_SECURITY_MODEL.md, etc. |
| External audit package | 8 | EXTERNAL_AUDIT_PACKAGE/* |
| Curated research | 5 | research disclaimer document (category), STF Paper 1.0, etc. |

### 3.2 Denylist (Absolute Exclusions)

- Productive source trees: proprietary server implementation (not disclosed), proprietary client implementation (not disclosed), proprietary trust-layer implementation (not disclosed) (except 2 schemas)
- Unpublished research archives
- Legacy forensic workspace
- Plugins (all categories)
- Secrets, dev tooling, CI internals

### 3.3 Clean-Room Workspace

Phase 1 workspace: isolated temp directory, recreated (wipe + mkdir), outside dev repo tree.

Phase 1 boundary preparation is **documented** at research level with contractual skeleton categories. Ingress category model is **frozen** in this snapshot; enumeration gates remain documented open questions (OQ-1).

---

## 4. Integrity Architecture

Three independent layers (see Authorization Model Â§3):

| Layer | Mechanism | Question answered |
|-------|-----------|-------------------|
| Integrity | SHA-256 | Changed since packaging? |
| Provenance | Optional signature | Who signed manifest? |
| Authorization | APPROVAL_RECORD | Human permitted delivery? |

Coherence constraint binds version across ZIP name, VERSION file, and all manifests.

---

## 5. State Machine Architecture

States form a directed graph with blocking nodes. Current posture: CEB v1 **CLOSED**; concurrent `AUTHORIZATION_READY_FOR_BUILD` + `REQUIRES_DESIGN_DECISION`.

Key invariant: **READY_FOR_EXTERNAL_REVIEW â‰  delivery authorized**

Transition to `APPROVED_FOR_DELIVERY` requires:
- Gate exit 0
- V2 audit without CRITICAL/HIGH blockers
- OQ-1, OQ-3, OQ-4, OQ-5 resolved or waived
- SRO sign-off in APPROVAL_RECORD

---

## 6. Comparison with Adjacent Models

| Model | Relationship to CEB/STF |
|-------|------------------------|
| Zero Trust | Complementary â€” CEB does not replace network identity verification |
| SLSA | Complementary â€” CEB adds human OQ gates and research IP boundary |
| TPM/TEE | Not equivalent â€” STF models attestation synthetically in sandbox |
| SIEM/EDR | Not replacement â€” SentinelOps is defensive copilot research |

---

## 7. Package Structure (Option A)

```
SentriOps_CEB_v1.0-CEB-RELEASE/
â”œâ”€â”€ README_FIRST
â”œâ”€â”€ LICENSE
â”œâ”€â”€ application/README.md          (placeholder â€” no binaries)
â”œâ”€â”€ demo/
â”‚   â”œâ”€â”€ schemas/                   (2 JSON schemas)
â”‚   â””â”€â”€ EVALUATION_TEMPLATE.md
â”œâ”€â”€ documentation/
â”‚   â”œâ”€â”€ external-audit/            (8 files)
â”‚   â””â”€â”€ research/                  (5 files)
â””â”€â”€ integrity/                     (manifests generated at BUILD)
```

---

_ARCHITECTURE.md â€” CEB v1 â€” 2026-06-30_

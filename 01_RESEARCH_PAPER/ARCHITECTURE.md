# Architecture

**Document:** CEB v1 Research Paper — Architecture  
**Date:** 2026-06-30

---

## 1. Architectural Overview

CEB v1 comprises four interacting architectural planes:

```
┌─────────────────────────────────────────────────────────────┐
│                    GOVERNANCE PLANE                          │
│  SRO · OQ Gates · State Machine · DESIGN_DECISION_READY     │
└──────────────────────────┬──────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────┐
│                    BOUNDARY PLANE                              │
│  Whitelist (26 proposed routes) · Denylist · Option A Scope            │
└──────────────────────────┬──────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────┐
│                    CLEAN-ROOM PLANE                            │
│  Isolated workspace · Selective copy · Sanitization           │
└──────────────────────────┬──────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────┐
│                    EVIDENCE PLANE                              │
│  SHA256 · Manifests · BUILD_RECORD · SIGNATURE/APPROVAL       │
└─────────────────────────────────────────────────────────────┘
```

---

## 2. Sovereign Trust Fabric (Research Layer)

STF operates as a meta-audit layer above operational decision logic:

### 2.1 Trust Decision Unit (TDU)

Atomic tuple: `(Decision, EvidencePackage, TrustContext)`

Each critical decision must cite minimum evidence satisfying falsifiable predicates before execution proceeds.

### 2.2 DecisionTrust(D,t)

Composite trust evaluation at decision D, time t. Eight predicates composed with **fail-closed** semantics: any unsatisfied predicate suspends trust-dependent action.

### 2.3 SARP Protocol Layers

| Layer | Function |
|-------|----------|
| SARP-01..07 | Manifest and execution integrity |
| SARP-09, SARP-04 | Tamper detection |
| G3.8, SARP-06 | Fail-closed degradation |
| SARP-10 | Build integrity via immutable hashes |
| SARP-16 | Component provenance |
| SARP-19 | Conditional recovery with attestation |
| SARP-Y | Meta-trust and bias detection |

Empirical validation exists for PR #43 scope only (sandbox, 300 tests).

### 2.4 SARP-OMEGA (Theoretical)

Axiomatic extension (ACI, AHP, AVI, AHS, ANCR, AAT) addressing epistemic limits of autonomous trust. Frozen v1.0; external review pending. **Not** validated by PR #43 empirical closure.

---

## 3. CEB Boundary Architecture

### 3.1 Whitelist as Boundary Primitive

The whitelist is the **sole authorized ingress mechanism**. Properties:

- File-level enumeration (26 routes for Option A)
- No directory-level grants
- Two declarative JSON schemas from `trust-fabric/` (point copy only)
- Absence of entry = valid block

Categories:

| Category | Count | Examples |
|----------|-------|----------|
| Contractual skeleton | 6 | README_FIRST, LICENSE, placeholder READMEs |
| Public schemas | 2 | trust_event_schema.json, UEO schema |
| Evaluation template | 1 | EVALUATION_TEMPLATE.md |
| Partner documentation | 4 | PARTNER_SECURITY_MODEL.md, etc. |
| External audit package | 8 | EXTERNAL_AUDIT_PACKAGE/* |
| Curated research | 5 | SARP_NO_CLAIMS.md, STF Paper 1.0, etc. |

### 3.2 Denylist (Absolute Exclusions)

- Productive source trees: `backend/`, `frontend/`, `trust-fabric/` (except 2 schemas)
- Unpublished research archives
- Legacy forensic workspace
- Plugins (all categories)
- Secrets, dev tooling, CI internals

### 3.3 Clean-Room Workspace

Phase 1 workspace: isolated temp directory, recreated (wipe + mkdir), outside dev repo tree.

Phase 1 **executed** with 6 contractual skeleton files. Proposed 26-route whitelist **pending** SRO finalization. Sanitization PASS; secret scan PASS on skeleton scope.

---

## 4. Integrity Architecture

Three independent layers (see Authorization Model §3):

| Layer | Mechanism | Question answered |
|-------|-----------|-------------------|
| Integrity | SHA-256 | Changed since packaging? |
| Provenance | Optional signature | Who signed manifest? |
| Authorization | APPROVAL_RECORD | Human permitted delivery? |

Coherence constraint binds version across ZIP name, VERSION file, and all manifests.

---

## 5. State Machine Architecture

States form a directed graph with blocking nodes. Current posture: CEB v1 **CLOSED**; concurrent `AUTHORIZATION_READY_FOR_BUILD` + `REQUIRES_DESIGN_DECISION`.

Key invariant: **READY_FOR_EXTERNAL_REVIEW ≠ delivery authorized**

Transition to `APPROVED_FOR_DELIVERY` requires:
- Gate exit 0
- V2 audit without CRITICAL/HIGH blockers
- OQ-1, OQ-3, OQ-4, OQ-5 resolved or waived
- SRO sign-off in APPROVAL_RECORD

---

## 6. Comparison with Adjacent Models

| Model | Relationship to CEB/STF |
|-------|------------------------|
| Zero Trust | Complementary — CEB does not replace network identity verification |
| SLSA | Complementary — CEB adds human OQ gates and research IP boundary |
| TPM/TEE | Not equivalent — STF models attestation synthetically in sandbox |
| SIEM/EDR | Not replacement — SentinelOps is defensive copilot research |

---

## 7. Package Structure (Option A)

```
SentriOps_Partner_Evaluation_partner-eval-1.0.0/
├── README_FIRST
├── LICENSE
├── application/README.md          (placeholder — no binaries)
├── demo/
│   ├── schemas/                   (2 JSON schemas)
│   └── EVALUATION_TEMPLATE.md
├── documentation/
│   ├── external-audit/            (8 files)
│   └── research/                  (5 files)
└── integrity/                     (manifests generated at BUILD)
```

---

_ARCHITECTURE.md — CEB v1 — 2026-06-30_

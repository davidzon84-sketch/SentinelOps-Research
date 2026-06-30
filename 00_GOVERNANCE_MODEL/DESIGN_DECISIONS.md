# CEB v1 Design Decisions (D-1 through D-5)

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Governance â€” Design Freeze Register  
**Date:** 2026-06-30  
**Program status:** CEB v1 **CLOSED** (design freeze complete)  
**Concurrent operational states:** `AUTHORIZATION_READY_FOR_BUILD` Â· `REQUIRES_DESIGN_DECISION` (whitelist pending)

> **Explicit declaration:** This document records frozen design decisions. It does not produce ZIP artifacts, execute builds, modify productive code, or authorize partner delivery.

---

## 1. Purpose

Design decisions D-1 through D-5 translate pre-release readiness findings into verifiable boundary constraints. They constitute the authoritative design freeze for CEB v1 and remain binding until superseded by a new Release ID under CEB v2 or later.

---

## 2. Decision Register

### D-1 â€” Release Identity

| Field | Frozen value (v1.0-CEB-RELEASE) |
|-------|-------------------------------|
| Human name | SentinelOps CEB v1.0 Governance Architecture |
| Product line | SentinelOps CEB Governance |
| Publication version | `v1.0-CEB-RELEASE` |
| Release ID format | `SOPS-CEB-RELEASE-YYYY-MM-DD-vN` |
| Target archive name | `SentriOps_CEB_v1.0-CEB-RELEASE.zip` |
| `integrity/VERSION` | `v1.0-CEB-RELEASE` |

**Rationale.** Discontinuity with legacy blocked artifacts requires an unambiguous frozen publication identity. This artifact is a non-executable governance model.

**OQ-1 status:** Documented at research level — enumeration gates for ingress categories.

**Superseded nomenclature:** Prior "Demo" and partner-evaluation naming lines are discontinued in favor of `v1.0-CEB-RELEASE`.

---

### D-2 â€” Application Boundary

| Component | Permitted | Condition |
|-----------|-----------|-----------|
| `README_FIRST` | Yes | Boundary notice; no compliance promises |
| `LICENSE` | Yes | Limited evaluation license |
| `demo/` | Yes | Synthetic data; isolated instructions |
| `documentation/` | Yes | Curated guides; no internal roadmap |
| `integrity/` | Yes | Manifests and hashes; no private keys |
| `application/` | Conditional | Placeholder only under Option A |

**Private (never crosses boundary):** proprietary server implementation (not disclosed), proprietary client implementation (not disclosed), proprietary trust-layer implementation (not disclosed) (source tree); unpublished research archives; secrets; dev toolchain; internal governance; legacy blocked artifacts; forensic workspace origin.

**Out of scope:** Regulatory certification; SIEM/EDR/WAF replacement; dev infrastructure access; IP transfer; undeclared telemetry; external targeting.

---

### D-3 â€” Clean-Room Build Model

| Principle | Requirement |
|-----------|-------------|
| Workspace isolation | Outside development repository tree |
| Ingress | File-level whitelist only; no directory grants |
| Prohibited origins | Dev working tree, `internal audit workspace/`, legacy ZIP |
| Recursive copy | **Prohibited** |
| Non-execution | Valid terminal posture when preconditions unmet |

**Phase 1 status:** **EXECUTED** (2026-06-30) â€” isolated workspace prepared; contractual skeleton staged; no compilation, binaries, or ZIP.

---

### D-4 â€” Evidence and Integrity Model

Three independent layers:

1. **Integrity (SHA-256):** Per-file and ZIP-level hashes in `integrity/SHA256_MANIFEST.txt`, `RELEASE_MANIFEST.json`, `DELIVERY_MANIFEST.json`.
2. **Provenance (signature):** Optional in v1.0 â€” OQ-4 **OPEN**.
3. **Authorization (human):** `integrity/APPROVAL_RECORD.md` â€” sole delivery enabler.

Mandatory coherence: `ZIP_name.version == integrity/VERSION == RELEASE_MANIFEST.version == DELIVERY_MANIFEST.version`.

---

### D-5 â€” Plugin Policy

| Category | CEB v1.0 policy |
|----------|-----------------|
| Included | **None** â€” `plugins/` absent by default |
| Excluded | `plugins/premium/*`, `plugins/proprietary server implementation/*`, any infra/secret/tenant plugin |
| Future inclusion | Requires sandbox audit + whitelist amendment + OQ-5 resolution |

---

## 3. Scope Decision (OQ-6 â€” CLOSED)

**Option A selected:** Pure Documentation/Research Review for v1.0.

| Rule | Value |
|------|-------|
| v1.0 content | Curated documentation, public JSON schemas (point copy), contractual placeholders |
| Option B (deferred) | Functional evaluation binaries â†’ Release ID `-v2` with IP co-approval (OQ-3) |
| Prohibited always | Productive source trees |

---

## 4. Whitelist Status

| Field | Value |
|-------|-------|
| **DESIGN_DECISION_READY** | Partial â€” scope frozen; **file enumeration pending** |
| **Proposed routes** | 26 (documented in `03_CLEAN_ROOM_PIPELINE/WHITELIST_POLICY.md`) |
| **Authoritative status** | **PENDING** â€” blocks exit from `REQUIRES_DESIGN_DECISION` |
| **Blocking OQs** | OQ-1 (identity alignment affects manifest fields) |

Absence of finalized whitelist is a **valid block**, not a defect requiring silent scope expansion.

---

## 5. Adversarial Audit V2

| Field | Value |
|-------|-------|
| Protocol | `PARTNER_SECURITY_AUDIT_V2/AUDIT_V2_PROTOCOL.md` |
| Criteria | FC-01 through FC-25 frozen |
| Review status | **COMPLETED** (2026-06-30) |
| Artifact-dependent items | Remain `PENDING` until build/ZIP exists â€” expected under Option A |

V2 review completion validates criteria and protocol readiness; it does not substitute artifact verification or delivery authorization.

---

## 6. Open Question Cross-Reference

| ID | Status | Impact on design freeze |
|----|--------|-------------------------|
| OQ-1 | **OPEN** | Identity fields provisional |
| OQ-2 | **CLOSED** | SRO = David Baldizon |
| OQ-3 | **OPEN** | Blocks Option B binaries |
| OQ-4 | **OPEN** | Signature optional |
| OQ-5 | **OPEN** | Plugin inclusion if partner mandates |
| OQ-6 | **CLOSED** | Option A documental v1.0 |

---

## 7. CEB v1 Closure Statement

```
CEB_V1_DESIGN_FREEZE
STATUS                    = CLOSED (2026-06-30)
OPERATIONAL_STATES        = AUTHORIZATION_READY_FOR_BUILD + REQUIRES_DESIGN_DECISION
WHITELIST                 = PENDING (proposed 26 routes)
PHASE_1                   = EXECUTED
PHASE_2                   = NOT AUTHORIZED (Option A)
V2_REVIEW                 = COMPLETED
DELIVERY_AUTHORIZED       = NO
OPEN_QUESTIONS            = 4 (OQ-1, OQ-3, OQ-4, OQ-5)
NON_EXECUTION_POSTURE     = VALID AND PREFERRED until gates close
```

CEB v1 design freeze is **closed**. Operational progress toward delivery remains gated by open OQs and whitelist finalization.

---

_DESIGN_DECISIONS.md â€” CEB v1 Governance â€” 2026-06-30_

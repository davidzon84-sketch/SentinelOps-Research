# CEB v1 Design Decisions (D-1 through D-5)

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Governance — Design Freeze Register  
**Date:** 2026-06-30  
**Program status:** CEB v1 **CLOSED** (design freeze complete)  
**Concurrent operational states:** `AUTHORIZATION_READY_FOR_BUILD` · `REQUIRES_DESIGN_DECISION` (whitelist pending)

> **Explicit declaration:** This document records frozen design decisions. It does not produce ZIP artifacts, execute builds, modify productive code, or authorize partner delivery.

---

## 1. Purpose

Design decisions D-1 through D-5 translate pre-release readiness findings into verifiable boundary constraints. They constitute the authoritative design freeze for CEB v1 and remain binding until superseded by a new Release ID under CEB v2 or later.

---

## 2. Decision Register

### D-1 — Release Identity

| Field | Proposed value (pending OQ-1) |
|-------|-------------------------------|
| Human name | SentriOps Partner Evaluation v1.0 |
| Product line | SentriOps Partner Evaluation |
| Semantic version | `partner-eval-1.0.0` |
| Release ID format | `SOPS-PARTNER-EVAL-YYYY-MM-DD-vN` |
| Target ZIP name | `SentriOps_Partner_Evaluation_partner-eval-1.0.0.zip` |
| `integrity/VERSION` | `partner-eval-1.0.0` |

**Rationale.** Discontinuity with legacy `v1.22.0` requires an unambiguous identity. "Evaluation" communicates limited scope without implying certification or live-data operation.

**OQ-1 status:** **OPEN** — supersession of "Demo" / `partner-eval-2.0.0` nomenclature requires explicit SRO confirmation before manifest generation.

**Superseded sources:** `PARTNER_RELEASE_IDENTITY.md` (`partner-eval-2.0.0`, "Demo" naming); `PARTNER_VERSION_POLICY.md` §5 (`SentriOps_Partner_Demo_<version>.zip`).

---

### D-2 — Application Boundary

| Component | Permitted | Condition |
|-----------|-----------|-----------|
| `README_FIRST` | Yes | Boundary notice; no compliance promises |
| `LICENSE` | Yes | Limited evaluation license |
| `demo/` | Yes | Synthetic data; isolated instructions |
| `documentation/` | Yes | Curated guides; no internal roadmap |
| `integrity/` | Yes | Manifests and hashes; no private keys |
| `application/` | Conditional | Placeholder only under Option A |

**Private (never crosses boundary):** `backend/`, `frontend/`, `trust-fabric/` (source tree); unpublished research archives; secrets; dev toolchain; internal governance; legacy `v1.22.0` artifact; forensic workspace origin.

**Out of scope:** Regulatory certification; SIEM/EDR/WAF replacement; dev infrastructure access; IP transfer; undeclared telemetry; external targeting.

---

### D-3 — Clean-Room Build Model

| Principle | Requirement |
|-----------|-------------|
| Workspace isolation | Outside development repository tree |
| Ingress | File-level whitelist only; no directory grants |
| Prohibited origins | Dev working tree, `PARTNER_SECURITY_AUDIT/workspace/`, legacy ZIP |
| Recursive copy | **Prohibited** |
| Non-execution | Valid terminal posture when preconditions unmet |

**Phase 1 status:** **EXECUTED** (2026-06-30) — isolated workspace prepared; contractual skeleton staged; no compilation, binaries, or ZIP.

---

### D-4 — Evidence and Integrity Model

Three independent layers:

1. **Integrity (SHA-256):** Per-file and ZIP-level hashes in `integrity/SHA256_MANIFEST.txt`, `RELEASE_MANIFEST.json`, `DELIVERY_MANIFEST.json`.
2. **Provenance (signature):** Optional in v1.0 — OQ-4 **OPEN**.
3. **Authorization (human):** `integrity/APPROVAL_RECORD.md` — sole delivery enabler.

Mandatory coherence: `ZIP_name.version == integrity/VERSION == RELEASE_MANIFEST.version == DELIVERY_MANIFEST.version`.

---

### D-5 — Plugin Policy

| Category | CEB v1.0 policy |
|----------|-----------------|
| Included | **None** — `plugins/` absent by default |
| Excluded | `plugins/premium/*`, `plugins/backend/*`, any infra/secret/tenant plugin |
| Future inclusion | Requires sandbox audit + whitelist amendment + OQ-5 resolution |

---

## 3. Scope Decision (OQ-6 — CLOSED)

**Option A selected:** Pure Documentation/Research Review for v1.0.

| Rule | Value |
|------|-------|
| v1.0 content | Curated documentation, public JSON schemas (point copy), contractual placeholders |
| Option B (deferred) | Functional evaluation binaries → Release ID `-v2` with IP co-approval (OQ-3) |
| Prohibited always | Productive source trees |

---

## 4. Whitelist Status

| Field | Value |
|-------|-------|
| **DESIGN_DECISION_READY** | Partial — scope frozen; **file enumeration pending** |
| **Proposed routes** | 26 (documented in `03_CLEAN_ROOM_PIPELINE/WHITELIST_POLICY.md`) |
| **Authoritative status** | **PENDING** — blocks exit from `REQUIRES_DESIGN_DECISION` |
| **Blocking OQs** | OQ-1 (identity alignment affects manifest fields) |

Absence of finalized whitelist is a **valid block**, not a defect requiring silent scope expansion.

---

## 5. Adversarial Audit V2

| Field | Value |
|-------|-------|
| Protocol | `PARTNER_SECURITY_AUDIT_V2/AUDIT_V2_PROTOCOL.md` |
| Criteria | FC-01 through FC-25 frozen |
| Review status | **COMPLETED** (2026-06-30) |
| Artifact-dependent items | Remain `PENDING` until build/ZIP exists — expected under Option A |

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

_DESIGN_DECISIONS.md — CEB v1 Governance — 2026-06-30_

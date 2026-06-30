# CEB v1 Release Authorization Model

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Governance — Operational Authorization Model  
**Date:** 2026-06-30  
**CEB v1 cycle:** CLOSED  
**Current operational states:** `AUTHORIZATION_READY_FOR_BUILD` · `REQUIRES_DESIGN_DECISION` (whitelist pending)  
**Security Release Owner:** David Baldizon

> **Explicit declaration:** This document does not produce ZIP artifacts, execute builds, modify productive code, or substitute human approval.

---

## 1. Scope and Posture

The CEB v1 Release Authorization Model translates design decisions D-1 through D-5 into verifiable authorization requirements. It establishes controls for integrity, provenance, and human decision authority without claiming absolute security of any artifact.

### Provisional Release Identity (OQ-1 OPEN)

| Field | Proposed value |
|-------|----------------|
| Human name | SentriOps Partner Evaluation v1.0 |
| Semantic version | `partner-eval-1.0.0` |
| Release ID format | `SOPS-PARTNER-EVAL-YYYY-MM-DD-vN` |
| Target ZIP name | `SentriOps_Partner_Evaluation_partner-eval-1.0.0.zip` |

Identity fields are **provisional** until OQ-1 closes.

---

## 2. Security Release Owner (SRO)

### 2.1 Role Definition

The Security Release Owner is the final human authority for crossing the boundary toward external evaluation. This role is not automatable and is not delegable to gates or adversarial audits.

| Attribute | Definition |
|-----------|------------|
| **Holder** | David Baldizon — Project Owner (SentinelOps OS); designated SRO (OQ-2 **CLOSED** 2026-06-30) |
| **Research / IP Owner** | David Baldizon — custody of unpublished research and exposure policy |
| **Security Release Architect** | Design and contract role — does not substitute SRO approval |

### 2.2 SRO Responsibilities

1. Authorize or reject initiation of clean-room build under declared scope.
2. Review build evidence (`BUILD_RECORD`, manifests, clean-room log) before declaring `BUILD_VALIDATED`.
3. Confirm adversarial audit V2 has no open CRITICAL/HIGH blockers before external review transition.
4. Issue documented verdict in `integrity/APPROVAL_RECORD.md` — sole mechanism enabling `APPROVED_FOR_DELIVERY`.
5. Reject delivery if any identity field diverges from version policy.

### 2.3 Approval Authority Limits

| Action | Authorizer |
|--------|------------|
| Initiate clean-room build under CEB v1 | SRO |
| Declare `BUILD_VALIDATED` | SRO + technical evidence |
| Declare `READY_FOR_EXTERNAL_REVIEW` | Gate exit 0 + V2 audit without blockers |
| Deliver ZIP to external partner | SRO + complete `APPROVAL_RECORD.md` |
| Omit V2 audit or human approval | **Prohibited** |

---

## 3. Cryptographic Identity Model

Three **independent** layers. Conflating them invalidates the evidence chain.

### 3.1 Integrity — Hash (SHA-256)

| Question | Has package content changed since packaging? |
| Mechanism | SHA-256 per file + SHA-256 of complete ZIP |
| Evidence | `integrity/SHA256_MANIFEST.txt`, `RELEASE_MANIFEST.json`, `DELIVERY_MANIFEST.json` |
| Limit | Proves artifact integrity, not absence of vulnerabilities or sender authenticity |

### 3.2 Provenance — Signature (optional v1.0)

| Question | Who generated the manifest and with what cryptographic identity? |
| Mechanism | Manifest signature (e.g., `RELEASE_MANIFEST.json.sig`) + embedded public key |
| CEB v1.0 status | **Optional** — OQ-4 **OPEN** |
| Prohibited | Private keys (`*.pem`, `*.key`) in partner package |

### 3.3 Authorization — Human Decision

| Question | Did an authorized human permit delivery? |
| Mechanism | `integrity/APPROVAL_RECORD.md` — roles, UTC date, release_id, verdict |
| Rule | Without complete `APPROVAL_RECORD.md` → maximum state `READY_FOR_EXTERNAL_REVIEW` |

### 3.4 Mandatory Coherence

```
ZIP_name.version == integrity/VERSION == RELEASE_MANIFEST.version == DELIVERY_MANIFEST.version
```

Any divergence → `BLOCKED_PENDING_REMEDIATION`.

---

## 4. Plugin Policy (D-5)

| Category | CEB v1.0 Policy |
|----------|-----------------|
| Included | **None** — `plugins/` directory absent by default |
| Excluded absolutely | `plugins/premium/*`, `plugins/backend/*`, any plugin with infra/secret/tenant access |
| OQ-5 | **OPEN** — partner acceptance of zero-plugin v1.0 |

---

## 5. Binary Scope (OQ-6 — CLOSED)

**Option A selected:** Pure Documentation/Research Review for v1.0.

| Component | v1.0 Policy |
|-----------|-------------|
| `application/` | `README.md` placeholder only — no functional binaries |
| Option B (deferred) | Functional evaluation binaries → release ID `-v2` with IP co-approval (OQ-3) |
| Always prohibited | Productive source: `backend/`, `frontend/`, `trust-fabric/` as source tree |

---

## 6. Release Evidence Package

### 6.1 Mandatory `integrity/` Files (generated at BUILD)

| File | Purpose | Phase |
|------|---------|-------|
| `SHA256_MANIFEST.txt` | Flat `hash  path` list | BUILD |
| `RELEASE_MANIFEST.json` | Structured inventory | BUILD |
| `DELIVERY_MANIFEST.json` | ZIP hash, timestamp, `security_status` | POST-ZIP |
| `VERSION` | Single version string | BUILD |
| `APPROVAL_RECORD.md` | Human approval record | POST-AUDIT |

### 6.2 Operational BUILD_RECORD (outside ZIP)

Location: `partner-release/reports/BUILD_RECORD_<ReleaseID>.md`  
Covers operational provenance; does not substitute manifests or human approval.

---

## 7. Evidence Generation Flow

```
CLEAN_BUILD_ENVIRONMENT
  → SHA-256 inventory
  → SHA256_MANIFEST.txt + RELEASE_MANIFEST.json + VERSION
  → BUILD_RECORD (start and close)
  → PACKAGE_GENERATION (ZIP) [requires explicit authorization]
  → DELIVERY_MANIFEST.json (security_status: pending)
  → AUDIT_GATE (exit 0) → BUILD_VALIDATED
  → AUDIT V2 (no CRITICAL/HIGH) → READY_FOR_EXTERNAL_REVIEW
  → APPROVAL_RECORD.md → APPROVED_FOR_DELIVERY
```

**Current position:** Phase 1 executed; flow paused at clean-room preparation — valid under Option A and open OQs.

---

## 8. Open Questions Register

| ID | Status | Question |
|----|--------|----------|
| OQ-1 | **OPEN** | Nomenclature supersession confirmation |
| OQ-2 | **CLOSED** | SRO = David Baldizon |
| OQ-3 | **OPEN** | Research/IP Owner co-approval for binaries |
| OQ-4 | **OPEN** | Manifest signature in v1.0 |
| OQ-5 | **OPEN** | v1.0 without plugins acceptable to partner |
| OQ-6 | **CLOSED** | Option A documental for v1.0 |

**Open count:** 4

---

## 9. V2 Review Status

Adversarial Audit V2 **review completed** (2026-06-30). Criteria frozen; FC-03 PASS (SRO identified). Artifact-dependent items PENDING — consistent with non-execution posture.

---

## 10. Final Authorization Statement

```
CEB_V1_RELEASE_AUTHORIZATION_MODEL
BOUNDARY              = Controlled Evaluation Boundary v1
CYCLE_STATUS          = CLOSED
OPERATIONAL_STATES    = AUTHORIZATION_READY_FOR_BUILD + REQUIRES_DESIGN_DECISION
IDENTITY              = PROVISIONAL (OQ-1 OPEN)
SCOPE                 = Option A — documental only
WHITELIST             = PENDING
PHASE_1               = EXECUTED
V2_REVIEW             = COMPLETED
OPEN_QUESTIONS        = 4 (OQ-1, OQ-3, OQ-4, OQ-5)
DELIVERY_AUTHORIZED   = NO
NON_EXECUTION         = VALID SECURITY STATE
```

This model authorizes continued governance documentation and clean-room preparation. It does **not** authorize partner delivery.

---

_CEB v1 Release Authorization Model — 2026-06-30_

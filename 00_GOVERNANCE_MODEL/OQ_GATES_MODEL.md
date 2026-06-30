# CEB v1 Open Question (OQ) Gates Model

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Governance â€” Decision Gate Framework  
**Date:** 2026-06-30  
**Security Release Owner:** David Baldizon  
**CEB v1 cycle:** CLOSED

---

## 1. Purpose

Open Questions (OQ) are **explicit decision gates** that block specific state transitions until human authority resolves them. Unlike automated gates (hash verification, denylist scan), OQ gates require documented SRO or IP Owner decisions and cannot be closed by tooling alone.

---

## 2. Gate Taxonomy

| Gate class | Mechanism | Closes by |
|------------|-----------|-----------|
| **OQ Gate** | Human decision register | SRO/IP Owner documented answer |
| **Design Gate** | Whitelist + scope freeze | File-level enumeration + SRO sign-off |
| **Automated Gate** | `structural validation gate (conceptual)` | Exit code 0 |
| **Adversarial Gate** | Audit V2 checklist | No CRITICAL/HIGH blockers |
| **Authorization Gate** | `APPROVAL_RECORD.md` | SRO sign-off |

OQ gates operate **upstream** of automated and adversarial gates. Unresolved OQ gates may leave the program in valid non-execution states indefinitely.

---

## 3. OQ Register

### 3.1 Closed Questions

| ID | Question | Decision | Date | Impact |
|----|----------|----------|------|--------|
| **OQ-2** | Who is Security Release Owner? | **David Baldizon**, Project Owner | 2026-06-30 | Approval authority chain |
| **OQ-6** | Structure-only vs binaries in first delivery? | **Option A** â€” documental v1.0; binaries deferred to `-v2` | 2026-06-30 | Scope, Phase 2 path |

### 3.2 Open Questions

| ID | Question | Blocks | Priority | Default if unresolved |
|----|----------|--------|----------|----------------------|
| **OQ-1** | Confirm frozen publication identity `v1.0-CEB-RELEASE` for Zenodo/GitHub deposit? | Identity alignment; manifest templates; ingress enumeration gates | **High** | Documented at research level |
| **OQ-3** | Does David Baldizon confirm Research/IP Owner role for binary co-approval? | Option B binary delivery; `application/` with executables | Medium (High for v2) | Remain Option A only |
| **OQ-4** | Include manifest cryptographic signature in v1.0? | `RELEASE_MANIFEST.json.sig` in package | Low | Ship without signature |
| **OQ-5** | Is v1.0 without plugins acceptable to partner? | Plugin inclusion decision | Medium | Zero plugins (conservative default) |

**Closed count:** 2 Â· **Open count:** 4

---

## 4. OQ Gate â†’ State Mapping

| OQ status | Permitted maximum state | Rationale |
|-----------|------------------------|-----------|
| OQ-1 open | `REQUIRES_DESIGN_DECISION` | Identity ambiguity blocks manifest generation |
| OQ-2 open | `DESIGN_READY_FOR_BUILD` | No approval authority defined |
| OQ-6 open | `REQUIRES_DESIGN_DECISION` | Cannot define scope or Phase 2 path |
| OQ-3 open (Option B) | `BUILD_VALIDATED` (binaries only) | IP exposure requires co-approval |
| OQ-4 open | `READY_FOR_EXTERNAL_REVIEW` | Signature optional; does not block review |
| OQ-5 open | `APPROVED_FOR_DELIVERY` | Partner content confirmation required |

**Current posture:** OQ-1 open â†’ concurrent `AUTHORIZATION_READY_FOR_BUILD` + `REQUIRES_DESIGN_DECISION` is valid.

---

## 5. OQ Resolution Protocol

Each OQ closure requires:

1. **Authority:** Named SRO or IP Owner
2. **Timestamp:** UTC date
3. **Decision text:** Recorded in governance artifact (`DESIGN_DECISIONS.md` or `SIGNATURE_RECORD.md`)
4. **Downstream update:** Whitelist, manifests, or scope documents amended if applicable

Automated gate PASS does **not** close OQ gates.

---

## 6. Relationship to V2 Review

Adversarial Audit V2 **review completed** (2026-06-30). FC-03 (SRO identified) **PASS** via OQ-2 closure. FC-19 through FC-21 (binary scope) reflect OQ-6 Option A â€” no binaries expected in v1.0.

Open OQs do not invalidate V2 review completion; they define remaining human gates before delivery authorization.

---

## 7. Non-Execution Principle

Four open OQs with Phase 1 executed and no build/ZIP is a **valid terminal posture** for CEB v1 Option A. The program must not infer closure of OQ-1 from tooling output or partial assembly.

---

## 8. Register Summary

```
OQ_REGISTER_CEB_V1
CLOSED    = OQ-2, OQ-6
OPEN      = OQ-1, OQ-3, OQ-4, OQ-5
BLOCKS    = APPROVED_FOR_DELIVERY (all delivery OQs)
WHITELIST = PENDING (OQ-1 dependency)
```

---

_OQ Gates Model â€” CEB v1 â€” 2026-06-30_

# Zenodo Version

**Field:** Version / Release Identity  
**Date:** 2026-06-30  
**Status:** Provisional — OQ-1 OPEN

---

## Release Identity

| Field | Value |
|-------|-------|
| **Human name** | SentriOps Partner Evaluation v1.0 *(provisional)* |
| **Semantic version** | `partner-eval-1.0.0` |
| **Release ID** | `SOPS-PARTNER-EVAL-2026-06-30-v1` |
| **CEB boundary version** | v1 (**CLOSED**) |
| **Scope option** | A — Pure Documentation/Research Review |

---

## Version Policy

- `v1.0` = first controlled external evaluation line under CEB v1
- **Discontinuous** with legacy `v1.22.0` (blocked artifact)
- Subsequent deliveries increment Release ID suffix (`-v2`, `-v3`) independently of semantic version
- Never reuse hashes or identity from prior blocked releases
- Zenodo version increments align with semantic version upon deposit

---

## Dual Publication Versioning

| Channel | Version binding |
|---------|-------------------|
| **Zenodo** | `partner-eval-1.0.0` in metadata; immutable snapshot |
| **GitHub** | Tag `partner-eval-1.0.0`; living governance trace |
| **Coherence** | Zenodo deposit references Git commit SHA in BUILD_RECORD |

---

## Related Research Versions

| Component | Version | Status |
|-----------|---------|--------|
| SARP-OMEGA | v1.0 | Frozen 2026-06-29 |
| STF Paper | 1.0 | Frozen |
| PR #43 empirical scope | SHA `50969f5` | Formal closure (separate from CEB package) |
| EXTERNAL_AUDIT_PACKAGE | Externalization v1 | Public research docs |

---

## Zenodo Version Field

```
version = "partner-eval-1.0.0"
```

---

## Current Program State at This Version

```
CEB_V1_CYCLE          = CLOSED
OPERATIONAL_STATES    = AUTHORIZATION_READY_FOR_BUILD + REQUIRES_DESIGN_DECISION
PHASE_1               = EXECUTED
V2_REVIEW             = COMPLETED
WHITELIST             = PENDING
DELIVERY              = NOT AUTHORIZED
OPEN_OQ               = 4 (OQ-1, OQ-3, OQ-4, OQ-5)
```

---

_VERSION.md — Zenodo Metadata — CEB v1 — 2026-06-30_

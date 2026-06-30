# Zenodo Version

**Field:** Version / Release Identity  
**Date:** 2026-06-30  
**Status:** Frozen research snapshot — **v1.0-CEB-RELEASE**

---

## Release Identity

| Field | Value |
|-------|-------|
| **Human name** | SentinelOps CEB v1.0 Governance Architecture |
| **Publication version** | `v1.0-CEB-RELEASE` |
| **Short version** | `v1.0-CEB` |
| **Release ID** | `SOPS-CEB-RELEASE-2026-06-30-v1` |
| **CEB boundary version** | v1 (**CLOSED**) |
| **Scope** | Option A — Pure Documentation/Research Review (non-executable) |

---

## Version Policy

- `v1.0-CEB` = first frozen publication line under CEB v1 governance model
- **Discontinuous** with legacy blocked product artifacts (not republished)
- Subsequent deposits increment Release ID suffix (`-v2`, `-v3`) independently of semantic version
- Never reuse hashes or identity from prior blocked releases
- Zenodo version field binds to `v1.0-CEB-RELEASE` for this deposit

---

## Dual Publication Versioning

| Channel | Version binding |
|---------|-------------------|
| **Zenodo** | `v1.0-CEB-RELEASE` in metadata; immutable frozen snapshot |
| **GitHub** | Tag `v1.0-CEB`; governance reference trace |
| **Coherence** | Zenodo deposit references Git commit SHA in deposit notes |

---

## Related Research Versions (Context Only)

| Component | Version | Status |
|-----------|---------|--------|
| Sovereign Trust Fabric (theoretical) | v1.0 | Frozen 2026-06-29 — not executable in this artifact |
| STF Paper | 1.0 | Frozen — research framing only |
| External audit package | Externalization v1 | Public research docs (abstract references) |

---

## Zenodo Version Field

```
version = "v1.0-CEB-RELEASE"
```

---

## GitHub Tag

```
v1.0-CEB
```

---

## Frozen Publication State

```
FINAL_STATE           = v1.0-CEB-RELEASE
ARTIFACT_CLASS        = non-executable governance model
PUBLICATION_POSTURE   = frozen research snapshot
CEB_V1_CYCLE          = CLOSED (governance model)
DELIVERY              = NOT AUTHORIZED (by design)
OPEN_OQ               = documented at research level (OQ-1..OQ-5)
```

---

_VERSION.md — Zenodo Metadata — CEB v1 — v1.0-CEB-RELEASE — 2026-06-30_

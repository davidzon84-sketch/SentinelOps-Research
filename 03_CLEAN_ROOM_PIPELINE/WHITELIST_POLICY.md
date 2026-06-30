# Whitelist Policy

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Clean-Room Pipeline — Boundary Ingress Policy  
**Date:** 2026-06-30  
**Status:** **PENDING** — proposed routes documented; SRO finalization required  
**DESIGN_DECISION_READY:** Partial (scope frozen; enumeration pending)

---

## 1. Policy Statement

The whitelist is the **sole authorized mechanism** for transferring files from the development repository into the clean-room evaluation workspace. Directory-level grants, recursive copy, and implicit inclusion are **prohibited**.

**Absence from the whitelist is a valid block.** Operators must not expand scope to unblock assembly without SRO-documented whitelist amendment and new governance trace.

**Current posture:** Whitelist routes are **proposed** below. Finalization blocked by OQ-1 (identity) and concurrent `REQUIRES_DESIGN_DECISION` state.

---

## 2. Selection Criteria (All Required)

| ID | Criterion | Verification |
|----|-----------|--------------|
| C-1 | Indispensable for declared partner evaluation scope | Per-row justification |
| C-2 | No secrets — no .env values, keys, tokens, credentials | Pre-copy scan |
| C-3 | No productive source — no backend/frontend/trust-fabric tree | Denylist |
| C-4 | No prohibited origin — no forensic workspace, no legacy ZIP | BS-3 |
| C-5 | IP bounded — no unpublished research, roadmap, pricing | D-2 |
| C-6 | Explicitly enumerated — file appears in manifest table | No directory grants |

---

## 3. Proposed Inventory (26 Routes — Option A)

*Status: PROPOSED — not authorized for copy until whitelist finalized.*

### §3.1 Contractual Skeleton (6)

| # | Origin | Destination |
|---|--------|-------------|
| 1 | partner-release/SentriOps_Partner_Demo_vNEXT/README_FIRST | README_FIRST |
| 2 | partner-release/SentriOps_Partner_Demo_vNEXT/LICENSE | LICENSE |
| 3 | partner-release/SentriOps_Partner_Demo_vNEXT/application/README.md | application/README.md |
| 4 | partner-release/SentriOps_Partner_Demo_vNEXT/demo/README.md | demo/README.md |
| 5 | partner-release/SentriOps_Partner_Demo_vNEXT/documentation/README.md | documentation/README.md |
| 6 | partner-release/SentriOps_Partner_Demo_vNEXT/integrity/README.md | integrity/README.md |

### §3.2 Public Schemas — Point Copy Only (2)

| # | Origin | Destination |
|---|--------|-------------|
| 7 | trust-fabric/api/trust_event_schema.json | demo/schemas/trust_event_schema.json |
| 8 | trust-fabric/uep/schema/universal_evidence_object.schema.json | demo/schemas/universal_evidence_object.schema.json |

### §3.3 Evaluation Template (1)

| # | Origin | Destination |
|---|--------|-------------|
| 9 | SentriOps_Partner_Evaluation_v1/results/EVALUATION_TEMPLATE.md | demo/EVALUATION_TEMPLATE.md |

### §3.4 Partner Documentation (4)

| # | Origin | Destination |
|---|--------|-------------|
| 10 | SentriOps_Partner_Evaluation_v1/documentation/PARTNER_SECURITY_MODEL.md | documentation/PARTNER_SECURITY_MODEL.md |
| 11 | SentriOps_Partner_Evaluation_v1/license/PARTNER_EVALUATION_LICENSE.md | documentation/PARTNER_EVALUATION_LICENSE.md |
| 12 | SentriOps_Partner_Evaluation_v1/demo/README.md | documentation/DEMO_SCOPE.md |
| 13 | SentriOps_Partner_Evaluation_v1/README.md | documentation/PACKAGE_OVERVIEW.md |

### §3.4 External Audit Package (8)

| # | Origin | Destination |
|---|--------|-------------|
| 14–21 | EXTERNAL_AUDIT_PACKAGE/*.md | documentation/external-audit/*.md |

### §3.5 Curated Research (5)

| # | Origin | Destination |
|---|--------|-------------|
| 22 | docs/research/SARP_NO_CLAIMS.md | documentation/research/SARP_NO_CLAIMS.md |
| 23 | docs/research/CLI_USER_GUIDE_G6.md | documentation/research/CLI_USER_GUIDE_G6.md |
| 24 | docs/research/SARP_OMEGA_V1_0_FREEZE.md | documentation/research/SARP_OMEGA_V1_0_FREEZE.md |
| 25 | docs/research/SOVEREIGN_TRUST_FABRIC_PAPER_1_0.md | documentation/research/SOVEREIGN_TRUST_FABRIC_PAPER_1_0.md |
| 26 | docs/research/TRUST_FABRIC_ARCHITECTURE_REVIEW_G1_G2.md | documentation/research/TRUST_FABRIC_ARCHITECTURE_REVIEW_G1_G2.md |

---

## 4. Phase 1 Executed Scope (6 Routes)

Phase 1 (2026-06-30) copied **contractual skeleton only** (routes 1–6) to isolated clean-room workspace. Full 26-route assembly **not executed** — blocked by pending whitelist finalization.

---

## 5. Absolute Exclusions

| Category | Patterns |
|----------|----------|
| Productive source | backend/, frontend/, trust-fabric/ *(tree)* |
| Unpublished research | PAPER/, SentriOps_Research_Archive/, docs/research/ *(full tree)* |
| Forensic / legacy | PARTNER_SECURITY_AUDIT/workspace/, v1.22.0 ZIP |
| Plugins | plugins/ *(all)* |
| Secrets / dev | .env values, *.pem, *.key, .git/, node_modules/, CI internals |
| Legacy product stack | docker-compose.release.yml (forensic), install scripts, product Docker images |
| Binaries (Option A) | application/* except README.md placeholder |

---

## 6. Generated at BUILD (Not Copied from Dev Repo)

| Path | Phase | Status |
|------|-------|--------|
| integrity/VERSION | BUILD | Not generated |
| integrity/SHA256_MANIFEST.txt | BUILD | Not generated |
| integrity/RELEASE_MANIFEST.json | BUILD | Not generated |
| integrity/DELIVERY_MANIFEST.json | POST-ZIP | Not generated |
| integrity/APPROVAL_RECORD.md | POST-AUDIT | Not generated |
| integrity/RELEASE_MANIFEST.json.sig | Optional (OQ-4) | Not generated |

---

## 7. Whitelist Finalization Process

1. SRO closes OQ-1 (identity alignment).
2. SRO confirms proposed 26 routes or amends with C-1..C-6 justification per file.
3. Security Release Architect records finalized manifest.
4. `DESIGN_DECISION_READY: TRUE` set for whitelist dimension.
5. Exit from `REQUIRES_DESIGN_DECISION` authorized for full assembly.

**Silent finalization is prohibited.**

---

## 8. Enforcement

| Mechanism | Role |
|-----------|------|
| Pre-copy denylist scan | Build operator |
| partner_release_gate.py | Automated structural validation |
| Adversarial audit V2-F | Doc vs artifact coherence |
| SHA256 manifest | Independent evaluator verification |

V2 review **completed** — enforcement criteria frozen; artifact verification pending build.

---

## 9. Status Summary

```
WHITELIST_POLICY_CEB_V1
PROPOSED_ROUTES     = 26
PHASE_1_COPIED      = 6 (skeleton only)
STATUS              = PENDING FINALIZATION
BLOCKING_OQ         = OQ-1
CONCURRENT_STATE    = REQUIRES_DESIGN_DECISION
```

---

_Whitelist Policy — CEB v1 — 2026-06-30_

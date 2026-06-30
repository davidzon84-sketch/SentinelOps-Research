# Future Work

**Document:** CEB v1 Research Paper â€” Future Work  
**Date:** 2026-06-30

---

## 1. Immediate Operational (CEB v1 Continuation)

| Item | Dependency | Target state |
|------|------------|--------------|
| Close OQ-1 (identity) | SRO decision | Exit REQUIRES_DESIGN_DECISION |
| Finalize whitelist (26 routes) | OQ-1 + SRO confirmation | Full assembly authorized |
| Generate integrity manifests | Whitelist assembly complete | `BUILD_VALIDATED` |
| Execute structural validation gate (conceptual) | Manifests present | Gate evidence archived |
| Close OQ-3, OQ-4, OQ-5 | SRO decisions | Delivery gate cleared |
| SRO sign-off | All gates pass | `APPROVED_FOR_DELIVERY` |

**Note:** Adversarial Audit V2 **review completed** (2026-06-30). Artifact-dependent verification remains pending â€” consistent with Option A non-execution posture.

---

## 2. CEB v1 Release `-v2` (Option B â€” Deferred)

Option B would introduce functional evaluation binaries under stricter controls:

| Component | Requirement |
|-----------|-------------|
| `deferred evaluation CLI (not in public artifact)` | CLI G6 binary; stripped; RE review |
| `deferred evaluation harness (not in public artifact)` | Requires author definition of minimal harness |
| Build input manifest | File-level compile inputs enumerated |
| OQ-3 | IP Owner co-approval mandatory |
| BS-4 | Documented pipeline/toolchain in BUILD_RECORD |
| New Release ID | `-v2` suffix; no hash.js of v1 hashes |

**Explicit deferral rationale:** No pre-compiled binaries exist in development repository; compile-from-source would require exposing proprietary trust-layer implementation subsetâ€”a boundary violation without explicit author enumeration.

---

## 3. Research Extensions (STF / extended governance evaluation model (theoretical))

| Direction | Description |
|-----------|-------------|
| External review of extended governance evaluation model (theoretical) v1.0 | Academic falsification per external falsification protocol (research) protocol |
| TD(t) operationalization | Move Trust Distance from experimental to measurable |
| ContinuityTrust empirical bridge | Connect epistemological extension to STF predicates |
| Hardware attestation integration | Explore TEE/TPM complementarity (not equivalence claim) |
| Multi-tenant trust isolation | Formal model for MSP deployment contexts |

---

## 4. Governance Hardening

| Enhancement | Purpose |
|-------------|---------|
| Manifest signing workflow (OQ-4) | Strengthen provenance layer |
| Reproducible clean-room across hosts | Multi-environment assembly verification |
| Automated whitelist drift detection | Prevent silent scope expansion |
| OQ gate automation (tracking only) | Surface stale open questions; not auto-close |
| Partner feedback loop | Structured evaluation template (EVALUATION_TEMPLATE.md) |

---

## 5. Publication Path (Zenodo)

Metadata prepared in `04_METADATA_ZENODO/`. DOI assignment pending deposit of documentation package (not productive code). See DOI_PLACEHOLDER.md.

---

## 6. Explicit Non-Goals

The following are **out of scope** for CEB v1 future work:

- Public release of proprietary server implementation/proprietary client implementation/proprietary trust-layer implementation source
- Offensive security tooling or external scanning automation
- Compliance certification claims
- Legacy v1.22.0 artifact rehabilitation
- Plugin premium/backend inclusion without independent V2-G audit

---

## 7. Success Criteria for v1.0 Completion

CEB v1.0 (Option A) may be considered complete when:

1. All integrity manifests generated and coherent.
2. Gate and V2 audit pass without CRITICAL/HIGH findings.
3. OQ-3, OQ-4, OQ-5 closed or explicitly waived with documentation.
4. SRO delivery authorization recorded.
5. External evaluator can verify package integrity independently via SHA256_MANIFEST.

Until then, **non-execution and concurrent blocking states remain valid outcomes.**

---

_FUTURE_WORK.md â€” CEB v1 â€” 2026-06-30_

# Limitations

**Document:** CEB v1 Research Paper — Declared Limitations  
**Publication version:** v1.0-CEB-RELEASE (frozen research snapshot)  
**Date:** 2026-06-30  
**Sources:** external audit package (category), research disclaimer document (category), CEB governance model

---

## Governing Clause

> *"This defines behavior under degraded trust; it does not assert impossibility of compromise."*

---

## 1. Trust Fabric Research Limitations

### Does NOT Claim

1. **Absolute invulnerability** — models degradation response, not impossibility of attack.
2. **Regulatory certification** — does not substitute SOC 2, Common Criteria, FedRAMP, or ISO 27001.
3. **Superiority over Zero Trust, SLSA, TPM/TEE** — complementary positioning only.
4. **Resistance to total adversary control** — root compromise across keys and runtime simultaneously.
5. **Autonomous self-sufficient identity** — requires external distinguisher (AAT axiom).
6. **Ontological truth** — `Provenance.complete ⊄ Reality.true`.
7. **Substitution of human governance** — SRO approval remains mandatory for CEB delivery.
8. **Implicit intent measurement** — AVI operates on declared intent only.
9. **Certifiable TD(t)/IIS(t) metrics** — experimental constructs.
10. **Sandbox empirical scope validates extended governance evaluation model (theoretical)** — separate scopes explicitly documented.
11. **Autonomous recovery after total trust collapse** — ANCR requires external evidence.

---

## 2. CEB v1 Package Limitations

| Limitation | Description |
|------------|-------------|
| **No productive code** | Evaluators cannot inspect proprietary implementation |
| **Option A only (v1.0)** | No functional binaries in frozen snapshot |
| **No plugins** | Zero extensibility surface in publication artifact |
| **Manifest templates only** | integrity/ schemas documented; live manifests not generated — valid non-execution posture |
| **Category model frozen** | Ingress categories defined; per-item enumeration gates documented at research level (OQ-1) |
| **Adversarial review criteria frozen** | V2 criteria documented; artifact verification not applicable to non-executable snapshot |
| **Structural validation gate** | Conceptual gate documented; not run on documentation-only artifact |
| **Delivery not authorized** | OQ-3, OQ-4, OQ-5 documented; no delivery sign-off in frozen snapshot |
| **Signature optional** | Provenance layer may be absent per governance model |

---

## 3. Clean-Room Limitations

1. Clean-room assembly does not prove absence of vulnerabilities in unreleased code.
2. Two JSON schemas copied from proprietary trust-layer implementation (not disclosed) are declarative only; no validator implementation included.
3. Secret scan uses lexical patterns; semantic secret embedding not exhaustively excluded.
4. Assembly report documents single-host context; multi-host reproducibility not claimed.

---

## 4. Empirical Scope Limits

| Scope | Limitation |
|-------|------------|
| Sandbox empirical scope | In-memory sandbox; not production deployment |
| extended governance evaluation model (theoretical) v1.0 | Theoretical freeze; external review at research level |
| Phase 1 boundary documentation | Documental only; no runtime evaluation harness included |
| External audit package | Documentary organization; no new empirical evidence |

---

## 5. Open Epistemic Challenges (STF)

| # | Challenge | Related axiom |
|---|-----------|---------------|
| 1 | Sovereign trust without external root? | AAT, ANCR |
| 2 | Honest suspension vs Denial-of-Trust? | AHS |
| 3 | Computationally measurable intent? | AVI |
| 4 | Identity vs historical convention? | ACI, AHP |
| 5 | Autonomous justification without human authority? | AAT |
| 6 | Operationalizable TD(t)/IIS(t)? | Metrics layer |

---

## 6. Partner Evaluation Limits

External evaluators reviewing CEB v1 documentation can:

- Assess research claims against evidence matrix
- Evaluate governance architecture completeness
- Falsify theoretical axioms per external falsification protocol (research) protocol

External evaluators **cannot** from this package alone:

- Verify runtime behavior of SentinelOps product
- Confirm production tenant isolation
- Validate live agent enrollment or approval workflows
- Certify supply-chain security of unreleased binaries

---

## 7. Non-Delivery as Limitation Acknowledgment

The frozen **v1.0-CEB publication artifact** (CEB v1 CLOSED; concurrent `AUTHORIZATION_READY_FOR_BUILD` + `REQUIRES_DESIGN_DECISION`; no delivery) is an **honest limitation disclosure**: the governance model permits external review of architecture and research framing without implying product readiness.

---

_LIMITATIONS.md — CEB v1 — v1.0-CEB-RELEASE — 2026-06-30_

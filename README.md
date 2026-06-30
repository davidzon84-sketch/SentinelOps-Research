# SentinelOps Research — Controlled Evaluation Boundary (CEB) v1

**Repository type:** Public research and governance documentation mirror  
**Release line (reference):** SentriOps Partner Evaluation v1.0 (`partner-eval-1.0.0`, provisional)  
**Version date:** 2026-06-30  

This repository is **not** a software product distribution. It publishes the **Controlled Evaluation Boundary (CEB) v1** documentation bundle: governance models, research framing, audit-evidence schemas, clean-room pipeline semantics, Zenodo metadata, and executive briefs. External readers can evaluate the **research and release-governance posture** without access to proprietary implementation code.

---

## What problem CEB addresses

Organizations that study **trust continuity**—how systems justify decisions when initial security assumptions degrade—need a way to share **research and governance artifacts** with external reviewers (partners, cloud security programs, academic archives) while **excluding** product source, secrets, customer data, and unreviewed binaries.

CEB v1 treats that separation as a **first-class architectural boundary**, not an afterthought.

---

## System architecture (conceptual)

CEB is a **documentation-only evaluation perimeter** around trust-continuity research. It does not describe or ship a runnable application from this mirror.

| Layer | Role in CEB v1 |
|-------|----------------|
| **Governance model** | Authorization states, open-question gates, and explicit human sign-off before any external delivery |
| **Research corpus** | Formal paper structure, limitations, and architecture narrative at the **research** level (not implementation) |
| **Audit evidence** | Schemas for build records, signatures, SHA-256 manifests, and execution traces—**templates**, not live operational logs |
| **Clean-room pipeline** | Whitelist-only ingress into an isolated assembly workspace; no recursive copy of proprietary trees |
| **Publication metadata** | Fields intended for Zenodo deposit and citation |
| **Executive summaries** | Non-technical and cloud-security-oriented briefs for program stakeholders |

**Proprietary evaluation engines** (internal risk, approval, or trust-runtime components) are **out of scope** for this mirror. The bundle explains *how release decisions are gated*, not *how product code is implemented*.

```
  [ Private development & product code ]     (never in this repo )
              |
              |  whitelist-only, human-gated
              v
  [ CEB v1 documentation bundle ]  ------>  Zenodo (frozen DOI snapshot)
              |
              +-------------------------->  GitHub (living governance reference)
```

---

## Non-execution as a valid state

CEB v1 encodes a deliberate principle:

> **Choosing not to build, compile, package, or deliver is a correct and often preferred security outcome** when boundary preconditions, open questions, or whitelist entries are incomplete.

Phase 1 clean-room preparation may complete **without** producing binaries or partner ZIPs. Open governance items (see `00_GOVERNANCE_MODEL/`) can keep **delivery unauthorized** while design and review continue. That posture is **success**, not stall.

See [`00_GOVERNANCE_MODEL/STATE_MACHINE.md`](./00_GOVERNANCE_MODEL/STATE_MACHINE.md).

---

## Repository layout (28 documents)

| Directory | Focus |
|-----------|---------|
| [`00_GOVERNANCE_MODEL/`](./00_GOVERNANCE_MODEL/) | Authorization model, state machine, OQ gates, design decisions |
| [`01_RESEARCH_PAPER/`](./01_RESEARCH_PAPER/) | Research paper sections (STF / trust-continuity framing) |
| [`02_AUDIT_EVIDENCE/`](./02_AUDIT_EVIDENCE/) | Evidence and trace **schemas** |
| [`03_CLEAN_ROOM_PIPELINE/`](./03_CLEAN_ROOM_PIPELINE/) | Phase 1 executed, Phase 2 pending, whitelist policy |
| [`04_METADATA_ZENODO/`](./04_METADATA_ZENODO/) | Deposit title, authors, keywords, version, license notes |
| [`05_EXECUTIVE_SUMMARY/`](./05_EXECUTIVE_SUMMARY/) | Microsoft Research, AWS Security, and non-technical briefs |

---

## Dual publication: Zenodo + GitHub

| Channel | Purpose |
|---------|---------|
| **Zenodo** | Versioned, citable archive (DOI) of a **frozen** documentation snapshot |
| **GitHub** | Traceability for governance evolution, open-question resolution, and gate artifacts |

Neither channel alone **authorizes** partner delivery. Human Security Release Owner sign-off and closed gates remain required. Details: [`04_METADATA_ZENODO/`](./04_METADATA_ZENODO/) and governance docs in `00_GOVERNANCE_MODEL/`.

**License (this mirror):** See root [`LICENSE`](./LICENSE) (CC BY-NC 4.0). Zenodo deposit license notes may reference CC BY 4.0 for the archival record—reconcile at deposit time with [`04_METADATA_ZENODO/LICENSE.md`](./04_METADATA_ZENODO/LICENSE.md).

---

## What this repository explicitly excludes

- Product application source code and installers  
- Runnable services, plugins, or evaluation binaries (v1.0 is documentation-only; Option A)  
- Secrets, credentials, customer data, or internal operational paths  
- Claims of certification, compliance attestation, SIEM/EDR replacement, or breach prevention guarantees  

Honest limitations: [`01_RESEARCH_PAPER/LIMITATIONS.md`](./01_RESEARCH_PAPER/LIMITATIONS.md).

---

## Program status snapshot (2026-06-30)

Governance design for CEB v1 is **closed** at the documentation level; **delivery to external partners is not authorized** while selected open questions remain. Treat status tables inside the bundle as authoritative for gate IDs (OQ-1 through OQ-6).

---

## Citation

When citing this work, prefer the Zenodo DOI once assigned ([`04_METADATA_ZENODO/DOI_PLACEHOLDER.md`](./04_METADATA_ZENODO/DOI_PLACEHOLDER.md)). Until then, cite this GitHub repository and commit SHA.

---

_SentinelOps Research — CEB v1 public documentation mirror._

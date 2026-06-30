# SentinelOps Research — Controlled Evaluation Boundary (CEB) v1

**Repository type:** Public **research and governance** documentation (not software)  
**Release line (reference):** SentriOps Partner Evaluation v1.0 (`partner-eval-1.0.0`, provisional)  
**Version date:** 2026-06-30  

This repository is **not deployable**. It does not install, run, or operate any product. It publishes the **Controlled Evaluation Boundary (CEB) v1** model: how trust-continuity **research** may be shared under explicit **governance, auditability, and control boundaries**—without disclosing proprietary implementation.

---

## Academic and architectural purpose

Readers evaluate a **conceptual system architecture** and **execution-control governance model** suitable for external review (partners, cloud security programs, Zenodo citation). No algorithms, pseudocode, automation logic, or operational steps sufficient to reconstruct runtime behavior are included.

---

## System architecture (high level)

| Plane | Research role |
|-------|----------------|
| **Governance** | Open-question gates, state machine, Security Release Owner authority |
| **Boundary** | Authorized ingress categories and denylists (abstract) |
| **Clean-room** | Isolation principles between private development and evaluation perimeter |
| **Evidence** | Schemas for manifests, build records, signatures, and traces (**templates only**) |
| **Research** | Trust-continuity framing, limitations, honest non-claims |
| **Publication** | Zenodo metadata for DOI deposit |

```
  [ Private implementation — not published ]
              |
              |  human-gated boundary (documentation only)
              v
  [ CEB v1 research mirror ]  ------>  Zenodo (citable snapshot)
              |
              +---------------------->  GitHub (governance reference)
```

**Governance evaluation framework:** release progression is modeled as **states and attestations**, not as disclosed product engines.

---

## Non-execution as a valid state

> **Choosing not to compile, package, or deliver remains a correct security and governance outcome** when preconditions or open questions are unresolved.

See [`00_GOVERNANCE_MODEL/STATE_MACHINE.md`](./00_GOVERNANCE_MODEL/STATE_MACHINE.md).

---

## Layout

| Directory | Focus |
|-----------|---------|
| [`00_GOVERNANCE_MODEL/`](./00_GOVERNANCE_MODEL/) | Authorization, OQ gates, state machine |
| [`01_RESEARCH_PAPER/`](./01_RESEARCH_PAPER/) | Research sections (architectural, not implementation) |
| [`02_AUDIT_EVIDENCE/`](./02_AUDIT_EVIDENCE/) | Auditability **schemas** |
| [`03_CLEAN_ROOM_PIPELINE/`](./03_CLEAN_ROOM_PIPELINE/) | Boundary ingress **research records** |
| [`04_METADATA_ZENODO/`](./04_METADATA_ZENODO/) | Deposit metadata |
| [`05_EXECUTIVE_SUMMARY/`](./05_EXECUTIVE_SUMMARY/) | Executive briefs |

---

## License and dual publication

**License:** [CC BY 4.0](./LICENSE) — aligned with [`04_METADATA_ZENODO/LICENSE.md`](./04_METADATA_ZENODO/LICENSE.md).

| Channel | Role |
|---------|------|
| **Zenodo** | Versioned DOI archive |
| **GitHub** | Living governance reference |

Neither channel authorizes partner delivery without human sign-off per governance docs.

---

## Explicit exclusions

Product source, installers, runnable services, secrets, customer data, certification claims, and SIEM/EDR replacement claims.

---

## Citation

Prefer Zenodo DOI when assigned ([`04_METADATA_ZENODO/DOI_PLACEHOLDER.md`](./04_METADATA_ZENODO/DOI_PLACEHOLDER.md)); until then cite repository URL and commit SHA.

---

_SentinelOps Research — CEB v1 public research artifact — not a software release._

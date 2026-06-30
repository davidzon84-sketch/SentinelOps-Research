# Whitelist Policy

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Clean-room boundary — authorized ingress policy (research model)  
**Date:** 2026-06-30  
**Status:** **PENDING** — category model frozen; per-item enumeration requires SRO finalization  

---

## 1. Policy Statement

The **authorized ingress list** is the sole conceptual mechanism for allowing material to cross from private development into an isolated evaluation perimeter. Directory-level grants, recursive copy, and implicit inclusion are **prohibited**.

**Absence from the authorized list is a valid block.**

---

## 2. Selection Criteria

| ID | Criterion |
|----|-----------|
| C-1 | Indispensable for declared external evaluation scope |
| C-2 | No secrets or credential material |
| C-3 | No proprietary implementation trees (not disclosed) |
| C-4 | No prohibited origin classes |
| C-5 | IP bounded |
| C-6 | Explicit enumeration — no directory grants |

---

## 3. Authorized Ingress Categories (Option A — Abstract)

| Category | Architectural role |
|----------|-------------------|
| Contractual framing | Package identity and evaluation terms |
| Declarative schemas | Interoperable JSON schema excerpts (category only) |
| Evaluation templates | Structured reviewer findings |
| External audit excerpts | Third-party review framing |
| Curated research | Trust-continuity paper excerpts |

**Reference scale:** on the order of 26 documentation slots; enumeration pending OQ-1.

---

## 4. Absolute Exclusions

Proprietary implementation, unpublished archives, secrets, legacy product artifacts, and operational automation are **architecturally excluded** from public reconstruction.

---

_Whitelist Policy — CEB v1 research model — 2026-06-30_

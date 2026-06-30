# AWS Security Brief â€” CEB v1 Supply-Chain and Release Governance

**Audience:** AWS Security / Infrastructure teams â€” supply-chain, release engineering, partner evaluation  
**Classification:** Security architecture brief  
**Date:** 2026-06-30  
**Author:** David Baldizon

---

## Executive Summary

CEB v1 defines a **defensive release boundary** for sharing SentinelOps trust-continuity research with external evaluators. The model prioritizes supply-chain integrity, minimum attack surface, and human authorization over execution velocity. v1.0 ships documentation only (Option A); binaries deferred until explicit v2 authorization.

---

## Supply-Chain Threat Model (Release Context)

| Threat | CEB control |
|--------|-------------|
| Unauthorized code in artifact | Whitelist (26 files); no recursive repo copy |
| Secret exfiltration via package | Pre-copy denylist; lexical secret scan (Phase 1.1 PASS) |
| Artifact tampering post-release | SHA-256 per-file + ZIP hash in DELIVERY_MANIFEST |
| Unauthorized delivery | SRO approval gate; READY_FOR_EXTERNAL_REVIEW â‰  delivery |
| Legacy compromised artifact reuse | v1.22.0 blocked; discontinuity enforced |
| Scope expansion without audit | REQUIRES_DESIGN_DECISION blocking state |

---

## Build Integrity Architecture

Three orthogonal layers:

1. **Integrity (SHA-256)** â€” detects modification
2. **Provenance (optional signature)** â€” attributes manifest generation
3. **Authorization (human)** â€” records permitted delivery

Confusing these layers invalidates the evidence chain â€” analogous to conflating S3 object integrity, code signing, and change advisory board approval in cloud release pipelines.

---

## Clean-Room Isolation (AWS Parallel)

| CEB concept | Cloud infrastructure analog |
|-------------|----------------------------|
| Clean-room workspace | Isolated build account / separate partition |
| Whitelist ingress | IAM resource policy allow-list |
| Denylist | SCP deny rules for prohibited paths |
| BUILD_RECORD | CodePipeline / CodeBuild audit trail |
| Gate exit 0 | Automated compliance check (Config, custom policy) |
| SRO approval | Manual approval stage before production deploy |
| Non-execution | Change freeze when CAB input incomplete |

---

## Governance Reduces Execution Risk

CEB v1 demonstrates that **not building** is correct when:

- No verified binaries exist in source repository
- Compile inputs are not enumerated
- IP co-approval (OQ-3) is unresolved
- Whitelist is absent or incomplete

This prevents a common supply-chain failure mode: shipping artifacts assembled under implicit scope from development environments.

Phase 2 (compile/strip) remains **PENDING** â€” intentionally not executed for v1.0.

---

## Partner Evaluation Surface (Option A)

| Included | Excluded |
|----------|----------|
| 8 external audit research docs | proprietary server implementation/, proprietary client implementation/, proprietary trust-layer implementation/ source |
| 5 curated research papers | Plugins (all categories) |
| 2 public JSON schemas | Docker product stack |
| Threat model + evaluation template | Legacy install scripts |
| Contractual placeholders | Secrets, CI internals |

Minimum attack surface: no executables, no plugin extensibility, no infrastructure deployment scripts.

---

## Operational Status

```
CEB v1 cycle:          CLOSED
Operational states:    AUTHORIZATION_READY_FOR_BUILD + REQUIRES_DESIGN_DECISION
Phase 1:               EXECUTED (6 skeleton files)
Proposed whitelist:    26 routes (PENDING finalization)
V2 review:             COMPLETED
Manifests:             Not generated (valid)
Automated gate:        Not executed (valid)
Delivery:              NOT AUTHORIZED
SRO:                   David Baldizon
Open OQ:               OQ-1 (identity), OQ-3 (IP), OQ-4 (signature), OQ-5 (plugins)
```

---

## AWS-Relevant Review Questions

1. Does the whitelist-denylist model provide sufficient supply-chain assurance for documentation-only artifacts?
2. Is the three-layer integrity model correctly separated for evaluator independence?
3. What additional controls would apply if Option B binaries are added (v2)?
4. How should DELIVERY_MANIFEST.security_status integrate with partner onboarding workflows?

---

## Explicit Non-Claims

- Not AWS service integration documentation
- Not AWS security certification
- Not production deployment guide for SentinelOps on AWS
- Does not replace customer-side security review of any future binary artifacts

---

_AWS Security Brief â€” CEB v1 â€” 2026-06-30_

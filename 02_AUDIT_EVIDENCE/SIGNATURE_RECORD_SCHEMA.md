# SIGNATURE_RECORD Schema

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Audit Evidence â€” Human Authorization Record Specification  
**Date:** 2026-06-30  
**Source template:** internal governance template (not published)

---

## 1. Purpose

The SIGNATURE_RECORD (operational) and `integrity/APPROVAL_RECORD.md` (in-package) document **human authorization** for release delivery. This layer answers: did an authorized Security Release Owner permit external distribution of this artifact?

Authorization is **orthogonal** to SHA-256 integrity and optional manifest signatures.

---

## 2. Document Locations

| Document | Location | Audience |
|----------|----------|----------|
| SIGNATURE_RECORD | `internal release governance archive/reports/` or audit archive | Internal operations |
| APPROVAL_RECORD | `integrity/APPROVAL_RECORD.md` inside ZIP | External evaluator |

Both must be coherent. SIGNATURE_RECORD may contain operational notes excluded from partner package.

---

## 3. Schema: SRO Identity

| Field | Type | Required | CEB v1.0 Value |
|-------|------|----------|----------------|
| `sro_name` | string | Yes | David Baldizon |
| `sro_role` | string | Yes | Project Owner (SentinelOps OS) |
| `sro_function` | string | Yes | Security Release Owner |

---

## 4. Schema: Artifact Identity

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `artifact_name` | string | Yes | ZIP filename |
| `release_id` | string | Yes | SOPS-CEB-RELEASE-YYYY-MM-DD-vN |
| `version` | semver | Yes | v1.0-CEB-RELEASE |
| `artifact_sha256` | hex | Yes | SHA-256 of complete ZIP or DELIVERY_MANIFEST reference |

**Coherence rule:** `artifact_sha256` must match `DELIVERY_MANIFEST.json` zip hash field.

---

## 5. Schema: Authorization Declaration

Fixed declaration text (hash substituted at signing):

> Autorizo la liberaciÃ³n del artefacto de evaluaciÃ³n identificado bajo el hash **[HASH]** tras verificar que cumple con los criterios de no-exposiciÃ³n, ausencia de secretos y alineaciÃ³n con la polÃ­tica de mÃ­nima superficie de ataque del CEB v1.

English equivalent accepted for international review:

> I authorize release of the evaluation artifact identified under hash **[HASH]** after verifying non-exposure criteria, absence of secrets, and alignment with CEB v1 minimum attack surface policy.

---

## 6. Schema: Signature Block

| Field | Type | Required | Constraints |
|-------|------|----------|-------------|
| `signature_type` | enum | Yes | `digital`, `physical` |
| `public_key_reference` | string | If digital | Reference only â€” **no private key** |
| `signature_payload` | string | Yes | Signature or archival reference |
| `signature_timestamp_utc` | ISO 8601 | Yes | UTC mandatory |

### Prohibited Content

- Private keys (`*.pem`, `*.key`)
- JWT or session tokens
- Passwords or API keys

---

## 7. Schema: Preconditions Checklist

All must be checked before signing:

| # | Precondition | Field |
|---|--------------|-------|
| 1 | BUILD_RECORD complete | `preconditions.build_record: true` |
| 2 | structural validation gate attestation (conceptual) | `preconditions.gate_exit_0: true` |
| 3 | V2 audit no CRITICAL/HIGH | `preconditions.v2_clean: true` |
| 4 | DELIVERY_MANIFEST zip hash verified | `preconditions.delivery_hash: true` |
| 5 | Scope option documented | `preconditions.scope_documented: true` |
| 6 | Zero plugins (v1.0) | `preconditions.no_plugins: true` |
| 7 | No productive source exposed | `preconditions.no_source: true` |
| 8 | OQ-3, OQ-4, OQ-5 closed or waived | `preconditions.oq_delivery_closed: true` |

---

## 8. Schema: APPROVAL_RECORD (In-Package Variant)

Minimal fields for partner-visible record:

```yaml
release_id: SOPS-CEB-RELEASE-2026-06-30-v1
version: v1.0-CEB-RELEASE
approval_date_utc: [ISO 8601]
sro_name: David Baldizon
sro_role: Security Release Owner
verdict: APPROVED | REJECTED
scope_option: A
open_questions_status: [OQ-3, OQ-4, OQ-5 resolution summary]
notes: [optional bounded text]
```

---

## 9. State Contribution

| Condition | Maximum achievable state |
|-----------|-------------------------|
| No SIGNATURE_RECORD / APPROVAL_RECORD | `READY_FOR_EXTERNAL_REVIEW` |
| Complete sign-off + all preconditions | `APPROVED_FOR_DELIVERY` |
| REJECTED verdict | `BLOCKED_PENDING_REMEDIATION` |

**Invariant:** Hash verification alone cannot elevate state to `APPROVED_FOR_DELIVERY`.

---

## 10. Current Status

| Field | Status |
|-------|--------|
| SRO designated | Yes (OQ-2 closed) |
| SIGNATURE_RECORD completed | **No** â€” pending gate + audit |
| APPROVAL_RECORD in package | **No** â€” not yet generated |
| Delivery authorized | **No** |

---

_SIGNATURE_RECORD Schema â€” CEB v1 â€” 2026-06-30_

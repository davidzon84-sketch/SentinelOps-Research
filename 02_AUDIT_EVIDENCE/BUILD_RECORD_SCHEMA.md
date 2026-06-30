# BUILD_RECORD Schema

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Audit Evidence â€” Operational Build Record Specification  
**Date:** 2026-06-30  
**Source template:** internal governance template (not published)

---

## 1. Purpose

The BUILD_RECORD documents **operational provenance** of a clean-room assembly or build. It answers: who assembled what, from where, under which scope, with what exclusions, and with what gate results.

The BUILD_RECORD is **not** a substitute for:
- `integrity/SHA256_MANIFEST.txt` (per-file integrity)
- `integrity/RELEASE_MANIFEST.json` (structured inventory)
- `integrity/APPROVAL_RECORD.md` (human delivery authorization)

**Location convention:** internal audit archive (not published)

---

## 2. Schema: Identity Block

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `build_id` | string | Yes | Unique build execution identifier |
| `release_id` | string | Yes | Format: `SOPS-CEB-RELEASE-YYYY-MM-DD-vN` |
| `version` | semver | Yes | Must be `v1.0-CEB-RELEASE` for CEB v1.0 line |
| `zip_target_name` | string | Conditional | Required if ZIP generated |
| `scope_option` | enum | Yes | `A` (documental) or `B` (binaries) |
| `status` | enum | Yes | `PENDING`, `IN_PROGRESS`, `COMPLETE` |

---

## 3. Schema: Clean-Room Workspace

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `clean_room_path` | path | Yes | Isolated workspace location |
| `start_timestamp_utc` | ISO 8601 | Yes | Assembly/build start |
| `end_timestamp_utc` | ISO 8601 | On complete | Assembly/build end |
| `prohibited_origin_verified` | boolean[3] | Yes | No dev tree, no forensic workspace, no legacy ZIP |

### Prohibited Origin Checklist

- [ ] No development repository working tree as direct source
- [ ] No `internal audit workspace/`
- [ ] No legacy `legacy partner artifact (discontinued)`

---

## 4. Schema: Source Snapshot

### 4.1 Included Categories

| Category | Option A (v1.0) | Option B (deferred) |
|----------|-----------------|---------------------|
| Contractual skeleton | Yes (6 files) | Yes |
| Public JSON schemas | Yes (2 files) | Yes |
| Partner documentation | Yes (17 files) | Yes |
| Functional binaries | **No** | Yes (enumerated) |
| Generated integrity files | At BUILD phase | At BUILD phase |

### 4.2 Excluded Categories (mandatory verification)

| Category | Verification field |
|----------|-------------------|
| Productive source | `excluded.productive_source: PASS/FAIL` |
| Plugins | `excluded.plugins: PASS/FAIL` |
| Diagnostic executables | `excluded.diagnostics: PASS/FAIL` |
| Secrets | `excluded.secrets: PASS/FAIL` |
| Legacy origin | `excluded.legacy: PASS/FAIL` |
| Denylist contractual | `excluded.denylist: PASS/FAIL` |

---

## 5. Schema: Toolchain

Not applicable in this public research artifact (Option A). Operational toolchain classes remain private.

---

## 6. Schema: Compile Flags (Option B only)

| Flag | Required value |
|------|----------------|
| `strip_symbols` | true |
| `no_debug_paths` | true |
| `minimal_debug_metadata` | true |
| `denylist_pre_copy` | true |

---

## 7. Schema: Binary Inventory (Option B only)

| Column | Type | Description |
|--------|------|-------------|
| `#` | integer | Row index |
| `package_path` | string | Relative path in deliverable |
| `functional_purpose` | string | Documented evaluation purpose (abstract) |
| `sha256_post_strip` | hex | Hash after strip |
| `strip_applied` | boolean | Must be true |

Option A: single row â€” `application/README.md` placeholder; no binaries.

---

## 8. Schema: Gate Results (Conceptual)

| Field | Type | Description |
|-------|------|-------------|
| `gate_id` | string | Governance gate identifier |
| `result` | enum | `PASS` / `FAIL` / `NOT_RUN` |
| `attested_by` | string | Human or recorded validation role |
| `timestamp_utc` | ISO 8601 | Attestation time |

No operational automation or script identifiers are published in this mirror.

---

## 9. Schema: Operator Block

| Field | Type | Required |
|-------|------|----------|
| `operator_identity` | string | Yes |
| `operator_role` | string | Yes (e.g., Build Operator) |
| `sro` | string | Yes â€” David Baldizon |
| `record_date` | date | Yes |

---

## 10. Schema: Output Hashes

| Field | Type | Phase |
|-------|------|-------|
| `inventory_sha256_generated` | boolean | BUILD |
| `zip_sha256` | hex | POST-ZIP |
| `version_coherence` | boolean | BUILD â€” all version fields match |

---

## 11. State Contribution

| BUILD_RECORD.status | Contributes to state |
|---------------------|---------------------|
| `IN_PROGRESS` | `BUILD_IN_PROGRESS` |
| `COMPLETE` + manifests | `BUILD_VALIDATED` candidate |

Incomplete BUILD_RECORD blocks transition to `BUILD_VALIDATED`.

---

## 12. Phase 1.1 Reference Values (Option A)

| Field | Value (2026-06-30) |
|-------|-------------------|
| `release_id` | `SOPS-CEB-RELEASE-2026-06-30-v1` |
| `scope_option` | A |
| `files_copied` | 26 |
| `files_missing` | 0 |
| `compilation` | Not executed |
| `zip_sha256` | Not generated |
| `status` | Assembly complete; BUILD_RECORD formal generation pending |

---

_BUILD_RECORD Schema â€” CEB v1 â€” 2026-06-30_

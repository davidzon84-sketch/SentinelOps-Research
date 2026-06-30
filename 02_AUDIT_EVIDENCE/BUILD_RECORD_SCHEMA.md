# BUILD_RECORD Schema

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Audit Evidence — Operational Build Record Specification  
**Date:** 2026-06-30  
**Source template:** `partner-release/templates/BUILD_RECORD.md`

---

## 1. Purpose

The BUILD_RECORD documents **operational provenance** of a clean-room assembly or build. It answers: who assembled what, from where, under which scope, with what exclusions, and with what gate results.

The BUILD_RECORD is **not** a substitute for:
- `integrity/SHA256_MANIFEST.txt` (per-file integrity)
- `integrity/RELEASE_MANIFEST.json` (structured inventory)
- `integrity/APPROVAL_RECORD.md` (human delivery authorization)

**Location convention:** `partner-release/reports/BUILD_RECORD_<ReleaseID>.md` (outside deliverable ZIP).

---

## 2. Schema: Identity Block

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `build_id` | string | Yes | Unique build execution identifier |
| `release_id` | string | Yes | Format: `SOPS-PARTNER-EVAL-YYYY-MM-DD-vN` |
| `version` | semver | Yes | Must be `partner-eval-1.0.0` for CEB v1.0 line |
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
- [ ] No `PARTNER_SECURITY_AUDIT/workspace/`
- [ ] No legacy `SentinelOPS_OS_Partner_Release_v1.22.0.zip`

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

## 5. Schema: Toolchain (Option B only)

| Field | Type | Required (B) | Description |
|-------|------|--------------|-------------|
| `compiler` | string | Yes | Compiler identity and version |
| `linker` | string | Conditional | If applicable |
| `strip_tool` | string | Yes | Symbol stripping tool |
| `build_host_os` | string | Yes | Host operating system |
| `python_version` | string | For gates | Gate script runtime |

For Option A: toolchain block marked `N/A — documental assembly only`.

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
| `functional_purpose` | string | Trust Fabric / SARP-OMEGA eval justification |
| `sha256_post_strip` | hex | Hash after strip |
| `strip_applied` | boolean | Must be true |

Option A: single row — `application/README.md` placeholder; no binaries.

---

## 8. Schema: Gate Results

| Gate | Field | Type |
|------|-------|------|
| `audit_partner_package.py` | `exit_code` | integer |
| | `timestamp_utc` | ISO 8601 |
| | `report_path` | path |
| `partner_release_gate.py` | `exit_code` | integer (must be 0 for progression) |
| | `timestamp_utc` | ISO 8601 |
| | `report_path` | path |

---

## 9. Schema: Operator Block

| Field | Type | Required |
|-------|------|----------|
| `operator_identity` | string | Yes |
| `operator_role` | string | Yes (e.g., Build Operator) |
| `sro` | string | Yes — David Baldizon |
| `record_date` | date | Yes |

---

## 10. Schema: Output Hashes

| Field | Type | Phase |
|-------|------|-------|
| `inventory_sha256_generated` | boolean | BUILD |
| `zip_sha256` | hex | POST-ZIP |
| `version_coherence` | boolean | BUILD — all version fields match |

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
| `release_id` | `SOPS-PARTNER-EVAL-2026-06-30-v1` |
| `scope_option` | A |
| `files_copied` | 26 |
| `files_missing` | 0 |
| `compilation` | Not executed |
| `zip_sha256` | Not generated |
| `status` | Assembly complete; BUILD_RECORD formal generation pending |

---

_BUILD_RECORD Schema — CEB v1 — 2026-06-30_

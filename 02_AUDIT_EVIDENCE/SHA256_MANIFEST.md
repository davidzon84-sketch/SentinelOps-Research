# SHA256 Manifest Specification

**Boundary:** Controlled Evaluation Boundary v1  
**Document type:** Audit Evidence — Integrity Manifest Format  
**Date:** 2026-06-30

---

## 1. Purpose

The SHA256 manifest provides **independent, tool-agnostic integrity verification** of every file in the partner evaluation package. Evaluators can verify content without parsing JSON or trusting structured manifest generators.

---

## 2. Artifacts in Integrity Layer

| File | Format | Primary question |
|------|--------|------------------|
| `SHA256_MANIFEST.txt` | Plain text | Per-file integrity |
| `RELEASE_MANIFEST.json` | JSON | Structured inventory + metadata |
| `DELIVERY_MANIFEST.json` | JSON | Complete ZIP hash + security_status |
| `VERSION` | Plain text | Single version string |

---

## 3. SHA256_MANIFEST.txt Format

### 3.1 Line Format

```
<SHA256_HEX>  <RELATIVE_PATH>
```

- Hash: lowercase hexadecimal, 64 characters (SHA-256)
- Separator: two spaces between hash and path
- Path: forward slashes; relative to package root
- Sort order: lexicographic by path (recommended for reproducibility)
- Encoding: UTF-8, LF line endings

### 3.2 Example (Illustrative — Phase 1.1 partial)

```
32ed59c43236551eb6789c09b0e44d06c5dfa5c258c27fb0884042cb261ee99d  README_FIRST
96ca46bff2a8c51ca4f62b30ad4a0c9dea508bdd1f428e7546410a15129d2889  LICENSE
bb92629bdf608640cd0f3a147b104f74f632c95c75313f5a8f63fdd4be3bd628  application/README.md
...
```

Phase 1 executed with 6 skeleton files. Proposed 26-route whitelist pending finalization. Full package manifest **not generated** — valid under concurrent `REQUIRES_DESIGN_DECISION` state.

### 3.3 Exclusions from Manifest

- The manifest file itself (avoid circular hash)
- Optional: `DELIVERY_MANIFEST.json` if generated post-ZIP (document policy in BUILD_RECORD)

---

## 4. RELEASE_MANIFEST.json Schema

```json
{
  "release_id": "SOPS-PARTNER-EVAL-2026-06-30-v1",
  "version": "partner-eval-1.0.0",
  "generated_at_utc": "2026-06-30T00:00:00Z",
  "scope_option": "A",
  "files": [
    {
      "path": "README_FIRST",
      "sha256": "32ed59c43236551eb6789c09b0e44d06c5dfa5c258c27fb0884042cb261ee99d",
      "category": "contractual"
    }
  ],
  "file_count": 26,
  "notes": "Option A documental assembly; no binaries"
}
```

### Required top-level fields

| Field | Type | Required |
|-------|------|----------|
| `release_id` | string | Yes |
| `version` | string | Yes |
| `generated_at_utc` | ISO 8601 | Yes |
| `scope_option` | A \| B | Yes |
| `files` | array | Yes |
| `file_count` | integer | Yes |

---

## 5. DELIVERY_MANIFEST.json Schema

```json
{
  "release_id": "SOPS-PARTNER-EVAL-2026-06-30-v1",
  "version": "partner-eval-1.0.0",
  "artifact_name": "SentriOps_Partner_Evaluation_partner-eval-1.0.0.zip",
  "zip_sha256": "[hex — post ZIP generation]",
  "packaged_at_utc": "[ISO 8601]",
  "security_status": "pending",
  "notes": "Hash proves artifact integrity, not security absolute"
}
```

### security_status Values

| Value | Meaning |
|-------|---------|
| `pending` | Gate/audit/approval incomplete |
| `ready_for_review` | Gate + V2 pass; approval pending |
| `approved` | SRO sign-off complete |
| `blocked` | Remediation required |

---

## 6. VERSION File

Single line, no trailing whitespace:

```
partner-eval-1.0.0
```

---

## 7. Verification Procedure (Evaluator)

```bash
# Unix-like systems
sha256sum -c SHA256_MANIFEST.txt

# Manual single file
sha256sum README_FIRST
```

Evaluator compares output to manifest entries. Mismatch → integrity failure; does not alone imply authorization status.

---

## 8. Coherence Constraints

All must match:

```
ZIP_filename.version == VERSION == RELEASE_MANIFEST.version == DELIVERY_MANIFEST.version
```

Violation triggers `BLOCKED_PENDING_REMEDIATION`; requires new Release ID.

---

## 9. Optional Signature Extension (OQ-4)

If manifest signing approved:

| File | Content |
|------|---------|
| `RELEASE_MANIFEST.json.sig` | Signature over canonical JSON |
| Embedded public key | In documentation/ or integrity/ |

Private signing key **never** in package.

---

## 10. Current Status

| Artifact | Status |
|----------|--------|
| Phase 1.1 per-file hashes | Documented in PHASE_1.md |
| integrity/SHA256_MANIFEST.txt | **Pending generation** |
| RELEASE_MANIFEST.json | **Pending** |
| DELIVERY_MANIFEST.json | **Pending** (requires ZIP) |
| VERSION | **Pending** |

---

_SHA256 Manifest Specification — CEB v1 — 2026-06-30_

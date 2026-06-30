# Integrity Verification Report — SentinelOps-Research Mirror

**Generated:** 2026-06-30  
**Source bundle:** `internal CEB assembly bundle/` (filesystem copy only; no productive repo clone)  
**Destination:** `this public research mirror/`  
**Initial commit:** `fb6e2178c26c19b60bec9ebbf3fd9432437750e7`

---

## 1. File count verification

| Check | Result |
|-------|--------|
| Source CEB files | **28** (expected) |
| Mirror tracked files (git) | **29** (28 CEB paths + root `LICENSE`) |
| Hidden dirs from source (`.git`, `.vscode`, `.idea`) | **None copied** (new independent `.git` at mirror only) |

---

## 2. Sanitization

| Check | Result |
|-------|--------|
| `[redacted-internal-path]/` / `[redacted-internal-path]/` in `.md` | **PASS** — no matches after scan |
| `internal CEB assembly bundle/` internal package roots | **PASS** — replaced with neutral bundle references in affected files |
| Root `README.md` | **PASS** — rewritten for public GitHub (intentional DIFF) |
| Governance references to excluded product trees | **PASS** — retained as policy concepts in bundle docs (not operational paths) |

**Sanitization overall:** **PASS**

---

## 3. Security scan (lexical)

Patterns searched: `token`, `secret`, `key`, `password`, `login`, `local-only development URLs`

| Finding | Triage |
|---------|--------|
| Multiple hits on *secret*, *key*, *password*, *token* | **False positives** — governance denylist, schema field names, Zenodo keywords, bilingual approval templates with `[HASH]` placeholders |
| `local-only development URLs` | **No hits** |
| Embedded credentials / API values | **None found** |

**Security scan:** **PASS** (no abort; no CRITICAL credentials)

---

## 4. SHA256 — source vs mirror (CEB 28 files)

| Relative path | Source SHA256 | Mirror SHA256 | Status |
|---------------|---------------|---------------|--------|
| 00_GOVERNANCE_MODEL/CEB_V1_RELEASE_AUTHORIZATION_MODEL.md | 5576b2dd38301b6f9065f1310a4ba0a73421b47aec6f9d8115842d3cdf1f78a3 | 5576b2dd38301b6f9065f1310a4ba0a73421b47aec6f9d8115842d3cdf1f78a3 | MATCH |
| 00_GOVERNANCE_MODEL/DESIGN_DECISIONS.md | 1557fea87ea62b298b6d48eed803c457d21d2f73a127d03bf22ed371c0c3b952 | 1557fea87ea62b298b6d48eed803c457d21d2f73a127d03bf22ed371c0c3b952 | MATCH |
| 00_GOVERNANCE_MODEL/OQ_GATES_MODEL.md | fb3e7bebeb82ee56e09c03180a4cba7a35bf975902c2601971259fd327a81424 | fb3e7bebeb82ee56e09c03180a4cba7a35bf975902c2601971259fd327a81424 | MATCH |
| 00_GOVERNANCE_MODEL/STATE_MACHINE.md | 1424beccede25d773ee0309efe3578f9c6f38701b3a14af9200397fa9302e01e | 1424beccede25d773ee0309efe3578f9c6f38701b3a14af9200397fa9302e01e | MATCH |
| 01_RESEARCH_PAPER/ABSTRACT.md | 32da65bed55b38df14fd7c8f3e77b83335226e7c84862e3906ab150d5ea8b35b | 32da65bed55b38df14fd7c8f3e77b83335226e7c84862e3906ab150d5ea8b35b | MATCH |
| 01_RESEARCH_PAPER/ARCHITECTURE.md | 17383c6be7c97ecb10c091b8f9196275243329633f72e08f7e256dc986e3aa90 | 17383c6be7c97ecb10c091b8f9196275243329633f72e08f7e256dc986e3aa90 | MATCH |
| 01_RESEARCH_PAPER/FUTURE_WORK.md | e289de311af48d22032cc974db84afdbcd1878b8e3a6362ee95bed9ae8f1acdf | e289de311af48d22032cc974db84afdbcd1878b8e3a6362ee95bed9ae8f1acdf | MATCH |
| 01_RESEARCH_PAPER/INTRODUCTION.md | 0d4b7a8c812ad3c044144dcbf1183aa01030cbf72cda6ef8bf6a3ad4e9c9c9df | 0d4b7a8c812ad3c044144dcbf1183aa01030cbf72cda6ef8bf6a3ad4e9c9c9df | MATCH |
| 01_RESEARCH_PAPER/LIMITATIONS.md | 9d169409cdcc6fd81e0d550bd2d7fcf9c8efa98ed507eb96323a3859ded5035e | 9d169409cdcc6fd81e0d550bd2d7fcf9c8efa98ed507eb96323a3859ded5035e | MATCH |
| 01_RESEARCH_PAPER/PAPER.md | a2febd10201dcf2870df8d7c407943db1b3ad332c41c1668f3213cf58d760675 | a2febd10201dcf2870df8d7c407943db1b3ad332c41c1668f3213cf58d760675 | MATCH |
| 02_AUDIT_EVIDENCE/BUILD_RECORD_SCHEMA.md | e249bc0f487902cc1d66709171f0b808990cf4308b099231f79b48b6bd702d3f | e249bc0f487902cc1d66709171f0b808990cf4308b099231f79b48b6bd702d3f | MATCH |
| 02_AUDIT_EVIDENCE/EXECUTION_TRACE_MODEL.md | c87e218199db33d894f01615024b06f12ae8055ec2c356cbdb013ea43f834495 | 9906e0a279b46fd31b9eee18e67935c8cc95ac41b23398aa416c69887c204bb2 | DIFF — path sanitization |
| 02_AUDIT_EVIDENCE/SHA256_MANIFEST.md | 7057359bb95644947ee766839e641b75177893a37e310d8e7bff46e208b7a9ee | 7057359bb95644947ee766839e641b75177893a37e310d8e7bff46e208b7a9ee | MATCH |
| 02_AUDIT_EVIDENCE/SIGNATURE_RECORD_SCHEMA.md | eaa92cc51d72531e95e049fd1d1206221bfbc800ecaf00c4dcfff2ae4c23705c | eaa92cc51d72531e95e049fd1d1206221bfbc800ecaf00c4dcfff2ae4c23705c | MATCH |
| 03_CLEAN_ROOM_PIPELINE/PHASE_1.md | 2018c20371bdbf541331b773278692a75e9b56d1d99f7259b1387a949a894b7f | 2018c20371bdbf541331b773278692a75e9b56d1d99f7259b1387a949a894b7f | MATCH |
| 03_CLEAN_ROOM_PIPELINE/PHASE_2_PENDING.md | 4ccaaa31463e3cba921edfa2fb61bad1b96729f86b8877d85345240d7367872f | 4ccaaa31463e3cba921edfa2fb61bad1b96729f86b8877d85345240d7367872f | MATCH |
| 03_CLEAN_ROOM_PIPELINE/REQUIRES_DESIGN_DECISION.md | f297bb9d740b9383255ac5615c24b426ba11248ef4c4327a71d997855ca01e95 | f297bb9d740b9383255ac5615c24b426ba11248ef4c4327a71d997855ca01e95 | MATCH |
| 03_CLEAN_ROOM_PIPELINE/WHITELIST_POLICY.md | 2aaf03b2c10e6f57212e541ea52d27bbf8b77343903c2b9515a39a65678aa92d | 2aaf03b2c10e6f57212e541ea52d27bbf8b77343903c2b9515a39a65678aa92d | MATCH |
| 04_METADATA_ZENODO/AUTHORS.md | 90b6175077973b2ebe8574ba5517b9f03c11a3ebbad45bd0b1ccefda96a9575a | 90b6175077973b2ebe8574ba5517b9f03c11a3ebbad45bd0b1ccefda96a9575a | MATCH |
| 04_METADATA_ZENODO/DOI_PLACEHOLDER.md | 393d9f1f63a75d1bf1b0567a18cc0c7d550306d902210911374984487dd26796 | 5b89449d0cb504a1b198d4874b4298d9fe6b77e974b8103b66a5db78b082c3ab | DIFF — path sanitization |
| 04_METADATA_ZENODO/KEYWORDS.md | a798746ca0b669b077cfa128ad0cc150b00441c90eac46de6a6f7e0d9690f4dc | a798746ca0b669b077cfa128ad0cc150b00441c90eac46de6a6f7e0d9690f4dc | MATCH |
| 04_METADATA_ZENODO/LICENSE.md | cb4e4f0ca3152f7721bfa3eee5e892200f13a2a58cb085c609671d4b162386ea | d58b46e3e588160214c90bdd9c0a5f8ac9cbdb13001c43e864956cc76c845315 | DIFF — path sanitization |
| 04_METADATA_ZENODO/TITLE.md | bb84def1b2c8432764e4389e24278bb3e76fa5bac758a3c3c89b567abc782bfa | bb84def1b2c8432764e4389e24278bb3e76fa5bac758a3c3c89b567abc782bfa | MATCH |
| 04_METADATA_ZENODO/VERSION.md | 1aa451169fc92fbb40421823063a038baed0e4109840ebe295f74ce8a3414604 | 1aa451169fc92fbb40421823063a038baed0e4109840ebe295f74ce8a3414604 | MATCH |
| 05_EXECUTIVE_SUMMARY/AWS_SECURITY_BRIEF.md | 6fcba5d170b977f5310a5c82d16a64b6d5c2164ecce4ef01d5befe962d9dcad4 | 6fcba5d170b977f5310a5c82d16a64b6d5c2164ecce4ef01d5befe962d9dcad4 | MATCH |
| 05_EXECUTIVE_SUMMARY/MICROSOFT_RESEARCH_BRIEF.md | 9254e34e31efda5fb05008c587df2be1d111466c76e36cde2222c54c1d6b1bf5 | 9254e34e31efda5fb05008c587df2be1d111466c76e36cde2222c54c1d6b1bf5 | MATCH |
| 05_EXECUTIVE_SUMMARY/NON_TECHNICAL_SUMMARY.md | 7d0166ea7d49cd0fe86d5b00a6f1823a04b4e8f06cbae61f3491587287e24181 | 7d0166ea7d49cd0fe86d5b00a6f1823a04b4e8f06cbae61f3491587287e24181 | MATCH |
| README.md | 89ee1e1f9d0a2afd3dd385fc727e8878ca2484bb0c5bd02f54dbd6ec015a3810 | b5ca678eb6b764e20f0695bd6973157a0fd1f8fc6f96c65dc8fd77112d08fc80 | DIFF — public rewrite |

| `LICENSE` (mirror only) | N/A | `56a2328d4e883e190a8301352a9b2ea2c598e37b2cba7191f39508c381bafbc3` | **NEW** — CC BY-NC 4.0 root license |

**Byte-identical copies:** 24 / 28 CEB files  
**Intentional differences:** 4 (`README.md` public rewrite; `02_AUDIT_EVIDENCE/EXECUTION_TRACE_MODEL.md`, `04_METADATA_ZENODO/DOI_PLACEHOLDER.md`, `04_METADATA_ZENODO/LICENSE.md` path sanitization)

---

## 5. Publication status

| Gate | Status |
|------|--------|
| Sanitization | PASS |
| Security scan | PASS |
| Git initial commit | Complete (not pushed) |

**Status:** **READY_FOR_GITHUB_PUBLICATION**

**Notes for Zenodo linking:** Reconcile root `LICENSE` (CC BY-NC 4.0) with deposit notes in `04_METADATA_ZENODO/LICENSE.md` (CC BY-NC 4.0 recommendation) before DOI deposit. Record commit `fb6e2178c26c19b60bec9ebbf3fd9432437750e7` in BUILD_RECORD when publishing.

---

_Security Release Engineer — mirror integrity gate_


> Superseded for publication gates by `PUBLICATION_READINESS_REPORT.md` and `PUBLICATION_FINAL_REPORT.md` (freeze: v1.0-CEB-RELEASE).

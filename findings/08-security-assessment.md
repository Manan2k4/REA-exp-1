# Static Security Assessment

| # | Severity | Confidence | Status | Finding |
|---:|---|---:|---|---|
| 1 | MEDIUM | 7/10 | Suspected / source-corroborated | FileProvider path scope is broad (`external-path` `"."`), increasing exposure if a confused-deputy URI grant path exists. Provider is non-exported, so no direct unauthenticated provider access was established. |
| 2 | MEDIUM | 6/10 | Suspected / source-corroborated | Group code is used as `SHA-256(groupCode)` directly for NaCl SecretBox key derivation. Low-entropy group codes are susceptible to offline guessing if boxed certificate material is captured. |
| 3 | LOW | 6/10 | Confirmed manifest | `ShareActivity` is exported and accepts `SEND`/`SEND_MULTIPLE` for `*/*`; input validation and URI handling must be robust. No exploitability was established from manifest-only evidence. |
| 4 | LOW | 5/10 | Unverified | Transfer `relative_path` metadata could create traversal risk if receiver containment checks are incomplete. Source excerpts were insufficient to confirm or dismiss all checks. |

## Evidence and remediation

1. Restrict FileProvider paths to the smallest app-owned share directory, avoid broad external roots, and grant only intended URI permissions. Verify all share/deep-link flows.
2. Use a memory-hard KDF with a per-install salt for group-code-derived keys, rate-limit/confirm pairing, and rotate peer certificates safely. Preserve interoperability requirements explicitly.
3. Treat every incoming `Intent`, MIME type, and `content://` URI as hostile; enforce size/type limits and validate permissions before resolving.
4. Canonicalize destination paths and enforce containment under an app-selected root; reject absolute paths, traversal, unsupported file types, and symlink escapes.

No hardcoded private keys or credentials were found in the limited readable-string review. Dependency versions were visible in public build metadata, but APK dependency provenance and CVE status were not assessed through an APK-capable REA scanner.

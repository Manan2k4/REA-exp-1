# Warpinator Android 1.9 — Executive Summary

## Scope and limitations

The analyzed artifact is `target/warpinator-android_1.9.apk`. Static inspection was performed without installing or executing the APK. REA-specific APK/JADX tools were not available in the exposed MCP tool registry; local Android SDK `aapt` and `apksigner` were available and used. Consequently, class/method behavior is confirmed from APK strings and manifest evidence only where explicitly marked; detailed implementation claims are corroborated by the public source repository, not presented as independent APK decompilation.

## Identity

| Property | Result |
|---|---|
| Package | `slowscript.warpinator` |
| Application | Warpinator |
| Version | 1.9 / version code 1090 |
| min / target / compile | 21 / 35 / 36 |
| SHA-256 | `A3407632C622C2EF2A730299F729A91D21E2254830E23B0A08D2DB22DED2CEAE` |
| Signing | v1 and v2 valid; one RSA-2048 signer, DN `CN=slowscript` |

## Main conclusions

1. The manifest exposes a launcher/deep-link `MainActivity`, an exported share-target `ShareActivity`, a foreground `MainService`, a Quick Settings tile service protected by `BIND_QUICK_SETTINGS_TILE`, and a non-exported boot receiver.
2. The APK includes gRPC, protobuf, JmDNS, Bouncy Castle, NaCl, Conscrypt, and Netty-related dependency metadata. Readable DEX strings contain the `Warp`/`WarpRegistration` protocol names and transfer RPC names.
3. Public source corroborates mDNS service discovery, gRPC transfer operations, group-code-derived NaCl secret boxes for certificate exchange, per-IP self-signed RSA certificates, and zlib compression.
4. The strongest static security concern is the broad FileProvider path (`external-path` with `"."`) in the corresponding public source. The provider is not exported and grants URI permissions, so impact depends on an app-controlled URI grant or confused-deputy flow; APK-side confirmation of the exact XML was not possible with the unavailable resource decoder.
5. No exploit was attempted, no live network probing was performed, and no secret/private key material was disclosed.

See [08-security-assessment.md](08-security-assessment.md) for confidence-qualified findings.

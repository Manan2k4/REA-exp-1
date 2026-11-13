# Public Source Comparison

Repository compared: https://github.com/slowscript/warpinator-android (public `master`, retrieved 2026-11-13).

## Corroborated

- Manifest components, permissions, package ID, version 1.9, and SDK values match the APK's decoded package metadata.
- Source file set contains `MainActivity`, `MainService`, `Server`, `GrpcService`, `Transfer`, `Authenticator`, `CertServer`, `Autostart`, `TileMainService`, and `warp.proto`, matching DEX strings and manifest names.
- `warp.proto` matches DEX protocol identifiers and describes the transfer/registration RPCs.
- Build metadata identifies JmDNS, gRPC, protobuf, Bouncy Castle, NaCl, Conscrypt, and AndroidX dependencies consistent with APK `META-INF` entries.

## Source-only or not independently verified

The exact service type/ports, certificate implementation details, path reconstruction logic, TLS setup, and notification behavior are source-corroborated but not independently verified from decompiled APK code because JADX/REA APK analysis was unavailable. ProGuard/minification and possible build changes could alter class names or behavior while preserving public identifiers.

The comparison therefore supports compatibility context, not proof that every current `master` line is present in version code 1090.

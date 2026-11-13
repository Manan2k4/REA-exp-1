# APK Identification and Structure

## Artifact

- Path: `target\warpinator-android_1.9.apk`
- SHA-256: `A3407632C622C2EF2A730299F729A91D21E2254830E23B0A08D2DB22DED2CEAE`
- Archive evidence: [evidence/apk-zip-list.txt](evidence/apk-zip-list.txt)
- Package evidence: [evidence/aapt-badging.txt](evidence/aapt-badging.txt)

The archive contains `AndroidManifest.xml`, `resources.arsc`, `classes.dex`, AndroidX/third-party `META-INF` metadata, and signature files (`META-INF/CERT.RSA`, `CERT.SF`, `MANIFEST.MF`). The package has no `lib\` entries, so no native ABI libraries were observed. The DEX contains readable protocol identifiers including `WarpProto`, `TransferOpRequest`, `ServiceRegistration`, `StartTransfer`, `CancelTransferOpRequest`, and `RequestCertificate`.

## Signing

`apksigner` reports valid v1 and v2 signatures, no v3/v3.1/v4 signature or SourceStamp, one signer, RSA 2048:

- certificate SHA-256: `35dc38f1e46f82ca3085aaa05af614083872974da7a65a848616ef9fff8f207c`
- certificate SHA-1: `b4b6e4b60d537e07a9c95548e81a43b03241cf39`

Full output: [evidence/signature.txt](evidence/signature.txt).

## SDK and permissions

`minSdkVersion` is 21, target 35, compile/platform build 36. Declared permissions are Wi-Fi multicast, Internet, network/Wi-Fi state, foreground service and data-sync foreground service, boot completion, notifications, wake lock, and legacy external storage permissions capped at SDK 32/29. A package-defined dynamic receiver permission is also present.

Full decoded permission output: [evidence/aapt-permissions.txt](evidence/aapt-permissions.txt).

## Availability

The exposed REA tool registry did not provide an APK/JADX analyzer. Local `jadx`, `apktool`, `apkanalyzer` on PATH, and `aapt` discovery via PATH were initially absent; SDK `aapt.exe` and `apksigner.bat` were found at `C:\Users\ghoni\AppData\Local\Android\Sdk\build-tools\36.0.0`. No additional software was installed.

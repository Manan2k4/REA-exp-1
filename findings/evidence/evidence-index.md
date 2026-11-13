# Evidence Index

| Evidence | Collection method | Supports |
|---|---|---|
| [sha256.txt](sha256.txt) | `Get-FileHash -Algorithm SHA256` | Artifact identity |
| [aapt-badging.txt](aapt-badging.txt) | Android SDK `aapt dump badging` | Package/version/SDK/components/native ABIs |
| [aapt-permissions.txt](aapt-permissions.txt) | Android SDK `aapt dump permissions` | Requested and custom permissions |
| [manifest-xmltree.txt](manifest-xmltree.txt) | Android SDK `aapt dump xmltree` | Manifest components, filters, provider/service declarations |
| [signature.txt](signature.txt) | Android SDK `apksigner verify --verbose --print-certs` | Signature schemes and certificate fingerprints |
| [apk-zip-list.txt](apk-zip-list.txt) | 7-Zip read-only archive listing | DEX/resources/assets/META-INF/native-library inventory |

## Provenance rules

`APK-confirmed` means directly supported by the captured APK evidence above. `Source-corroborated` means supported by the public repository and matching package/protocol identifiers but not independently decompiled from this APK. `Unverified` means the available evidence is insufficient. The APK was never installed, executed, modified, or network-probed.

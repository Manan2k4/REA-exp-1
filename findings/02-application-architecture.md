# Application Architecture

## Manifest-confirmed components

| Component | Exported | Evidence / role |
|---|---:|---|
| `MainActivity` | yes | Launcher, `singleTask`, `warpinator:` BROWSABLE deep link, Quick Settings preferences |
| `ShareActivity` | yes | `SEND` and `SEND_MULTIPLE` share target for any MIME type |
| `AboutActivity`, `SettingsActivity`, `TransfersActivity` | default/unspecified | UI screens |
| `MainService` | default/unspecified | Foreground `dataSync` service |
| `TileMainService` | yes | Quick Settings tile, gated by `BIND_QUICK_SETTINGS_TILE` |
| `Autostart` | no | Boot/reboot/package-replaced receiver |
| `MainService$StopSvcReceiver` | no | Internal stop action |
| AndroidX `FileProvider` | no | URI grants, provider paths resource |

Decoded manifest: [evidence/manifest-xmltree.txt](evidence/manifest-xmltree.txt).

## Reconstructed flow

`WarpinatorApp` owns process-level initialization; `MainActivity` presents peers/settings and starts or binds the service. `MainService` owns network lifecycle, notifications, peer collection, and the multicast lock. `Server` owns JmDNS and gRPC server registration. `Remote` models peers; `GrpcService` implements protocol callbacks; `Transfer` handles file enumeration and receive/send progress. `Autostart` starts the service after boot/package replacement, while `TileMainService` toggles service state.

This internal responsibility map is corroborated by the public source tree. Exact APK class bodies and line-level correspondence remain unverified because JADX/DEX decompilation was unavailable.

See [diagrams/architecture.mmd](diagrams/architecture.mmd).

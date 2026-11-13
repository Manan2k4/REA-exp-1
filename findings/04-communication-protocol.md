# Communication Protocol

## Protobuf contract

The public `warp.proto` defines `Warp` and `WarpRegistration` services. DEX strings independently expose `WarpProto`, `TransferOpRequest`, `ServiceRegistration`, `RequestCertificate`, `RegisterService`, `StartTransfer`, `ProcessTransferOpRequest`, `PauseTransferOp`, `CancelTransferOpRequest`, and `StopTransfer`.

Important RPCs:

- discovery/handshake: `CheckDuplexConnection`, `WaitingForDuplex`, `GetRemoteMachineInfo`, `GetRemoteMachineAvatar`, `Ping`
- transfer control: `ProcessTransferOpRequest`, `StartTransfer`, `PauseTransferOp`, `CancelTransferOpRequest`, `StopTransfer`
- messaging: `SendTextMessage`
- registration/auth: `RequestCertificate`, `RegisterService`

`TransferOpRequest` carries operation identity/timestamp, sender/receiver names, total size/count, single-file metadata, and top-directory basenames. `FileChunk` carries relative path, file type, symlink target, bytes, mode, and timestamps.

## Sequence

The sender requests a transfer; the receiver accepts or rejects; the receiver invokes `StartTransfer`; streamed `FileChunk` messages reconstruct files/directories; either side may pause/cancel/stop. The public source indicates gRPC streaming and explicit cancellation/error callbacks. APK-independent confirmation of all branch behavior is unavailable.

See [diagrams/transfer-sequence.mmd](diagrams/transfer-sequence.mmd).

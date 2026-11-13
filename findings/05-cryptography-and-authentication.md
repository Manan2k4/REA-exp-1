# Cryptography and Authentication

The public source corroborates the following design:

- A per-device RSA-2048 key pair is generated with `SecureRandom`.
- A self-signed X.509 certificate is created with an IP subject-alternative name and approximately 30-day validity.
- The certificate is stored with a private key under the app's certificate directory.
- The certificate is wrapped using NaCl `SecretBox`; the 32-byte key is `SHA-256(groupCode)`, with a random 24-byte nonce.
- The default group code is `Warpinator`.
- A UDP certificate server responds to the exact ASCII request `REQUEST` with Base64-wrapped certificate bytes.
- A peer unwraps the certificate using the group code and places it in a trust store.
- TLS uses a trust store containing the peer certificate; the source requests `SSLContext.getInstance("SSL")`.

## Security interpretation

The group code is a shared secret for certificate bootstrapping, not a password-stretching scheme. SHA-256 directly over a low-entropy user group code permits offline guessing if an attacker obtains a boxed certificate. The per-peer certificate trust store provides pin-like identity binding after exchange, but the available evidence does not establish whether peer identity, IP changes, replay, or certificate replacement are handled robustly in the APK.

The source uses broad exception suppression while loading/regenerating the local certificate. This is a reliability and forensic-observability concern rather than proof of a cryptographic break.

Source-corroborated, APK-unverified details are deliberately marked as such.

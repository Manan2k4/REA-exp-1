# File Transfer Internals

The public source shows Storage Access Framework URI resolution for selected files and trees. Directory traversal queries child documents recursively and records relative paths. Transfer metadata includes file type, relative path, mode and modification time. Data is streamed through gRPC `FileChunk` messages; optional zlib compression is implemented with Java `Deflater`/`Inflater`.

The source explicitly reports symbolic links as unsupported. It also contains cancellation and gRPC error paths, notification progress, media scanning, and incoming-file handling. Exact overwrite, resume, temporary-file, and path-canonicalization behavior requires APK decompilation or a controlled source/version match; these items are therefore not asserted as confirmed.

## Safety review

The protocol has a `relative_path` field and a receiver must treat it as untrusted metadata. A safe implementation must reject absolute paths, `..` traversal, path escapes after canonicalization, and unexpected file types before writing. The available source excerpts establish the field and recursive reconstruction model but do not establish that every required containment check is present.

No malformed transfer was sent and no exploitation was attempted.

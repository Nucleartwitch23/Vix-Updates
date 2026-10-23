# Vix Services Update Format

This public repository hosts compiled releases only. Keep source code and secrets in the private development repository.

## Release format

Create a GitHub Release with a semantic version tag such as `v1.0.0`.

Attach:
- `VixDesktop.zip` containing `VixDesktop.exe` and its required application assets.
- `SHA256SUMS.txt` containing the SHA-256 digest of `VixDesktop.zip`.

Generate checksum on Windows PowerShell:
```powershell
(Get-FileHash .\VixDesktop.zip -Algorithm SHA256).Hash.ToLower() + "  VixDesktop.zip" | Set-Content SHA256SUMS.txt
```

Updater release endpoint:
`https://api.github.com/repos/Nucleartwitch23/Vix-Updates/releases/latest`

**Security:** SHA-256 verifies file integrity against the published checksum but does not authenticate a compromised release account. Code-sign binaries and ideally verify a separately signed update manifest before executing downloaded binaries. Use HTTPS, reject archive path traversal, stage installs atomically, and preserve rollback. Never embed a GitHub personal access token in the loader.

**Limitation:** Publishing a release is not the same as uploading files to the Git repository. The customer-facing loader must be configured to read this repository's Releases endpoint and thoroughly tested before distribution.

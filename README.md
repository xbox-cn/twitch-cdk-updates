# TwitchCDK Updates

Public update channel for TwitchCDK. This repository contains **no source code**.

- `version.json` — latest version, release notes, artifact path, SHA-256 and Ed25519 signature.
- `releases/` — compiled Linux amd64 runtime bundles (backend binary + frontend dist).

The server-side updater reads `version.json`, verifies the Ed25519 signature with
the public key committed in the main repository, downloads the referenced bundle,
verifies SHA-256, swaps the runtime and rebuilds only the two application
containers. Database data and `.env` are never touched.

## Manifest contract

```json
{
  "version": "3.1.0",
  "released_at": "2026-11-17T20:30:00+08:00",
  "notes": ["..."],
  "min_version": "3.0.0",
  "artifact": "releases/twitch-cdk-3.1.0-linux-amd64.tar.gz",
  "sha256": "<64 hex chars>",
  "size": 12345678,
  "signature": "<base64 Ed25519 signature>"
}
```

The signature covers this exact UTF-8 payload:

```text
version=<version>
artifact=<artifact>
sha256=<sha256>
size=<size>
```

`artifact` may be relative to this repository or an absolute HTTPS URL.
Automatic updates require HTTPS, a valid signature and a valid SHA-256.

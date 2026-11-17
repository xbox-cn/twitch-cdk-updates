# TwitchCDK Updates

Public update channel for TwitchCDK. This repository contains **no source code**.

- `version.json` — latest version, release notes, artifact path and SHA-256.
- `releases/` — compiled Linux amd64 runtime bundles (backend binary + frontend dist).

The server-side updater reads `version.json`, downloads the referenced bundle,
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
  "size": 12345678
}
```

`artifact` may be relative to this repository or an absolute HTTPS URL.
Automatic updates require HTTPS and a valid SHA-256.

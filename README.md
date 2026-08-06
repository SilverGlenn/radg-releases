# Radg 2.0 Release Channel

Compiled update packages and signed channel manifests for the Radg 2.0
HRIS desktop tool. **No source code is published here.**

## How updates work

`Radg Launcher.exe` on each HR computer:

1. Fetches `channels/stable.json` (or `channels/pilot.json`) plus its
   `.sig` signature file from this repository.
2. Verifies the Ed25519 signature and the embedded SHA-256 / size.
3. Downloads the referenced Release asset and installs it into a new
   version directory.
4. Runs a health check, activates the version atomically, and launches
   the app.

A tampered manifest or package is rejected; the installed version keeps
running. A failed startup rolls back to the previous version.

## Contents

- `channels/stable.json` — production channel (all HR computers).
- `channels/stable.json.sig` — Ed25519 signature over the manifest.
- `channels/pilot.json` — candidate channel (HR Generalist / HR Manager).
- Releases — `radg-2-<version>-build-<n>-windows-x64.zip` packages.

All updates are published automatically by CI from the private source
repository. Do not edit manifests by hand; the signature will not match.

# Electron Builds

Build, code-sign, and publish Electron apps on macOS, Windows, and Linux using [`electron-builder`](https://www.electron.build) (`samuelmeuli/action-electron-builder`).

## What it can do
- Runs your `package.json` `build` script, then packages with `electron-builder`
- Builds across `[macos-latest, ubuntu-latest, windows-latest]` in a matrix
- Publishes release artifacts to GitHub Releases when `release: true` (e.g. on `v*` tags)
- Supports macOS (`mac_certs`) and Windows (`windows_certs`) code signing

## Key Inputs
- `github_token` *(required)* — `${{ secrets.GITHUB_TOKEN }}`
- `release` — `true` to publish release artifacts (e.g. `${{ startsWith(github.ref, 'refs/tags/v') }}`)
- `mac_certs` / `mac_certs_password` — base64 `.p12` cert & password
- `windows_certs` / `windows_certs_password` — base64 cert & password
- `package_root` (default: `.`), `build_script_name` (default: `build`), `skip_build`, `use_vue_cli`, `args`, `max_attempts`

## Example

```yaml
name: Build/release
on: push

jobs:
  release:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [macos-latest, ubuntu-latest, windows-latest]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Build/release Electron app
        uses: samuelmeuli/action-electron-builder@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          release: ${{ startsWith(github.ref, 'refs/tags/v') }}
          # Optional code signing:
          mac_certs: ${{ secrets.mac_certs }}
          mac_certs_password: ${{ secrets.mac_certs_password }}
```

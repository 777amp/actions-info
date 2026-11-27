# Compression

Compress executables using [UPX](https://github.com/upx/upx) (`crazy-max/ghaction-upx`).

> **Note:** Supported on Linux and Windows runners only.

## What it can do
- Download/install a specific or `latest` UPX version
- Compress binaries matching newline-delimited glob patterns with custom UPX flags
- Install UPX only (`install-only: true`) for manual use in later steps

## Key Inputs
- `version` (default: `latest`, e.g. `v3.95`)
- `files` (newline-delimited path globs)
- `args` (flags passed to `upx`, e.g. `-fq` or `--best`)
- `install-only` (`true` / `false`)

## Examples

### Compress binaries
```yaml
- name: Run UPX
  uses: crazy-max/ghaction-upx@v4
  with:
    version: latest
    files: |
      ./bin/*.exe
    args: -fq
```

### Install UPX only
```yaml
- name: Install UPX
  uses: crazy-max/ghaction-upx@v4
  with:
    install-only: true

- name: Check version
  run: upx --version
```

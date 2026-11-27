# Virus Scanning

Upload and scan local build files or GitHub Release assets using [VirusTotal](https://www.virustotal.com) (`crazy-max/ghaction-virustotal`).

## What it can do
- Scan local files matched by glob patterns
- Upload to VirusTotal Monitor (`vt_monitor: true`)
- Automatically scan assets when a GitHub Release is published
- Append scan analysis links directly to the GitHub Release body (`update_release_body: true`)

## Key Inputs & Outputs
- **Inputs**: `vt_api_key` *(required)*, `files` *(required, newline-delimited globs)*, `vt_monitor`, `monitor_path`, `update_release_body`, `github_token`, `request_rate` (set `4` or lower for free public API)
- **Output**: `analysis` (`<filename>=<analysisURL>`, comma-separated)

## Examples

### Scan local files
```yaml
- name: VirusTotal Scan
  uses: crazy-max/ghaction-virustotal@v5
  with:
    vt_api_key: ${{ secrets.VT_API_KEY }}
    files: |
      ./foo-win32.exe
      ./foo-win64.exe
```

### Scan via VirusTotal Monitor
```yaml
- name: VirusTotal Scan
  uses: crazy-max/ghaction-virustotal@v5
  with:
    vt_api_key: ${{ secrets.VT_API_KEY }}
    vt_monitor: true
    monitor_path: /ghaction-virustotal
    files: |
      ./foo-win32.exe
      ./foo-win64.exe
```

### Scan published release assets & update release body
```yaml
on:
  release:
    types: [published]

jobs:
  virustotal:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: VirusTotal Scan
        uses: crazy-max/ghaction-virustotal@v5
        with:
          vt_api_key: ${{ secrets.VT_API_KEY }}
          update_release_body: true
          files: |
            .exe$
```

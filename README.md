# actions-info

Quick reference wiki of what GitHub Actions in this workspace can do, organized by capability area with minimal YAML examples.

| Area | What it does | Actions covered |
| --- | --- | --- |
| [Virus Scanning](virus-scanning.md) | Upload & scan build artifacts or release assets with VirusTotal | `crazy-max/ghaction-virustotal` |
| [Compression](compression.md) | Compress executables with UPX | `crazy-max/ghaction-upx` |
| [Notifications](notifications.md) | Send messages, embeds, and files to Discord & Telegram | `appleboy/discord-action`, `Ilshidur/action-discord`, `appleboy/telegram-action` |
| [Deployment](deployment.md) | Deploy static sites/build directories to GitHub Pages | `crazy-max/ghaction-github-pages` |
| [Remote SSH](ssh.md) | Run commands on remote servers over SSH (multi-host, proxy, stdout capture) | `appleboy/ssh-action` |
| [Versioning](versioning.md) | Calculate next major/minor/patch SemVer versions | `WyriHaximus/github-action-next-semvers` |
| [Electron Builds](electron.md) | Build, sign, and release Electron apps on macOS, Windows, and Linux | `samuelmeuli/action-electron-builder` |
| [Website Capture](website-capture.md) | Capture a webpage as an animated GIF or WebP | `PabloLec/website-to-gif` |

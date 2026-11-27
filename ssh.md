# Remote SSH

Execute commands on remote servers over SSH (`appleboy/ssh-action`).

## What it can do
- Authenticate via SSH private key (`key` / `key_path` + optional `passphrase`) or `password`
- Run inline `script` or a repo file (`script_path`)
- Target multiple hosts/ports (`host: "foo.com:1234,bar.com:5678"`), optionally synchronously (`sync: true`)
- Forward specific workflow env vars (`envs`) or all `GITHUB_*`/`INPUT_*` vars (`allenvs: true`)
- Capture remote stdout into step outputs (`capture_stdout: true`)
- Connect through a jump host (`proxy_host`, `proxy_username`, `proxy_key`, etc.)

## Key Inputs & Outputs
- **Connection**: `host`, `port` (`22`), `username`, `key` / `key_path` / `password`, `passphrase`, `fingerprint`, `sync`, `timeout`
- **Execution**: `script` / `script_path`, `envs`, `allenvs`, `command_timeout`, `capture_stdout`, `request_pty`, `debug`
- **Proxy**: `proxy_host`, `proxy_port`, `proxy_username`, `proxy_key` / `proxy_password`
- **Output**: `stdout` (when `capture_stdout: true`)

## Examples

### Run commands with SSH key
```yaml
- name: Execute remote SSH commands
  uses: appleboy/ssh-action@v1
  with:
    host: ${{ secrets.HOST }}
    username: ${{ secrets.USERNAME }}
    key: ${{ secrets.KEY }}
    port: ${{ secrets.PORT }}
    script: |
      set -e
      whoami
      ls -al
```

### Multi-host + pass env vars + capture stdout
```yaml
- name: Run on multiple hosts
  id: ssh
  uses: appleboy/ssh-action@v1
  env:
    SHA: ${{ github.sha }}
  with:
    host: "foo.com:22,bar.com:2222"
    sync: true
    username: ${{ secrets.USERNAME }}
    key: ${{ secrets.KEY }}
    envs: SHA
    capture_stdout: true
    script: |
      echo "Deploying $SHA"
      hostname

- name: Use output
  run: echo "${{ steps.ssh.outputs.stdout }}"
```

### Connect via jump host (proxy)
```yaml
- name: SSH via jump host
  uses: appleboy/ssh-action@v1
  with:
    host: ${{ secrets.HOST }}
    username: ${{ secrets.USERNAME }}
    key: ${{ secrets.KEY }}
    proxy_host: ${{ secrets.PROXY_HOST }}
    proxy_username: ${{ secrets.PROXY_USERNAME }}
    proxy_key: ${{ secrets.PROXY_KEY }}
    script: ls -al
```

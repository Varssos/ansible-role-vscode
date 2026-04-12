# vscode

Ansible role to install [Visual Studio Code](https://code.visualstudio.com/) on Debian/Ubuntu systems.

## Requirements

- Debian or Ubuntu host
- `become: true` privileges (sudo)

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `vscode_package_name` | `code` | Package name to install via apt |
| `vscode_gpg_key_url` | `https://packages.microsoft.com/keys/microsoft.asc` | URL to the Microsoft GPG key |
| `vscode_gpg_key_tmp` | `/tmp/microsoft.asc` | Temporary path for the downloaded key |
| `vscode_gpg_keyring` | `/etc/apt/keyrings/microsoft.gpg` | Path for the converted keyring file |

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: vscode
```

## License

MIT

## Author

Varssos
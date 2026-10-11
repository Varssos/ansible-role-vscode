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
| `vscode_user` | `{{ ansible_user }}` | User profile for VS Code extensions |
| `vscode_extensions` | See defaults | Extensions to install |

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: vscode
```

## Manual setup (without Ansible)

On an amd64 Debian/Ubuntu host:

```bash
sudo apt install curl gnupg
sudo install -d -m 0755 /etc/apt/keyrings
curl -fL https://packages.microsoft.com/keys/microsoft.asc -o /tmp/microsoft.asc
sudo gpg --dearmor --yes --output /etc/apt/keyrings/microsoft.gpg /tmp/microsoft.asc
sudo chmod 0644 /etc/apt/keyrings/microsoft.gpg
echo 'deb [arch=amd64 signed-by=/etc/apt/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main' | sudo tee /etc/apt/sources.list.d/vscode.list
sudo apt update
sudo apt install code
rm /tmp/microsoft.asc
```

Install the default extensions as your desktop user, without sudo:

```bash
code --list-extensions
for extension in \
  shd101wyy.markdown-preview-enhanced \
  ms-python.python \
  ms-python.debugpy \
  ms-azuretools.vscode-docker \
  ms-vscode.cpptools \
  ms-vscode.cpptools-extension-pack \
  waderyan.gitblame \
  donjayamanne.git-extension-pack \
  jebbs.plantuml; do
  code --install-extension "$extension"
done
```

## License

MIT

## Author

Varssos
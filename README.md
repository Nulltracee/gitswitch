# gitswitch

> [!NOTE]
> **gitswitch** lets you switch Git identities and SSH accounts with one command — while preventing commits from the wrong account.

## Features

* Switch Git identity
* Switch SSH accounts
* Block accounts in specific repos
* Prevent wrong-account commits

## Install

```bash
git clone https://github.com/Nulltracee/gitswitch/edit/main/README.md
cd gitswitch
install -Dm755 gitswitch ~/.local/bin/gitswitch
```

> [!IMPORTANT]
> Make sure **~/.local/bin** is in your PATH.

## Config
Configuration is stored in:

```text
~/.config/gitswitch/config.json
```

Example:

```json
{
  "accounts": {
    "personal": {
      "name": "Your Name",
      "email": "you@example.com",
      "ssh_host": "github-personal",
      "ssh_key": "~/.ssh/id_ed25519_personal",
      "forbidden_repos": ["~/work/*"]
    },
    "work": {
      "name": "Your Name",
      "email": "you@company.com",
      "ssh_host": "github-work",
      "ssh_key": "~/.ssh/id_ed25519_work",
      "forbidden_repos": ["~/personal/*"]
    }
  }
}
```

The config path can be overridden with `GITSWITCH_CONFIG`.

## Usage

```bash
gitswitch menu
gitswitch ${name_from_config}

gitswitch status
gitswitch list
gitswitch check

gitswitch uninstall
```

## Testing

Check the active Git identity:

```bash
gitswitch status
```

Test SSH authentication:

```bash
ssh -T git@github-personal
ssh -T git@github-work
```

Verify the remote:

```bash
git remote -v
git ls-remote origin
```

For SSH debugging:

```bash
ssh -vT git@github-work
```

## SSH

Each account uses a separate SSH alias configured in `~/.ssh/config`:

```ssh
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal
    IdentitiesOnly yes

Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
    IdentitiesOnly yes
```

## License

MIT

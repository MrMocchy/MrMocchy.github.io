
# Git

## インストール

```powershell title="PowerShell"
winget install --id Git.Git -e --source winget
```

```bash title="bash"
apt install git
```

## 初期設定

```bash
git config --global user.name 'example name'
git config --global user.email 'example@example.com'
git config --global init.defaultBranch main
git config --global core.autocrlf input
```



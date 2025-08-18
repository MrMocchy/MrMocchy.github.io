
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


## ブランチの新規作成

イチからプロジェクトを作り直す際などは、既存のブランチにて全削除などせず、新しく孤立したブランチを生やすのがいい。
強制プッシュに注意。

```bash
git branch -m main v1
git switch --orphan main
git commit --allow-empty -m "initial commit of v2"
git push -u origin main --force
```


??? note "以前は"

    1. GitHub にて、mainブランチをv1などと改名。
    2. cloneし直す
    3. 
    ```bash
    git switch --orphan main
    ```
    で新規ブランチを作成
    4. GitHub にて、Default Branchをmainに変更。

    でやっていた。
    gitの構造はこれで良いとして、もっと綺麗な方法(GitHubに行かずにローカルで完結するやり方)があるはず、とGeminiに聞いたのが上のもの。
    commitの行は自分で加えたため、メッセージは一般的でない気はする。




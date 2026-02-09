
# SSH

## Windows as Host

システム > オプション機能 > オプション機能を追加する
で「OpenSSHサーバー」を追加。

Windowsセキュリティ > ファイアウォールとネットワーク保護 > ファイアウォールによるアプリケーションの許可
で「OpenSSHサーバー」にネットワークの許可

??? note "できなかったら"
    「設定の変更」ボタンが機能しないことがある。
    
    ```powershell title="PowersShell"
    Get-NetFirewallRule | Where-Object Name -Like "*SSH*"
    ```
    を確認すると、
    ```
    Name                          : OpenSSH-Server-In-TCP
    DisplayName                   : OpenSSH SSH Server (sshd)
    Description                   : Inbound rule for OpenSSH SSH Server (sshd)
    DisplayGroup                  : OpenSSH Server
    Group                         : OpenSSH Server
    Enabled                       : True
    Profile                       : Private
    Platform                      : {}
    Direction                     : Inbound
    Action                        : Allow
    EdgeTraversalPolicy           : Block
    LooseSourceMapping            : False
    LocalOnlyMapping              : False
    Owner                         :
    PrimaryStatus                 : OK
    Status                        : 規則は、ストアから正常に解析されました。 (65536)
    EnforcementStatus             : NotApplicable
    PolicyStoreSource             : PersistentStore
    PolicyStoreSourceType         : Local
    RemoteDynamicKeywordAddresses : {}
    PolicyAppId                   :
    PackageFamilyName             :
    ```
    などとでる。ProfileがPrivateになっていたら、
    ```powershell title="PowerShell (管理者権限)"
    Set-NetFirewallRule –DisplayName "OpenSSH SSH Server (sshd)" -Profile Any
    ```
    とする。再度Get-で表示し、変更の確認をする。
    
    cf: [PowerShell 関連〜PowerShell から Windows Firewall を操作するメモ - ようへいの日々精進XP](https://inokara.hateblo.jp/entry/2016/02/21/195729) by [inokara](https://inokara.hateblo.jp/about)

OpenSSHの起動を設定する。
スタート右クリ > コンピュータの管理 > サービスとアプリケーション > サービス
から「OpenSSH SSH Server」の
スタートアップの種類を自動
にして起動（開始）する。
起動してたら再起動がよさそう。


## Windows as Client

鍵生成
```shell title="cmd"
cd %USERPROFILE%
mkdir .ssh
cd .ssh
ssh-keygen -t ed25519
type id_ed25519.pub
```
`.pub`のが公開鍵、拡張子なしが秘密鍵。
公開鍵の中身を表示したので、コピーしておく。

続いて、接続のたびにipとか入力する面倒を省くため、こんな感じに設定を書いておく。
```txt title="~/.ssh/config"
Host myPC
    HostName 192.168.100.10
    User username
```
（クライアント側から、接続するときに）公開鍵認証を必須にする、などいろいろオプションを設定できるが、これだけでよい。
公開鍵できるならそうしてくれるし、無理ならパスワードを求められる。

ここで、パスワードで接続してみる。
```shell title="cmd"
ssh myPC
```
timeoutしたらサーバーの問題の可能性大。一応pingしてみるのもいい。
パスワードはPINではなく、入るユーザーのMicrosoftアカウントのもの。
3回失敗でsshからやり直すが実質試し放題。
だから公開鍵にすべきという話だが、パスワードでの接続をできるようにしたまま、接続の簡便のためだけに公開鍵認証を設定する。
うっかり自分も出先で接続できなくなったら面倒なので。

接続できたら
```console title="cmd"
username@MYPC C:\Users\username>
```
となっているはず。
ここで、先ほどコピーした公開鍵を
```shell title="cmd"
echo 公開鍵の中身 >> authorized_keys
```
でホストに保存する。

これで公開鍵で接続できるはず。

??? note "できなかったら"
    確認事項
    
    ホスト
    
    - OpenSSHは起動しているか、または再起動してみる
    - OpenSSHのネットワークの権限は十分か
    - windowsに複数ユーザーが存在するなら、`~/.ssh`のアクセス権限は正しいか
      - 継承を無効化
      - システム、管理者、当該ユーザーはフルアクセス
      - 他ユーザーは全面禁止
    
    クライアント
    
    - pingは通るか
    - パスワードでは接続できるか
    - `ssh -i 秘密鍵ファイル username@(ip)`ではできるか
      - できないならホスト側で公開鍵ファイルが参照されていない可能性。以下を確認
    
    （ホスト側）
    ```
    # OpenSSHを停止
    net stop sshd
    # デバッグモードで起動
    C:\Windows\System32\OpenSSH\sshd -d
    ```
    で
    ```txt
    Could not open authorized keys '__PROGRAMDATA__/ssh/administrators_authorized_keys': No such file or directory
    ```
    とかでたら、`~/.ssh/authorized_keys`ではなく管理者の方を読み取ろうとしているらしい。
    その場合、`C:\ProgramData\ssh\sshd_config`の最後の2行を
    ```
    # Match Group administrators
    #       AuthorizedKeysFile __PROGRAMDATA__/ssh/administrators_authorized_keys
    ```
    とコメントアウトすればよい。そして一応OpenSSHを再起動。
    
    cf: [Windows　Permission denied (publickey,keyboard-interactive). - Qiita](https://qiita.com/Cmirai/items/360e28a8708958bf2295) by [@Cmirai](https://qiita.com/Cmirai)

公開鍵で接続出来たらパスワード認証を禁止するべきで、それにはホストの`C:\ProgramData\ssh\sshd_config`をいじる。
このディレクトリは、一度接続されるまで空っぽい。
パスワードで接続してからの順なので`sshd_config`は存在しているはずだが、もし必要なら`C:\Windows\System32\OpenSSH\sshd_config_default`をコピペ＆名前変更するとよい（管理者権限）。

自分はパスワード認証を残したいのでここまで。



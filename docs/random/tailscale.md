
# Tailscale

[SSH](./ssh.md)をインターネット越しに接続するために、TailscaleというVPNを使用した。
友人の勧めでこれを使い始めたが、別の友人にが使っているCloudflareも気になっている。

## Install

=== "Windows"

    ```shell
    winget install Tailscale.Tailscale
    ```
    winget で得られるのは[公式](https://tailscale.com/kb/1347/installation)ではなく、バージョンも最新でない。
    ただ、アップデートすると繋げなくなったり大丈夫だったり（v1.86.2現在）

=== "Linux"

    ```shell
    curl -fsSL https://tailscale.com/install.sh | sh
    ```

## Init

アカウント作成時は2デバイス登録まで流れに従う。

それ以降は
```shell
tailscale up
```
で認証が始まる。

??? "要検証"
    ホスト側は
    ```shell
    tailscale up --advertise-routes=192.168.100.0/24
    ```
    としてからブラウザでこのSubnetをApproveする。
    と聞いたけど直接SSHするならいらないかも。

## IP

```shell
tailscale ip
```
で自分のIPを、

```shell
tailscale status
```
で他デバイスを含めたIPを確認できる。

## iOS

でもTailscaleのアプリがある。設定からVPNを許可。

Termius というSSHアプリで出先からスマホで自宅PCに入れる。
iPhoneではサイズ的に操作性が××だが、画面キーボードはちゃんと工夫されていると感じた。


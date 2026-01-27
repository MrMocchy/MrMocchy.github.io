
# Docker

## 概念

``` mermaid
%%{init: {'theme':'dark'}}%%
graph TD
    R[レジストリ] --pull--> I[イメージ]
    I --run--> C[コンテナ]
    C --commit--> I
```
<style>
* {
    --md-mermaid-node-fg-color: var(--md-default-fg-color);
    --md-mermaid-node-bg-color: var(--md-default-bg-color);
}
</style>


## コマンド

- イメージの取得
    ```console
    docker pull イメージ名
    ```

- イメージの確認
    ```console
    docker images ls
    ```

- コンテナの起動
    （VSCodeで接続することが多いためあまり使用しないか）
    ```console
    docker run [オプション] イメージ名 [コマンド]
    ```
    ```console title="基本"
    docker run -it --name コンテナ名 イメージ名
    ```
    オプション
    - `-i` : 対話モード
    - `-t` : 擬似端末の割り当て
    - `-d` : バックグラウンドで実行
    - `--name コンテナ名` : コンテナ名の指定
    
    `run`のときに少なくとも`-i`をつけないと、コンテナ停止(`stop`)後に再開(`start`)できないっぽい（再開後即停止する）。
    コンテナを作成するだけなら`-id`でよさそう。

- コンテナの確認
    ```console
    docker ps -a
    ```
    オプション
    - `-a` : 停止中のコンテナも表示
    - `-s` : コンテナのサイズも表示

- 停止しているコンテナの再開
    ```console
    docker start コンテナ名
    ```

- 起動中のコンテナへの接続
    ```console
    docker exec -it コンテナ名 /bin/bash
    ```

- コンテナの停止
    ```console
    docker stop コンテナ名
    ```


# BusyBox

cf: [インストール不要！WindowsでLinuxコマンドを使う](https://qiita.com/tetsuy/items/22cba0bc2048967b270a)

- Linuxコマンドを使う
    ```cmd title="cmd"
    busybox64u コマンド [引数...]
    ```
    例：
    ```cmd title="cmd"
    busybox64u ls -l
    ```
    シェルも使える。

- 短く使う
    
    以下を用意。
    ```batch title="bb.bat"
    @busybox64u %*
    ```
    使い方は同じ。
    ```cmd title="cmd"
    bb ls -l
    ```

- cmdでそのままLinuxコマンドを使えるようにする
    ```batch title="cmd（管理者権限）"
    mklink ls.exe busybox64u.exe
    ```

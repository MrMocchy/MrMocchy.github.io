
# ffmpeg


## 基本
```shell
ffmpeg -i input.jpg output.png
```

上書き `-y`

出力抑制 `-v error`  
他の引数は下記の一覧から`-loglevel`を検索して参照。

サイズ（-1でアスペクト比を維持）

- `-vf scale=640:480`
- `-vf scale=1280:-1`

??? "サイズ取得"
    ```powershell title="PowerShell"
    $size = [regex]::Matches($(ffmpeg -i input.jpg 2>&1 | Select-String "Stream"), "(\d+)x(\d+)").Groups
    $width = $size[1].Value
    $height = $size[2].Value
    ```

## 参考

[公式ドキュメント](https://www.ffmpeg.org/ffmpeg.html)


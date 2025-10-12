
# yt-dlp

## 基本これ

mp3で保存
```
yt-dlp -x --audio-format mp3 --add-metadata --embed-thumbnail -o "%(title)s.%(ext)s" URL
```

## 使い方

```
yt-dlp [オプション] URL
```

## オプション

`-F`  
フォーマット一覧

`-f 18`  
ID指定してダウンロード。18は640x360のmp4音声アリ

`-I 1:26`  
プレイリストのインデックス範囲指定。両端含む

`-x --audio-format mp3`  
mp3で出力。-xが音声のみを意味する。

`--parse-metadata FROM:TO`  
`--parse-metadata "%(title)s:%(album)s - %(title)s"`  
mp3などのメタデータを編集

`--add-metadata`  
メタデータを書き込み

`--embed-thumbnail`  
サムネイル埋め込み

`-o "%(title)s.%(ext)s"`  
`-o "C:\Users\patro\Downloads\%(title)s.%(ext)s"`  
出力ファイル名指定

## その他

`ffmpeg -i input.mp3 -i thumbnail.jpg -map 0 -map 1 -c copy -id3v2_version 3 output.mp3`
後からサムネイル埋め込み(iTunesでも可能)

`yt-dlp --rm-cache-dir`  
キャッシュ削除

`yt-dlp --update`  
アップデートする。`-U`でも可  
`ERROR: unable to download video data: HTTP Error 403: Forbidden` と出たらアップデートが必要っぽい。

## 参考

[yt-dlp オプション一覧及びそのメモ](https://masayoshi-9a7ee.hatenablog.com/entry/2021/11/06/112639)

[動画ダウンロードツール youtube-dl のフォークである yt-dlp を使ってみる](https://vlike-vlife.netlify.app/posts/cli_yt-dlp)

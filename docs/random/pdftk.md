
# pdftk

## ページ抜き出し

```cmd
pdftk <in.pdf> cat <pages> output <out.pdf>

# 例
pdftk 第1回講義資料.pdf cat 10 output 第1回課題.pdf
pdftk 第1回講義資料.pdf cat 10-12 output 第1回課題.pdf
pdftk 第1回講義資料.pdf cat 10 12 14 output 第1回課題.pdf
```

## メタデータ編集

```
# メタデータ出力
pdftk <in.pdf> dump_data_utf8 output <meta.txt>

# メタデータファイルの編集
nano meta.txt

# メタデータ更新
pdftk <in.pdf> update_info_utf8 <meta.txt> output <out.pdf>
```


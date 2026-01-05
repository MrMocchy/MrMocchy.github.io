
# 論文用 matplotlib 設定

pngなどの画像として出して論文に貼るときは解像度を大きくしたいが、その場合は`plt.show()`ではウィンドウサイズが大きくなりすぎてしまうため、`plt.savefig()`で保存してから確認するのが良い。

```python
plt.rcParams["figure.dpi"] = 200

# 各種余白（詰め込みたい場合）
plt.rcParams["figure.subplot.top"] = 0.95
plt.rcParams["figure.subplot.bottom"] = 0.14
plt.rcParams["figure.subplot.left"] = 0.13
plt.rcParams["figure.subplot.right"] = 0.9

# フォント設定
plt.rcParams["font.family"] = "Harano Aji Mincho"
plt.rcParams["mathtext.fontset"] = "cm"  # Computer Modern

# 各部サイズ
plt.rcParams["font.size"] = 12
plt.rcParams["lines.markersize"] = 10
plt.rcParams["lines.linewidth"] = 3
plt.rcParams["axes.labelsize"] = 18
plt.rcParams["legend.fontsize"] = 14
```

`"font.family"`に指定するフォント名は、コンピュータにインストールされているものは
```python
import matplotlib.font_manager as fm
names = fm.get_font_names()
names.sort()
print("\n".join(names))
```
で確認できる。
フォント情報のキャッシュがwindowsでは`~/.matplotlib/fontlist-v390.json`、
linuxでは`~/.cache/matplotlib/fontlist-v390.json`とかに存在し、
新たにフォントをインストールしたらこれを削除して更新させる。


rcParamsで設定できる項目は
```python
import matplotlib
print(matplotlib.matplotlib_fname())
```
のファイルで確認するのが見やすい。



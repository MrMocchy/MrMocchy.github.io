
# PC Setup

## AutoHotkey

1. [公式サイト](https://www.autohotkey.com/)からv2.0をダウンロード、インストールする。
2. 以下のスクリプトを作成し適当に保存する。
```ahk title="startup.ahk"
;AHK v2.0

#SingleInstance Force

SetCapsLockState "AlwaysOff"

Insert::Backspace
\::Backspace
+\::Send "{Blind}{|}"

;*sc03A::{
;    ; CapsLockでの全角/半角切り替えの無効化
;}
```
3. Win+Rで`shell:startup`でスタートアップフォルダを開き、そこにスクリプトのショートカットを作成する。

## PowerToys

```powershell
winget install Microsoft.PowerToys --source winget
```
有効化するもの：

- 常に手前に表示 (Win+Ctrl+T)
- PowerToys Run (Alt+Space)
- Text Extractor (Win+Shift+T)
- Advanced Paste (メニュー：Win+Shift+V), (プレーンテキスト：Win+Ctrl+Alt+V)
- PowerRename
- Image Resizer

活用したいもの：

- ワークスペース
- New+ (Markdown)

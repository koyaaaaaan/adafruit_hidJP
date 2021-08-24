(For English speaker)
This project is for Japanese keyboard type 106 or 109.
Sorry to describe only in Japanese.

# adafruit_hidJPについて
Raspberry pi pico の Circuitpythonで提供されているUSBキーボードモジュールであるadafruit_hidの**日本語キーボード配列対応版**モジュールです。  
英語キーボードでは操作できない、アンダースコア・変換キーなどを送信することができます。


### 対応しているボード
Raspberry py Pico (要CircuitPythonインストール)


### 導入方法
CircuitPythonをRaspberry pi picoに導入後、以下のフォルダに配置してください
![/xxx/xxx/Circuitpython/lib/adafruit_hid/](folder.png)

その後、サンプルプログラムを Raspberry py Pico 内の code.py に書き込むことで動作します。
（必要に応じて、スイッチなどを自分で追加実装してください。）

# サンプルプログラム
### 文字列を送信
入力した文字をUSBキーボードとして送信するプログラム  
(Shiftキーは認識されます。Aと入力すればa+shiftとなります)
```
import usb_hid
from adafruit_hid.keycode import Keycode
from adafruit_hid.keyboard import Keyboard
from adafruit_hid.keyboard_layout_jp import KeyboardLayoutJP

keyboard = Keyboard(usb_hid.devices)
layout = KeyboardLayoutJP(keyboard)

# writeした文字列がPCに実際にタイプされたものとして送信されます
# キーボードの半角文字しか送れません。
# 全角を送りたい場合は全角ボタンを送信後にwriteする必要があります
layout.write("abc-ABC\+= ..,,<>@")

# タブを送信する場合はタブを直接指定してください
layout.write("tabtest  tabtest  tabtest")
```
 
### キーコード指定で送信
Functionキーなど、特殊キーを送信する場合はキーコードを指定します。
keycode.pyに羅列されています


特殊キーの送信の仕方サンプルプログラム
```
import usb_hid
from adafruit_hid.keycode import Keycode
from adafruit_hid.keyboard import Keyboard

keyboard = Keyboard(usb_hid.devices)

# キーコードは adafruit_hid/keycode.py を参照
# 通常の文字
keyboard.send(Keycode.A)
keyboard.send(Keycode.B)
keyboard.send(Keycode.ONE)
keyboard.send(Keycode.TWO)
keyboard.send(Keycode.SPACE)
keyboard.send(Keycode.COMMA)

# ファンクション等特殊キー
keyboard.send(Keycode.F1)
keyboard.send(Keycode.PRINT_SCREEN)
keyboard.send(Keycode.BACKSPACE)

# 複合キー
keyboard.send(Keycode.SHIFT, Keycode.A)
keyboard.send(Keycode.ALT, Keycode.A)
keyboard.send(Keycode.CONTROL, Keycode.S)
keyboard.send(Keycode.CONTROL,Keycode.SHIFT,Keycode.ALT, Keycode.A)
```


* ライブラリのディレクトリ構造

```
repository_directory
 |
 +- library_directory
 |   |
 |   +- library_script.py
 |   |
 |   +- __init__.py
 |
 +- setup.py
```

* 主題

```
from library_directory.library_script import *
```

ではなく

```
from library_script import *
```

と書きたい。

* 解決策

1. library_directoryディレクトリを他の名前に変更する(ここではcoreディレクトリとする)
2. 別に再びlibrary_directoryディレクトリを作成する。
3. library_directoryディレクトリの中にtoplevel.pyを以下の内容で作成する。

```
from core.library_script import *
```

4. library_directoryディレクトリ内の\_\_init\_\_.pyに以下の記述をする。

```
from library_directory.toplevel import *
```

* 最終的なディレクトリ構造

```
repository_directory
 |
 +- library_directory
 |   |
 |   +- __init__.py
 |   |
 |   +- toplevel.py
 |
 +- core
 |   |
 |   +- library_script.py
 |   |
 |   +- __init__.py
 |
 +- setup.py
```

* まとめ

こうすることで、
```
from library_directory import *
```
と書くと次のことが起こる。
1. library_directory.\_\_init\_\_.pyが呼ばれる。
2. その中に記述されている
```
from core.library_script import *
```
が実行される。

つまり、library_directoryをlibraryという名前にすれば
```
from library import *
```
と書くだけで複雑なディレクトリ構造のライブラリも一発でimportすることが可能になる。

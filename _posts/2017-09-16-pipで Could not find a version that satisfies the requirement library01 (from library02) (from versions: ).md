pipはdependency_linksを信用しないらしい。
なので、pipする際に--index-urlか--find-linksを明示的に指定してあげなければならない。

* 普通に実行
```
pip install "git+https://github.com/miyagaw61/enermemo.git#egg=enermemo"
```

失敗
```
Could not find a version that satisfies the requirement enert (from enermemo) (from versions: )
Cleaning up...
No matching distribution found for enert (from enermemo)
```

* 今度は--find-linksを指定して実行
```
pip install "git+https://github.com/miyagaw61/enermemo.git#egg=enermemo" --find-links="git+https://github.com/miyagaw61/enert.git#egg=enert"
```

これでも失敗する。
```
Could not find a version that satisfies the requirement enert (from enermemo) (from versions: )
Cleaning up...
No matching distribution found for enert (from enermemo)
```

実は、pipはバージョンが明記されていないものも信用しないらしい。
なのでバージョン情報も付ける必要があるようだ。

* バージョン情報も付与してpip実行
```
pip install "git+https://github.com/miyagaw61/enermemo.git#egg=enermemo" --find-links="git+https://github.com/miyagaw61/enert.git#egg=enert-0.0.1"
```

うまく入った。

最後の"-0.0.1"という部分がバージョンを表している。
pipがうまくパースしてくれるので、実際にとってきてくれるものはname=enertのままだ。

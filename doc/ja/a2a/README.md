[TOP](/README.md#top)　>　App to App

---

# App to App

## 目的

本稿では、A2Aモジュールを有効化する手順を説明します。<br>
A2Aモジュールは、その柔軟な広告フォーマットを通じて、新たな収益源を獲得することが可能となります。<br>
なお、つなぎこみのビジネス的背景に関するご質問は、営業担当宛てにお願い致します。

## AppToApp SDKのインポート

以下を`build.gradle`のdependenciesに追加してください。<br>
runaモジュールに加え、runa-a2aモジュールを追加します。

```gradle
  implementation 'com.rakuten.android.ads:runa:X.X.X'
  implementation 'com.rakuten.android.ads:runa-a2a:0.2.0'
```

## 実装

### キーワードによるターゲティング

`setKeywords()`メソッドでキーワードを指定します。

```kotlin
    AdView(context).apply {
        setKeywords(Keywords("PC", "MAC"))
    }.show()
```

その他の実装方法は[バナー広告](../bannerads/README.md)と同様となっていますので、そちらをご参照ください。


<br><br><br><br><br>
---
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/a2a/README.md)

[TOP](/README.md#top)　>　ビューアブルインプレッションの計測

---

# 検索広告におけるビューアブルインプレッションの計測

本機能は対象となる任意の View の視認性の計測を実行し、視認性の確立後にコールバックすることが可能です。
<br>

> ※ 本 API の利用は、楽天市場の検索 API を利用できるアプリが対象となります。

<br>

## View に対する視認性の監視

View の視認性監視には`ViewabilityProvider`クラスを使用します。<br>

### 監視する View の登録

View の監視を開始するには、`register`メソッドで対象の View と、その成果の送信先 URL を登録します。

`ViewabilityProvider$register(view: View, url: String, listener: ViewabilityListener)`

> `register`メソッドの引数<br>
>
> - `view` (必須) : 対象となる View
> - `url` (必須) : 成果の送信先 URL
> - `listener` (オプション) : 視認性が成立すると`onEstablished`がコールされます。

[実装例]

```java

val sampleTargetView = findViewById<LinearLayout>(R.id.sampleTarget)

ViewabilityProvider.register(sampleTargetView, "URL", object: ViewabilityListener {

  override fun onEstablished() {
      // Transmission completed
  }
})

```

> ※ register を実行するタイミングは、対象の View の描画が完了したタイミングが望ましいです。
>
> ※ `onEstablished`が呼ばれた後は、暗黙的に unregister するため、手動で`unregister`を実行する必要はありません。

<br>

### View の監視を解除

View の視認性の監視を途中で解除したい場合は、`unregister`メソッドを使用します。

`ViewabilityProvider$unregister(view: View)`

> `unregister`メソッドの引数<br>
>
> - `view` (必須) : 登録済みの View

```java
val sampleTargetView = findViewById<LinearLayout>(R.id.sampleTarget)

ViewabilityProvider.unregister(sampleTargetView)

```

<br>

### Open Measurement SDK の有効化

ビューアブルモジュールは Open Measurement SDK をサポートしています。<br>
`register` メソッドの第四引数に `OmNativeParameter` のインスタンスを渡すことにより、有効化できます。

```java

val sampleTargetView = findViewById<LinearLayout>(R.id.sampleTarget)

ViewabilityProvider.register(sampleTargetView, "URL", object: ViewabilityListener {

  override fun onEstablished() {
      // Transmission completed
  }
},
OmNativeParameter(
    "iabtechlab.com-omid",
    URL("https://s3-us-west-2.amazonaws.com/updated-omsdk-files/compliance-js/omid-validation-verification-script-v1-RAKUTEN-03142023.js"),
    "iabtechlab-Rakuten",
    URL("https://storage.googleapis.com/rssp-dev-cdn/sdk/js/omsdk-v1-1.4.3.js")
))

```

<br><br><br><br><br>

[TOP](../#top)

---

LANGUAGE :

> [![en](/doc/img/lang/en.png)](/doc/viewability/README.md)

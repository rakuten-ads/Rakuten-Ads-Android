[TOP](/README.md#top)　>　ビューアブルインプレッションの計測

---

# 検索広告におけるビューアブルインプレッションの計測

本機能は対象となる任意のViewの視認性の計測を実行し、視認性の確立後にコールバックすることが可能です。
<br>

> ※ 本APIの利用は、楽天市場の検索APIを利用できるアプリが対象となります。

<br>

## Viewに対する視認性の監視

Viewの視認性監視には`ViewabilityProvider`クラスを使用します。<br>

### 監視するViewの登録

Viewの監視を開始するには、`register`メソッドで対象のViewと、その成果の送信先URLを登録します。

`ViewabilityProvider$register(view: View, url: String, listener: ViewabilityListener)`

> `register`メソッドの引数<br>
>
> * `view` (必須) : 対象となるView
> * `url` (必須) : 成果の送信先URL
> * `listener` (オプション) : 視認性が成立すると`onEstablished`がコールされます。

[実装例]

```java

val sampleTargetView = findViewById<LinearLayout>(R.id.sampleTarget)

ViewabilityProvider.register(sampleTargetView, "URL", object: ViewabilityListener {

  override fun onEstablished() {
      // Transmission completed
  }
})

```

> ※ registerを実行するタイミングは、対象のViewの描画が完了したタイミングが望ましいです。
>
> ※ `onEstablished`が呼ばれた後は、暗黙的にunregisterするため、手動で`unregister`を実行する必要はありません。

<br>

### Viewの監視を解除

Viewの視認性の監視を途中で解除したい場合は、`unregister`メソッドを使用します。

`ViewabilityProvider$unregister(view: View)`

> `unregister`メソッドの引数<br>
>
> * `view` (必須) : 登録済みのView



```java
val sampleTargetView = findViewById<LinearLayout>(R.id.sampleTarget)

ViewabilityProvider.unregister(sampleTargetView)

```


<br><br><br><br><br>
---
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/img/lang/en.png)](/doc/viewability/README.md)

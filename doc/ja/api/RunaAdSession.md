[TOP](../#top)　>　[API](./README.md)　>　RunaAdSession

---

# RunaAdSession

[![support version](http://img.shields.io/badge/runa-1.2.0+-blueviolet.svg?style=flat)](https://developer.android.com)

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.RunaAdSession

複数のAdView間での重複を回避するためのオブジェクト。

### 公開メソッド

|戻り値|メソッド名|説明|
|:---:|:---|:---|
|void|bind([AdView](./AdView.md))|追加したAdView同士で表示される広告の重複を回避します。<br>本メソッドは[`AdView$show()`](./AdView.md#public_methods)よりも前に実行してください。|

### サンプルコード

```kotlin
import com.rakuten.android.ads.runa.AdView
import com.rakuten.android.ads.runa.AdStateListener
...

private val adSession = RunaAdSession()

...

override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        val adView1 = findViewById<AdView>(R.id.adview1)
        val adView2 = findViewById<AdView>(R.id.adview2)

        adSession.bind(adView1, adView2)


        adView1.apply {
              adStateListener = object: AdStateListener() {
                    override fun onLoadSuccess() {
                        adView2.show()
                    }
                    override fun onLoadFailure(adView: View?) {
                        adView2.show()
                    }
              }
        }.show()
}
...
```

> その他、[リスト表示で実装する場合のサンプル](../bannerads/sample_ad_session.md)はこちら

---
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/api/RunaAdSession.md)

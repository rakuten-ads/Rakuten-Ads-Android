[TOP](../#top)　>　[API](./README.md)　>　AdLoader

---

# AdLoader

[![support version](http://img.shields.io/badge/runa-1.3.0+-blueviolet.svg?style=flat)](https://developer.android.com)

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdLoader

一度に複数の広告をロードするためのオブジェクト。このクラスは内包する`Builder`クラスを用いてAdLoaderを生成し広告をロードします。

### 公開メソッド

|戻り値|メソッド名|説明|
:---:|:---|:---
void | execute() | 広告のロードを実行する。
List<AdView> | getAdViews() | 一括ロードに追加した[AdView](./AdView.md)を返します。
List<AdView> | getValidAdViews() | (Nullable) 正常に広告をロードできた[AdView](./AdView.md)のリストを返します。ロードが未完了の場合、nullを返します。
boolean | isLoading() | 広告がロード中かをbooleanで返します。

<div id="adLoader_builder"></div>

# Builder

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdLoader$Builder

AdLoaderを生成するためのBuilderクラス。広告のロードに必要に応じてBuilderパターンで各パラメータを設定します。

### コンストラクタ

|コンストラクタ|
|:---|
|Builder(Context context)|

### 公開メソッド

|戻り値|メソッド名|説明|
:---:|:---|:---
Builder | add([AdView](./AdView.md)... adViews) | 読み込みの対象となるAdViewを追加する。
Builder | with([AdLoaderStateListener](./AdLoaderStateListener.md) listener) | AdLoaderのロード状況の通知を受ける場合にAdLoaderStateListenerを追加します。
Builder | putProperty(String key, String value) | 必要に応じてプロパティを追加します。
Builder | putProperty(String key, int value) | 必要に応じてプロパティを追加します。
Builder | putProperty(String key, double value) | 必要に応じてプロパティを追加します。
Builder | putProperty(String key, long value) | 必要に応じてプロパティを追加します。
Builder | putProperty(String key, Bundle value) | 必要に応じてプロパティを追加します。
Builder | putProperty(String key, JSONObject value) | 必要に応じてプロパティを追加します。
AdLoader | build() | AdLoaderを生成します。


### サンプル

```kotlin
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        val adView1 = findViewById<AdView>(R.id.adview1).apply {
              tag = "adview1"
        }
        val adView2 = findViewById<AdView>(R.id.adview2)
        val adView3 = findViewById<AdView>(R.id.adview3)

        val adLoader = AdLoader.Builder(view.context)
            .add(adView1, adView2, adView3)
            .with(object: AdLoaderStateListener() {
                override fun onLoadSuccess(view: View?) {

                }
                override fun onLoadFailure(adView: View?, errorState: ErrorState) {
                      adView?.let { v ->
                        if (v.tag == "adview1") {
                           // Do something..
                        }
                      }
                }
                override fun onLoadAllComplete(adLoader: AdLoader, loadedAdViews: List<AdView>?) {
                      // Do something
                }
            })
            .build()
        adLoader.execute()
}
...
```
> ※ AdViewへのadSpotIdの設定はxml上で行われているものとしています。
>


---

* [API一覧](./README.md)

* [TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/api/AdLoader.md)

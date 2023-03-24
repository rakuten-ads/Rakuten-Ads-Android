[TOP](../#top)　>　バナー広告

---

# バナー広告

* **[1.広告サイズを指定する](#specify_adsize)**
* **[2.レイアウトXMLにAdViewを定義する](#define_adview_xml)**
* **[3.広告の状態を検知する](#detect_state)**
* **[4.複数のAdView間での重複排除](#avoid_duplication)**
* **[5.複数の広告を一度にロードする](#load_multiple)**
* **[6.AdSpotCodeを指定する](#set_adSpotCode)**
* **[7.AdSpotBranchIdを指定する](#set_adSpotBranchId)**
* **[8. ハードウェアアクセラレータを有効にする](#use_hardwareAccelerator)**
* **[9. テスト (サンプル広告枠Id)](#use_sample_adspot_id)**

---

<div id="specify_adsize"></div>

### 1. 広告サイズを指定する

`AdView`のサイズを指定するには `AdSize`を指定する必要があります。

enum class<br>

<details>
<summary>com.rakuten.android.ads.runa.AdSize</summary>

|種類|詳細|
|:---|:---|
|DEFAULT|ダッシュボードで設定したサイズ（AdSizeを指定しない場合は、DEFAULTで表示されます。）|
|ASPECT_FIT|画面横幅サイズに自動調整したサイズ|
|CUSTOM|標準サイズを下限に、画面横幅サイズを上限とした任意のサイズ(px)を指定することができます。<br>但し、この指定は広告の横幅のサイズと標準サイズの比率を基に算出されます。<br>指定可能なサイズ: (DEFAULT < `CUSTOM` < ASPECT_FIT)|

</details>

`AdSize`は以下のように指定することができます。

<details>
<summary><b>Javaによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Java-red.svg?style=flat)](https://www.java.com)

```java
AdView adView = new AdView(context);
adView.setAdSpotId(123);
adView.setAdViewSize(AdSize.ASPECT_FIT);
adView.show();
```
</details>
<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
AdView(context).apply {
  adSpotId = "123"
  adViewSize = AdSize.ASPECT_FIT
}.show()
```
</details>

---

<div id="define_adview_xml"></div>

### 2. レイアウトXMLでAdViewを定義して表示する

R.layout.activity_main
```xml
  <com.rakuten.android.ads.runa.AdView
        android:id="@+id/adview"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:adSpotId="@string/ad_spotid" />
```
> * `app:adSpotId` : 広告枠単位で発行されるユニークなID
>
> * ※ `layout_width`と`layout_height`には`wrap_content`"をセットしてください。AdViewが管理画面で設定した広告枠サイズに応じてサイズを適応します。

<details>
<summary><b>Javaによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Java-red.svg?style=flat)](https://www.java.com)

MainActivity.java
```java
import com.rakuten.android.ads.runa.AdView;

    ...
    @Overide
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ((AdView) findViewById(R.id.adview)).show();
    }
    ...  
```
</details>

<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

MainActivity.kt
```kotlin
import com.rakuten.android.ads.runa.AdView

    ...
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        findViewById<AdView>(R.id.adview).show()
    }
    ...  
```

</details>

---

<div id="detect_state"></div>

### 3. 広告の状態を検知する

広告の動作に応じてカスタマイズするには,以下のコードのように[`AdView`](../api/AdView.md)の`setAdStateListener`に[`AdStateListener`](../api/AdStateListener.md)クラスをセットすることで、イベントをフックします。
フックするイベントに応じて必要なメソッドを定義してください。

**AdStateListener**<br>
&nbsp;&nbsp;&nbsp;&nbsp;public abstract class
* `onLoadSuccess` : 広告の読み込みが成功した場合、このメソッドが呼ばれます。<br><br>
* `onLoadFailure` : 広告の読み込みが失敗した場合、このメソッドが呼ばれます。また、失敗した場合にAdViewは`View.INVISIBLE`となります。必要に応じてView.GONEにご設定ください。
  * [`ErrorState`](../api/ErrorState.md) : 広告リクエストでエラーが発生した時のステータスを示します。<br><br>
* `onClick` : 広告をクリックした際にこのメソッドが呼ばれます。<br><br>
* `onLeftApplication` : `onClick()`が呼ばれた後、ブラウザ（或いはアプリ）が立ち上がる際にこのメソッドが呼ばれます。<br><br>
* `onAdClose()` : 広告の目的のページ（或いはアプリ）からアプリに戻ってきた際にこのメソッドが呼ばれます。

<details>
<summary><b>Javaによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Java-red.svg?style=flat)](https://www.java.com)

```java
import com.rakuten.android.ads.runa.AdStateListener;
...

AdView ad = (AdView) findViewById(R.id.adview);
ad.setAdStateListener(new AdStateListener() {
    @Override
    public void onLoadSuccess() {
        // 広告が読み込みが成功した場合
    }

    @Override
    public void onLoadFailure(@Nullable View adView) {
        // 広告の読み込みが失敗した場合
        if (adView != null) adView.setVisibility(View.GONE);
    }

    @Override
    public void onClick(@Nullable View adView) {
        // 広告がクリックされた場合
    }
});
ad.show();
```
</details>
<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.AdStateListener
...

findViewById<AdView>(R.id.adview).apply {
    adStateListener = object : AdStateListener() {

        override fun onLoadSuccess() {
            // 広告が読み込みが成功した場合
        }

        override fun onLoadFailure(adView: View?) {
            // 広告の読み込みが失敗した場合
            visibility = View.GONE
        }

        override fun onClick(adView: View?) {
            // 広告がクリックされた場合
        }
}.show()
```
</details>

---

<div id="avoid_duplication"></div>

### 4. 複数のAdView間での重複排除

[![support version](http://img.shields.io/badge/runa-1.2.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.2.0)

　同一の画面にAdViewを複数個設置した際に、表示される広告コンテンツの重複を回避するには`RunaAdSession`を利用します。<br>
RunaAdSessionの`bind`メソッドに複数のAdViewを指定することで、それらのAdViewで表示される広告の重複を回避します。<br>
また、`bind`メソッドに指定したAdViewの`show`メソッドを実行する際は、それらの時間的間隔を空けて実行してください。<br>
(先にbindしたAdViewの広告データを、次にbindしたAdViewの読み込み時に参照しているためです。)<br>
以下の実装方法は必ずしも必要ではありませんが、AdView1とAdView2で表示コンテンツの重複を回避する実装例となります。<br>

<details>
<summary><b>Javaによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Java-red.svg?style=flat)](https://www.java.com)

```java
import com.rakuten.android.ads.runa.AdView;
import com.rakuten.android.ads.runa.AdStateListener;
...

private final RunaAdSession adSession = RunaAdSession();

...

@Override
fun onViewCreated(View view, Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        AdView adView1 = (AdView) findViewById(R.id.adview1);
        AdView adView2 = (AdView) findViewById(R.id.adview2);

        adSession.bind(adView1, adView2);

        adView1.setAdStateListener(new AdStateListener() {
                    override fun onLoadSuccess() {
                        adView2.show();
                    }
                    override fun onLoadFailure(View adView) {
                        adView2.show();
                    }
              });
        }
        adView1.show();
}
...
```
> ※ adView2のshowメソッドのコールはAdView1の読み込み完了後に実行されるように実装する必要があります。

</details>

<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

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
> ※ adView2のshowメソッドのコールはAdView1の読み込み完了後に実行されるように実装する必要があります。

</details>

> ※ [その他実装サンプル](./sample_ad_session.md)

---

<div id="load_multiple"></div>

### 5. 複数の広告を一度にロードする

[![support version](http://img.shields.io/badge/runa-1.3.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.3.0)

　カルーセル広告などを表示するなど、一度のロードで複数の広告を表示する場合に[`AdLoader`](../api/AdLoader.md)を利用します。<br>
AdLoaderはBuilderパターンで構成されており、[`AdLoader$Builder`](../api/AdLoader.md#adLoader_builder)クラスを定義して広告のロードに必要なパラメータを追加する必要があります。<br>
Builderには描画させたいAdViewを追加し、AdLoaderの読み込み状況を検知するための[`AdLoaderStateListener`](../api/AdLoaderStateListener.md)を必要に応じてセットしていきます。<br>
Builderへのパラメータの追加後は`build`メソッドでAdLoaderを生成し、AdLoaderは`execute`メソッドを実行することでロードを開始します。<br>
ロードが開始すると、読み込みが完了したAdViewから描画がされていきます。この時、描画の順序を制御することはできません。<br>
また、AdLoaderで広告を読み込む場合、排他排除機能を含むため前項(5. 複数のAdView間での重複排除)の`RunaAdSession`を用いた重複排除の実装は不要となります。

<details>
<summary><b>Javaによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Java-red.svg?style=flat)](https://www.java.com)

```java
@Override
fun onViewCreated(View view, Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState)
        AdView adView1 = (AdView) findViewById(R.id.adview1);
        adView1.setTag("adview1");

        AdView adView2 = (AdView) findViewById(R.id.adview2);
        AdView adView3 = (AdView) findViewById(R.id.adview3);

        AdLoader adLoader = new AdLoader.Builder(view.context)
            .add(adView1, adView2, adView3)
            .with(new AdLoaderStateListener() {
                @Override
                public void onLoadSuccess(view: View?) {

                }
                @Override
                public void onLoadFailure(adView: View?, errorState: ErrorState) {
                      adView?.let { v ->
                        if (v.tag == "adview1") {
                           // Do something..
                        }
                      }
                }
                @Override
                public void onAllLoadsFinished(adLoader: AdLoader, loadedAdViews: List<AdView>?) {
                      // Do something
                }
            })
            .build();
      adLoader.execute();
}
...
```
> ※ AdViewへのadSpotIdの設定はxml上で行われているものとしています。

</details>
<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

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
                override fun onAllLoadsFinished(adLoader: AdLoader, loadedAdViews: List<AdView>?) {
                      // Do something
                }
            })
            .build()
        adLoader.execute()
}
...
```
> ※ AdViewへのadSpotIdの設定はxml上で行われているものとしています。
</details>

---

<div id="set_adSpotCode"></div>

### 6. AdSpotCodeを指定する

[![support version](http://img.shields.io/badge/runa-1.5.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.5.0)

<details>
<summary><b>Javaによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Java-red.svg?style=flat)](https://www.java.com)

```java
import com.rakuten.android.ads.runa.AdView;

    ...
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        AdView adView = (AdView) findViewById(R.id.adview);
        adView.setAdSpotCode("{AD_SPOT_CODE}");
        adView.show();
    }
    ...  
```
</details>
<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.AdView

    ...
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        findViewById<AdView>(R.id.adview).apply {
            adSpotCode = "{AD_SPOT_CODE}"
        }.show()
    }
    ...  
```
</details>

<div id="set_adSpotBranchId"></div>

### 7. Ad Spot Branch IDを指定する

[![support version](http://img.shields.io/badge/runa-1.8.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.8.0)

画面内に、複数のAdViewに対して同一のAdSpotIDを指定した場合に<br>
AdSpotBranchIdを指定することで、レポート画面にてそれらを区別することができます。<br>
adSpotBranchIdには`AdSpotBranch`を指定します。

```kotlin
import com.rakuten.android.ads.runa.key.AdSpotBranch

binding.adView1.adSpotId = "111"
binding.adView1.AdSpotBranchId = AdSpotBranch.ID_1

binding.adView2.adSpotId = "111"
binding.adView2.AdSpotBranchId = AdSpotBranch.ID_2

binding.adView3.adSpotId = "111"
binding.adView3.AdSpotBranchId = AdSpotBranch.ID_3
```


<div id="use_hardwareAccelerator"></div>

### 8. ハードウェアアクセラレータを有効にする

[![support version](http://img.shields.io/badge/runa-1.8.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.8.0)

<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.AdView
import com.rakuten.android.ads.runa.key.Config

    ...
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        findViewById<AdView>(R.id.adview).apply {
            putProperty(Config.HardwareAcceleration.key, true)
        }.show()
    }
    ...  
```
</details>

<div id="use_sample_adspot_id"></div>

### 9. Test (Sample AdSpotId)

以下の広告枠IDでサンプル表示が可能です。<br>
正しく実装ができているかをご確認ください。

|サンプル広告枠ID|Size|Image|
|:---:|:---:|:---:|
|18261|300 x 250|<img src="/doc/img/dummy_ads/dummy01_300x250.png" width=300px />|
|18262|300 x 50|<img src="/doc/img/dummy_ads/dummy02_320x50.png" width=300px />|
|18263|300 x 100|<img src="/doc/img/dummy_ads/dummy03_320x100.png" width=300px />|
|18264|160 x 600|<img src="/doc/img/dummy_ads/dummy04_160x600.png" height=400px />|
|18265|729 x 90|<img src="/doc/img/dummy_ads/dummy05_728x90.jpeg" width=300px />|
|18266|336 x 280|<img src="/doc/img/dummy_ads/dummy06_336x280.png" width=300px />|
|18267|970 x 90|<img src="/doc/img/dummy_ads/dummy07_970x90.jpeg" width=300px />|
|18268|970 x 250|<img src="/doc/img/dummy_ads/dummy08_970x250.jpeg" width=300px />|
|18269|300 x 600|<img src="/doc/img/dummy_ads/dummy09_300x600.png" width=300px />|

---
[TOP](../#top)

[バナー広告拡張モジュール](/doc/ja/extension/README.md)

---
LANGUAGE :
> [![en](/doc/img/lang/en.png)](/doc/bannerads/README.md)

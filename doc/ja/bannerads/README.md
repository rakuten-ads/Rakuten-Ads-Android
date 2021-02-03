[TOP](../#top)　>　バナー広告

---

# バナー広告

* **[1.広告サイズを指定する](#specify_adsize)**
* **[2.レイアウトXMLにAdViewを定義する](#define_adview_xml)**
* **[3.Javaによる実装](#implement_java)**
* **[4.Kotlinによる実装](#implement_kotlin)**
* **[5.複数のAdView間での重複排除](#avoid_duplication)**

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

```java
AdView adView = new AdView(context);
adView.setAdSpotId(123);
adView.setAdViewSize(AdSize.ASPECT_FIT);
adView.show();
```

<div id="define_adview_xml"></div>

### 2. レイアウトXMLにAdViewを定義する

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

<div id="implement_java"></div>

### 3. Javaによる実装

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


#### 広告の状態を検知する

広告の動作に応じてカスタマイズするには,以下のコードのように[`AdView`](../api/AdView.md)の`setAdStateListener`に[`AdStateListener`](../api/AdStateListener.md)クラスをセットすることで、イベントをフックします。
フックするイベントに応じて必要なメソッドを定義してください。

```java
import com.rakuten.android.ads.runa.AdStateListener;
...

AdView ad = ((AdView) findViewById(R.id.adview))
                .setAdStateListener(new AdStateListener() {
                      @Override
                      public void onLoadSuccess() {
                            // 広告が読み込みが成功した場合
                      }

                      @Override
                      public void onLoadFailure(@Nullable View adView) {
                            // 広告の読み込みが失敗した場合
                            adView.setVisibility(View.GONE);
                      }

                      @Override
                      public void onClick(@Nullable View adView) {
                            // 広告がクリックされた場合
                      }
                });
ad.show();
```

**AdStateListener**<br>
&nbsp;&nbsp;&nbsp;&nbsp;public abstract class
* `onLoadSuccess` : 広告の読み込みが成功した場合、このメソッドが呼ばれます。<br><br>
* `onLoadFailure` : 広告の読み込みが失敗した場合、このメソッドが呼ばれます。また、失敗した場合にAdViewは`View.INVISIBLE`となります。必要に応じてView.GONEにご設定ください。
  * [`ErrorState`](../api/ErrorState.md) : 広告リクエストでエラーが発生した時のステータスを示します。<br><br>
* `onClick` : 広告をクリックした際にこのメソッドが呼ばれます。<br><br>
* `onLeftApplication` : `onClick()`が呼ばれた後、ブラウザ（或いはアプリ）が立ち上がる際にこのメソッドが呼ばれます。<br><br>
* `onAdClose()` : 広告の目的のページ（或いはアプリ）からアプリに戻ってきた際にこのメソッドが呼ばれます。


---
<div id="implement_kotlin"></div>

### 4. Kotlinによる実装

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

MainActivity.kt
```kotlin
import com.rakuten.android.ads.runa.AdView

    ...
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        findViewById<AdView>(R.id.adview).show();
    }
    ...  
```

#### 広告の状態を検知する

```kotlin
import com.rakuten.android.ads.runa.AdView
import com.rakuten.android.ads.runa.AdStateListener
...

findViewById<AdView>(R.id.adview)
.apply {
      adStateListener = object: AdStateListener() {

            override fun onLoadSuccess() {
                // 広告の読み込みが成功した場合

            }

            override fun onLoadFailure(adView: View?) {
                // 広告の読み込みが失敗した場合
                adView?.let {
                    it.visibility = View.GONE
                }
            }

            override fun onClick(adView: View?) {
                // 広告がクリックされた場合

            }
      }
}
.show()
```

<div id="avoid_duplication"></div>

### 5. 複数のAdView間での重複排除

同一の画面にAdViewを複数個設置した際に、表示される広告コンテンツの重複を回避するには`RunaAdSession`を利用します。<br>
RunaAdSessionの`bind`メソッドに複数のAdViewを指定することで、それらのAdViewで表示される広告の重複を回避します。<br>
また、`bind`メソッドに指定したAdViewの`show`メソッドを実行する際は、それらの時間的間隔を空けて実行してください。<br>
(先にbindしたAdViewの広告データを、次にbindしたAdViewの読み込み時に参照しているためです。)<br>
以下の実装方法は必ずしも必要ではありませんが、AdView1とAdView2で表示コンテンツの重複を回避する実装例となります。<br>

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




---
[TOP](../#top)

[バナー広告拡張モジュール](/doc/ja/extension/README.md)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/bannerads/README.md)

[TOP](../#top)　>　バナー広告

---

# バナー広告

* **[Javaによる実装](#implement_java)**
* **[Kotlinによる実装](#implement_kotlin)**

---

R.layout.activity_main
```xml
  <com.rakuten.android.ads.rps.AdView
        android:id="@+id/adview"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:adSpotId="@string/ad_spotid" />
```
> * `app:adSpotId` : 広告枠単位で発行されるユニークなID
>
> * ※ `layout_width`と`layout_height`には`wrap_content`"をセットしてください。AdViewが管理画面で設定した広告枠サイズに応じてサイズを適応します。

<div id="implement_java"></div>

[![Language](http://img.shields.io/badge/language-Java-red.svg?style=flat)](https://www.java.com)

MainActivity.java
```java
import com.rakuten.android.ads.rps.AdView;

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
import com.rakuten.android.ads.rps.AdStateListener;
...

((AdView) findViewById(R.id.adview))
          .setAdStateListener(new AdStateListener() {
                @Override
                public void onLoadSuccess() {
                      // 広告が読み込みが成功した場合
                }

                @Override
                public void onLoadFailure(@Nullable View v) {
                      // 広告の読み込みが失敗した場合
                }

                @Override
                public void onClick(@Nullable View v) {
                      // 広告がクリックされた場合
                }
          })
          .show();
```

**AdStateListener**<br>
&nbsp;&nbsp;&nbsp;&nbsp;public abstract class
* `onLoadSuccess` : 広告の読み込みが成功した場合、このメソッドが呼ばれます。
* `onLoadFailure` : 広告の読み込みが失敗した場合、このメソッドが呼ばれます。また、失敗した場合にAdViewは`View.INVISIBLE`となります。必要に応じてView.GONEにご設定ください。
* `onClick` : 広告をクリックした際にこのメソッドが呼ばれます。
* `onLeftApplication` : `onClick()`が呼ばれた後、ブラウザ（或いはアプリ）が立ち上がる際にこのメソッドが呼ばれます。
* `onAdClose()` : 広告の目的のページ（或いはアプリ）からアプリに戻ってきた際にこのメソッドが呼ばれます。


---
<div id="implement_kotlin"></div>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

MainActivity.kt
```kotlin
import com.rakuten.android.ads.rps.AdView

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
import com.rakuten.android.ads.rps.AdStateListener
...

findViewById<AdView>(R.id.adview).setAdStateListener(object: AdStateListener() {

            override fun onLoadSuccess() {
                // 広告の読み込みが成功した場合

            }

            override fun onLoadFailure(v: View?) {
                // 広告の読み込みが失敗した場合

            }

            override fun onClick(v: View?) {
                // 広告がクリックされた場合

            }
        }).show()
```


---
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/bannerads/README.md)

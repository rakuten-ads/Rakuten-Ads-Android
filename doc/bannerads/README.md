[TOP](/README.md#top)　>　Banner Ads

---

# Banner Ads

* **[1. Specify Ad Size](#specify_adsize)**
* **[2. Define AdView in layout xml](#define_adview_xml)**
* **[3. Implement by Java](#implement_java)**
* **[4. Implement by Kotlin](#implement_kotlin)**
* **[5. Avoid duplicates between multiple AdView](#avoid_duplication)**

---

<div id="specify_adsize"></div>

### 1. Specify ad size

You need to specify `AdSize` to adjust the size of the `AdView`.<br>
AdSize is enum class.

<details>
<summary>com.rakuten.android.ads.runa.AdSize</summary>

|Size Type|Desciption|
|:---|:---|
|DEFAULT|The ad size set in DashBoard.|
|ASPECT_FIT|Fit in display width.|
|CUSTOM|Can be specified to any size.<br>However, this specify is calculated based on the width.<br>Specifiable range: (DEFAULT < `CUSTOM` < ASPECT_FIT)|

</details>

Set this AdSize to setAdViewSize of AdView.

```java
AdView adView = new AdView(context);
adView.setAdSpotId(123);
adView.setAdViewSize(AdSize.ASPECT_FIT);
```

<div id="define_adview_xml"></div>

### 2. Define AdView in layout xml

R.layout.activity_main
```xml
  <com.rakuten.android.ads.runa.AdView
        android:id="@+id/adview"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:adSpotId="@string/ad_spotid"
        app:adSpotSize="AspectFit" />
```
> * `app:adSpotId` : It is unique identifier what is issued per position where ad is to be displayed.
>
> * ※ `layout_width`, `layout_height` : The both parameters always sets "`wrap_content`". AdView is sized automatically according to set adspot size on console.

<div id="implement_java"></div>

### 3. Implement by Java

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

#### Hook ad states

To further customize the behavior of you ad, you can hook a number of events in the AdView's each one. You can catch for each events through an [`AdStateListener`](../api/AdStateListener.md) class.

Below sample code is to use an [`AdStateListener`](../api/AdStateListener.md). Simply call the `setAdStateListener` method of AdView.

```java
import com.rakuten.android.ads.runa.AdStateListener;
...

AdView ad = ((AdView) findViewById(R.id.adview))
                .setAdStateListener(new AdStateListener() {
                      @Override
                      public void onLoadSuccess() {
                            // Code to be executed when an ad finishes loading successfully.
                      }

                      @Override
                      public void onLoadFailure(@Nullable View adView, ErrorState errorState) {
                            // Code to be executed when an ad finishes loading failure.
                            adView.setVisibility(View.GONE);
                      }

                      @Override
                      public void onClick(@Nullable View adView) {
                            // Code to be executed when clicked an ad.
                      }
                });
ad.show();
```

**AdStateListener**<br>
&nbsp;&nbsp;&nbsp;&nbsp;public abstract class
* `onLoadSuccess` : It is called this method, if it is loaded an advertise successfully.<br><br>
* `onLoadFailure` : It is called this method, in case of loaded an advertise failure. And if it failed, AdView will be hidden(`View.INVISIBLE`) automatically.
  * [`ErrorState`](../api/ErrorState.md) : Indicates the status when an error occurred in AdRequest.<br><br>
* `onClick` : It is called this method, if it is clicked an advertise. &nbsp; (e.g. You use this method in case of to detect that clicked ad.)<br><br>
* `onLeftApplication` : This method is called after `onClick()` when a user click opens browser(transition to ad's destination URL).<br><br>
* `onAdClose()` : When a user returns to the app after viewing an ad's destination URL, this method is called.

---
<div id="implement_kotlin"></div>

### 4. Implement by Kotlin

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

#### Hook ad states

```kotlin
import com.rakuten.android.ads.runa.AdStateListener
...

findViewById<AdView>(R.id.adview)
.apply {
      adStateListener = object: AdStateListener() {

            override fun onLoadSuccess() {
                // Code to be executed when an ad finishes loading successfully

            }

            override fun onLoadFailure(adView: View?, errorState: ErrorState) {
                // Code to be executed when an ad finishes loading failure.
                adView?.let {
                    it.visibility = View.GONE
                }
            }

            override fun onClick(adView: View?) {
                // Code to be executed when clicked an ad.

            }
      }
}
.show()
```

<div id="avoid_duplication"></div>

### 5. Avoid duplicates between multiple AdView

[![support version](http://img.shields.io/badge/runa-1.2.0+-blueviolet.svg?style=flat)](https://developer.android.com)

　Uses [`RunaAdSession`](../api/RunaAdSession.md) to avoid duplication of display ad content, in case of sets multiple AdView on same Screen.<br>
Sets multiple AdView to the `RunaAdSession$bind` method to avoid duplication of ads display in those AdViews.<br>
And, when set multiple AdView in the `bind` method, allow an interval to execute those `show` method, because browse to the ads loaded of the previously bound AdView.<br>
Below is just a sample to avoid duplication of content in AdView1 and AdView2. It's not necessarily required.

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
                    override fun onLoadFailure(adView: View?, errorState: ErrorState) {
                        adView2.show()
                    }
              }
        }.show()
}
...
```

> ※ `show()` method of AdView2 must be call after load AdView1 completed.
>
> ※ [Other implementation sample](./sample_ad_session.md)

### 6. Load multiple ads at once

[![support version](http://img.shields.io/badge/runa-1.3.0+-blueviolet.svg?style=flat)](https://developer.android.com)

 Use [`AdLoader`](../api/AdLoader.md) to display multiple ads with one load, such as displaying carousel ads.<br>
AdLoader consists of a Builder pattern, so need to declare the [`AdLoader$Builder`](../api/AdLoader.md#adLoader_builder) class and add some parameters to load ads.<br>
Add AdView to draw with the Builder, and sets [`AdLoaderStateListener`](../api/AdLoaderStateListener.md) to detect the loading status of AdLoader as needed. Generates AdLoader with `build` method after added parameters to the Builder, AdLoader starts loading ads that uses `execute` method.
 When loading starts, the loaded AdView will be drawn in sequence. At this time, the drawing order cannot be controlled.
Also, when loading ads with AdLoader, you don't need to implement deduplication with the previous item [`RunaAdSession`](#avoid_duplication), because this includes deduplication functionality.

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
> ※ This sample is assumed that the adSpotId setting for AdView is done on layout xml.

---
[TOP](/README.md#top)

[BannerAds Extension](/doc/extension/README.md)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/ja/bannerads/README.md)

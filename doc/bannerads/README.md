[TOP](/README.md#top)　>　 Banner Ads

---

# Banner Ads

- **[1. Specify Ad Size](#specify_adsize)**
- **[2. Define AdView in layout xml](#define_adview_xml)**
- **[3. Detect ads state](#detect_state)**
- **[4. Avoid duplicates between multiple AdView](#avoid_duplication)**
- **[5. Load multiple ads at once](#load_multiple)**
- **[6. Use AdSpotCode](#use_adSpotCode)**
- **[7. Set AdSpotBranchId](#set_adSpotBranchId)**
- **[8. Use HardwareAccelerator](#use_hardwareAccelerator)**
- **[9. Test (Sample AdSpotId)](#use_sample_adspot_id)**
- **[10. Custom usages at clicking](#custom_usages_at_clicking)**

---

<div id="specify_adsize"></div>

### 1. Specify ad size

You need to specify `AdSize` to adjust the size of the `AdView`.<br>
AdSize is enum class.

<details>
<summary>com.rakuten.android.ads.runa.AdSize</summary>

| Size Type     | Desciption                                                                                                                                       |
| :------------ | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| DEFAULT       | The ad size set in DashBoard.                                                                                                                    |
| ASPECT_FIT    | Fit in display width.                                                                                                                            |
| CUSTOM        | Can be specified to any size.<br>However, this specify is calculated based on the width.<br>Specifiable range: (DEFAULT < `CUSTOM` < ASPECT_FIT) |
| UNSAFE_CUSTOM | Can be specified to any size(pixel).<br>This mode ignores the size of an ad content, please carefully use it.                                    |
| FULL_SCREEN   | This size can be enabled only in Interstitial Ad.<br> WebView displaying ad contents will be extended to a screen size                           |

</details>

Set this AdSize to setAdViewSize of AdView.

<details>
<summary><b>Kotlin</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
AdView(context).apply {
  adSpotId = "123"
  adViewSize = AdSize.ASPECT_FIT
}.show()
```

</details><br>
<details>
<summary><b>Java</b></summary>

[![Language](http://img.shields.io/badge/language-Java-red.svg?style=flat)](https://www.java.com)

```java
AdView adView = new AdView(context);
adView.setAdSpotId(123);
adView.setAdViewSize(AdSize.ASPECT_FIT);
```

</details>

---

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

> - `app:adSpotId` : It is unique identifier what is issued per position where ad is to be displayed.
>
> - ※ `layout_width`, `layout_height` : The both parameters always sets "`wrap_content`". AdView is sized automatically according to set adspot size on console.

<details>
<summary><b>Kotlin</b></summary>

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

</details><br>
<details>
<summary><b>Java</b></summary>

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

---

<div id="detect_state"></div>

### 3. Detect ads state

To further customize the behavior of you ad, you can hook a number of events in the AdView's each one. You can catch for each events through an [`AdStateListener`](../api/AdStateListener.md) class.

Below sample code is to use an [`AdStateListener`](../api/AdStateListener.md). Simply call the `setAdStateListener` method of AdView.

**AdStateListener**<br>
&nbsp;&nbsp;&nbsp;&nbsp;public abstract class

- `onLoadSuccess` : It is called this method, if it is loaded an advertise successfully.<br><br>
- `onLoadFailure` : It is called this method, in case of loaded an advertise failure. And if it failed, AdView will be hidden(`View.INVISIBLE`) automatically.
  - [`ErrorState`](../api/ErrorState.md) : Indicates the status when an error occurred in AdRequest.<br><br>
- `onClick` : It is called this method, if it is clicked an advertise. &nbsp; (e.g. You use this method in case of to detect that clicked ad.)
  - You can get the click url from View which is the first argument of `onClick(adView: View?)` by casting to AdView.<br><br>
- `onLeftApplication` : This method is called after `onClick()` when a user click opens browser(transition to ad's destination URL).<br><br>
- `onAdClose()` : When a user returns to the app after viewing an ad's destination URL, this method is called.

<details>
<summary><b>Kotlin</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.AdStateListener
...

findViewById<AdView>(R.id.adview).apply {
    adStateListener = object : AdStateListener() {

        override fun onLoadSuccess() {
            // Code to be executed when an ad finishes loading successfully
        }

        override fun onLoadFailure(adView: View?) {
            // Code to be executed when an ad finishes loading failure.
            adView?.let {
              it.visibility = View.GONE
            }
        }

        override fun onClick(adView: View?) {
            // Code to be executed when clicked an ad.

            // You can get the click url.
            val clickUrl = (adView as AdView).clickUrl
        }
}.show()
```

</details><br>
<details>
<summary><b>Java</b></summary>

[![Language](http://img.shields.io/badge/language-Java-red.svg?style=flat)](https://www.java.com)

```java
import com.rakuten.android.ads.runa.AdStateListener;
...

AdView ad = (AdView) findViewById(R.id.adview);
ad.setAdStateListener(new AdStateListener() {
    @Override
    public void onLoadSuccess() {
        // Code to be executed when an ad finishes loading successfully.
    }

    @Override
    public void onLoadFailure(@Nullable View adView) {
        // Code to be executed when an ad finishes loading failure.
        if (adView != null) adView.setVisibility(View.GONE);
    }

    @Override
    public void onClick(@Nullable View adView) {
        // Code to be executed when clicked an ad.

        // You can get the click url.
        String clickUrl = (AdView)adView.clickUrl
    }
});
ad.show();
```

</details>

---

<div id="avoid_duplication"></div>

### 4. Avoid duplicates between multiple AdView

[![support version](http://img.shields.io/badge/runa-1.2.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.2.0)

Uses [`RunaAdSession`](../api/RunaAdSession.md) to avoid duplication of display ad content, in case of sets multiple AdView on same Screen.<br>
Sets multiple AdView to the `RunaAdSession$bind` method to avoid duplication of ads display in those AdViews.<br>
And, when set multiple AdView in the `bind` method, allow an interval to execute those `show` method, because browse to the ads loaded of the previously bound AdView.<br>
Below is just a sample to avoid duplication of content in AdView1 and AdView2. It's not necessarily required.

<details>
<summary><b>Kotlin</b></summary>

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
                    override fun onLoadFailure(adView: View?, errorState: ErrorState) {
                        adView2.show()
                    }
              }
        }.show()
}
...
```

> ※ `show()` method of AdView2 must be call after load AdView1 completed.

</details><br>
<details>
<summary><b>Java</b></summary>

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

> ※ adView2 の show メソッドのコールは AdView1 の読み込み完了後に実行されるように実装する必要があります。

</details>

> ※ [Other implementation sample](./sample_ad_session.md)

---

<div id="load_multiple"></div>

### 5. Load multiple ads at once

[![support version](http://img.shields.io/badge/runa-1.3.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.3.0)

Use [`AdLoader`](../api/AdLoader.md) to display multiple ads with one load, such as displaying carousel ads.<br>
AdLoader consists of a Builder pattern, so need to declare the [`AdLoader$Builder`](../api/AdLoader.md#adLoader_builder) class and add some parameters to load ads.<br>
Add AdView to draw with the Builder, and sets [`AdLoaderStateListener`](../api/AdLoaderStateListener.md) to detect the loading status of AdLoader as needed. Generates AdLoader with `build` method after added parameters to the Builder, AdLoader starts loading ads that uses `execute` method.
When loading starts, the loaded AdView will be drawn in sequence. At this time, the drawing order cannot be controlled.
Also, when loading ads with AdLoader, you don't need to implement deduplication with the previous item [`RunaAdSession`](#avoid_duplication), because this includes deduplication functionality.

<details>
<summary><b>Kotlin</b></summary>

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

> ※ This sample is assumed that the adSpotId setting for AdView is done on layout xml.

</details><br>
<details>
<summary><b>Java</b></summary>

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

> ※ This sample is assumed that the adSpotId setting for AdView is done on layout xml.

</details>

---

<div id="use_adSpotCode"></div>

### 6. Use AdSpotCode

[![support version](http://img.shields.io/badge/runa-1.5.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.5.0)

<details>
<summary><b>Kotlin</b></summary>

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

</details><br>
<details>
<summary><b>Java</b></summary>

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

<div id="set_adSpotBranchId"></div>

### 6. Set AdSpotBranch ID

[![support version](http://img.shields.io/badge/runa-1.8.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.8.0)

If you specify the same AdSpotID for multiple AdViews on the screen,<br>
By specifying AdSpotBranchId, you can distinguish between them in the report screen of Runa.<br>
Specify `AdSpotBranch` for adSpotBranchId.

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

### 8. User HardwareAccelerator

[![support version](http://img.shields.io/badge/runa-1.8.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.8.0)

<details>
<summary><b>Kotlin</b></summary>

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

Sample display is possible with the following AdSpot ID.<br>
Please make sure if it is implemented correctly.

| Sample AdSpot ID |   Size    |                               Image                               |
| :--------------: | :-------: | :---------------------------------------------------------------: |
|      18261       | 300 x 250 | <img src="/doc/img/dummy_ads/dummy01_300x250.png" width=300px />  |
|      18262       | 320 x 50  |  <img src="/doc/img/dummy_ads/dummy02_320x50.png" width=300px />  |
|      18263       | 320 x 100 | <img src="/doc/img/dummy_ads/dummy03_320x100.png" width=300px />  |
|      18264       | 160 x 600 | <img src="/doc/img/dummy_ads/dummy04_160x600.png" height=400px /> |
|      18265       | 728 x 90  | <img src="/doc/img/dummy_ads/dummy05_728x90.jpeg" width=300px />  |
|      18266       | 336 x 280 | <img src="/doc/img/dummy_ads/dummy06_336x280.png" width=300px />  |
|      18267       | 970 x 90  | <img src="/doc/img/dummy_ads/dummy07_970x90.jpeg" width=300px />  |
|      18268       | 970 x 250 | <img src="/doc/img/dummy_ads/dummy08_970x250.jpeg" width=300px /> |
|      18269       | 300 x 600 | <img src="/doc/img/dummy_ads/dummy09_300x600.png" width=300px />  |

<div id="custom_usages_at_clicking"></div>

### 9. Custom usages of clicking ads

When users click AdView, the behavior of opening url depends on target attribute of anchor tag inside the creative.<br>
However, you can control that with Click Delegation function.

#### <a target="_top">

You can get control the behavior at clicking `AdView` on your client with the click delegation function.

```kotlin
class AdViewFragment : Fragment() {
    private lateinit var binding: FragmentAdViewBinding

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)

        adview.apply {
            // Click delegation is enabled with the line
            putProperty("c11c51790bac6cbee0e0483576148145", Delegator.ClickDelegation)

            adStateListener = object : AdLoaderStateListener() {
                override fun onClick(view: View?, errorState: ErrorState?) {
                    val clickUrl = (view as AdView).clickUrl
                    Log.d("Click URL", clickUrl)

                    // Show the page of click url set in RUNA in your WebView
                    binding.yourWebView.webViewClient = WebViewClient()
                    binding.yourWebView.loadUrl(clickUrl)

                    // Show the the page of click url set in RUNA in external browser
                    val intent = Intent(Intent.ACTION_VIEW, Uri.parse(url))
                    startActivity(intent)
                }
            }
        }.show()
    }
}
```

#### <a target="_self">

It’s basically impossible extent the page of click url in WebView inside `AdView` due to content security policy with X-Frame-Options: DENY error.<br>
We recommend you should change the value of `target` attribute of anchor tags in your creative to "\_top".

---

[TOP](/README.md#top)

[BannerAds Extension](/doc/extension/README.md)

---

LANGUAGE :

> [![ja](/doc/img/lang/ja.png)](/doc/ja/bannerads/README.md)

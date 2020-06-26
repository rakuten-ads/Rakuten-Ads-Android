[TOP](/README.md#top)　>　Banner Ads

---

# Banner Ad

* **[Specify Ad Size](#specify_adsize)**
* **[Define AdView in layout xml](#define_adview_xml)**
* **[Implement by Java](#implement_java)**
* **[Implement by Kotlin](#implement_kotlin)**

---

<div id="specify_adsize"></div>

#### Specify ad size

You need to specify `AdSize` to adjust the size of the `AdView`.<br>
AdSize is enum class.

**com.rakuten.android.ads.runa.AdSize**

|Size Type|Desciption|
|:---|:---|
|DEFAULT|The ad size set in DashBoard.|
|ASPECT_FIT|Fit in display width.|
|CUSTOM|Can be specified to any size.<br>However, this specify is calculated based on the width.<br>Specifiable range: (DEFAULT < `CUSTOM` < ASPECT_FIT)|

Set this AdSize to setAdViewSize of AdView.

```java
AdView adView = new AdView(context);
adView.setAdSpotId(123);
adView.setAdViewSize(AdSize.ASPECT_FIT);
```

<div id="define_adview_xml"></div>

#### Define AdView in layout xml

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


---
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/ja/bannerads/README.md)

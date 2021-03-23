[TOP](../#top)　>　[API](./README.md)　>　AdLoader

---

# AdLoader

[![support version](http://img.shields.io/badge/runa-1.3.0+-blueviolet.svg?style=flat)](https://developer.android.com)

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdLoader

The object for load multiple ads at once. Generates AdLoader with `Builder` and loads ads.


### Public Method Summary

|Return|Method|Details|
:---:|:---|:---
void | execute() | Execute loading of ads.
List&lt;AdView&gt; | getAdViews() | Returns list of AdView that added to the Builder.
List&lt;AdView&gt; | getValidAdViews() | (Nullable) Returns list of AdView that load ads succeed. Returns null if load ads is not finished.
boolean | isLoading() | Returns a Boolean value about whether the ad is loading.

<div id="adLoader_builder"></div>

# Builder

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdLoader$Builder

The Builder class for generate an AdLoader. It also uses the builder pattern to set each parameters to load ads as needed.

### Public Constructors Summary

|constructors|
|:---|
|Builder(Context context)|

### Public Method Summary

|Return|Method|Details|
:---:|:---|:---
Builder | add([AdView](./AdView.md)... adViews) | Adds AdViews to be target of loading.
Builder | with([AdLoaderStateListener](./AdLoaderStateListener.md) listener) | Adds an AdLoaderStateListener if get a callback of AdLoader's loading status.
Builder | putProperty(String key, String value) | Adds key/value pair of property as needed.
Builder | putProperty(String key, int value) | Adds key/value pair of property as needed.
Builder | putProperty(String key, double value) | Adds key/value pair of property as needed.
Builder | putProperty(String key, long value) | Adds key/value pair of property as needed.
Builder | putProperty(String key, Bundle value) | Adds key/value pair of property as needed.
Builder | putProperty(String key, JSONObject value) | Adds key/value pair of property as needed.
AdLoader | build() | Generates AdLoader instance.


### Implementation Sample

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
                override fun onLoadAllComplete() {
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

* [API](./README.md)

* [TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/api/AdLoader.md)

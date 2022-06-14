[TOP](/README.md#top)　>　[API](./README.md)　>　Runa

---

# Runa

[![support version](http://img.shields.io/badge/runa-1.4.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.4.0)

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.Runa

public object class **Runa** extends [Object](https://developer.android.com/reference/java/lang/Object.html)<br>

An object to launch Runa SDK.


### Public Method Summary

|Return|Method|Details|
|:---:|:---|:---|
|void|init([Application](https://developer.android.com/reference/android/app/Application))|A method to launch Runa SDK.|
|void|setDebug(boolean)|Enable debug mode|
|Boolean|getDebug|Whether debug mode is enabled.|


### Sample Code

In the onCreate method of the class that inherits [`Application`](https://developer.android.com/reference/android/app/Application), implement as follows and launch the SDK.

```kotlin
class SampleApplication : Application() {
    override fun onCreate() {

        // Launch SDK
        Runa.init(this).also {
            // For output debug log according to status
            it.debug = BuildConfig.DEBUG
        }

    }
...
```


---
* [API](./README.md)

* [TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/ja/api/Runa.md)

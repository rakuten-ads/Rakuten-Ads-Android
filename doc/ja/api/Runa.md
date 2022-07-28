[TOP](../#top)　>　[API](./README.md)　>　Runa

---

# Runa

[![support version](http://img.shields.io/badge/runa-1.4.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.4.0)

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.Runa

public object class **Runa** extends [Object](https://developer.android.com/reference/java/lang/Object.html)<br>

Runa SDKを起動するためのオブジェクト


### Public Method Summary

|Return|Method|Details|
|:---:|:---|:---|
|void|init([Application](https://developer.android.com/reference/android/app/Application))|起動を実行するためのメソッド。|
|void|setDebug(Boolean)|デバッグモードの有効/無効にするためのメソッド|
|Boolean|getDebug|デバックモードの状況を取得するメソッド|


### サンプル

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

* [TOP](../#top)

---
LANGUAGE :
> [![en](/doc/img/lang/en.png)](/doc/api/Runa.md)

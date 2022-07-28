[TOP](/README.md#top)　>　Extension

---

# Extension Module for Banner Ads

The extension module gives several special configurations for certain purposes.<br>
Before using these configurations, appropriate values need to be confirmed first from the market admin sides.

---

## 1. Import the Extension Module

#### Example project-level build.gradle

Open the app-level `build.gradle` file for your app, and look for a "dependencies" section.

```gradle
  implementation 'com.rakuten.android.ads:runa:1.6.0'
  implementation 'com.rakuten.android.ads:runa-extension:1.6.0'
```

#### Corresponding versions

|runa-extension|runa|
|:---:|:---:|
|〜 v1.1.0|〜 v1.1.5|
|v1.2.0|v1.2.0, v1.2.1|
|v1.2.1|v1.2.2 〜 v1.2.7|
|v1.3.0|v1.3.0 〜 v1.3.5|
|v1.4.0|v1.4.0 〜 v1.4.1|
|v1.4.1|v1.4.2 〜 v1.5.0|
|v1.5.0|v1.5.0|
|v1.6.0|v1.6.0 〜 v1.6.1|

## 2. ContentGenre class

[![support version](http://img.shields.io/badge/extension-1.0.0+-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

ContentGenre(int masterId, String code, Type type)

> **masterID** : Rakuten Ichiba Genre ID. (e.g. 1)
>
> **code** : Ad Request's Genre ID. (e.g. "12345")
>
> **type** : (enum) Choice a type `Type.Children` or `Type.L1`

## 3. CustomTargeting class

[![support version](http://img.shields.io/badge/extension-1.0.0+-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

CustomTargeting is builder pattern. Use a Builder class.

```
CustomTargeting.Builder()
```

And add the key/values using the put() method. Then use build() method to get `CustomTergeting` object.

e.g.

```kotlin
val customTargeting = CustomTargeting.Builder().apply {
    put("K1", "V1", "V2", "V3")
}.build()
```

## 4. RzCookie

Sets the RzCookie

[![support version](http://img.shields.io/badge/extension-_1.1.5_〜_1.2.0-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

```kotlin
import com.rakuten.android.ads.runa.extension.setRz

...
    AdView().setRz("RZ_COOKIE")
```

[![support version](http://img.shields.io/badge/extension-1.2.1+-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

```kotlin
import com.rakuten.android.ads.runa.extension.setRzCookie
...

    AdView().setRzCookie("RZ_COOKIE")
```

## 5. RpCookie

[![support version](http://img.shields.io/badge/extension-_1.4.1-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.4.2)

```kotlin
import com.rakuten.android.ads.runa.extension.setRp

...
    AdView().setRp("RP_COOKIE")
```

## 6. Sample Implementation

**The case of ExtensionProperty using**

<details>
<summary>1.0.0+ (common)</summary>

[![support version](http://img.shields.io/badge/extension-1.0.0+-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

```kotlin
import com.rakuten.android.ads.runa.AdStateListener;
import com.rakuten.android.ads.runa.AdView;
import com.rakuten.android.ads.runa.extension.ContentGenre;
import com.rakuten.android.ads.runa.extension.CustomTargeting;
...

    // Create ContentGenre class
    val genre = ContentGenre(GENRE_MASTER_ID, GENRE_CODE, GENRE_TYPE)
    // Create CustomTargeting class
    val targeting = CustomTargeting.Builder().apply {
                          put(KEY, VALUE)
                          put(KEY2, VALUE2)
    }.buil()
    val adView = findViewById<AdView>(R.id.adview).apply {
        adSpotId = "AD_SPOT_ID"
        adViewSize = AdSize.ASPECT_FIT
        setContentGenre(genre)
        setCustomTargeting(targeting)
        setRzCookie("RZ_COOKIE")
        adStateListener = object : AdStateListener() {
            override fun onLoadSuccess() {
                visibility = View.VISIBLE
            }
            override fun onLoadFailure(view: View?, errorState: ErrorState) {
                visibility = View.GONE
            }
        }
    }
    adView.show()
```

</details>
<br>
<details>
<summary>1.2.0+</summary>

[![support version](http://img.shields.io/badge/extension-1.2.0-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

```kotlin
import com.rakuten.android.ads.runa.AdStateListener
import com.rakuten.android.ads.runa.AdView
import com.rakuten.android.ads.runa.extension.ContentGenre
import com.rakuten.android.ads.runa.extension.CustomTargeting
import com.rakuten.android.ads.runa.extension.ExtensionProperty
...

    // Create ContentGenre class
    val genre = ContentGenre(GENRE_MASTER_ID, GENRE_CODE, GENRE_TYPE)
    // Create CustomTargeting class
    val customTargeting = CustomTargeting.Builder().apply {
                          put(KEY, VALUE)
                          put(KEY2, VALUE2)
    }.buil()

    val extensionProperty = ExtensionProperty.Builder()
                              .withContentGenre(genre)
                              .withCustomTargeting(customTargeting)
                              .withRz("RZ_COOKIE")
                              .withLocation(location)
                              .build()

    findViewById<AdView>(R.id.adview).apply {
        adSpotId = "AD_SPOT_ID"
        adViewSize = AdSize.ASPECT_FIT
        adStateListener = object : AdStateListener() {
            override fun onLoadSuccess() {
                visibility = View.VISIBLE
            }
            override fun onLoadFailure(view: View?, errorState: ErrorState) {
                visibility = View.GONE
            }
        }
        extensionProperty.apply(this)
    }.show()
```

> `ExtensionProperty` is added from extension module v1.2.0 .

</details>
<br>
<details>
<summary>1.2.1+</summary>

[![support version](http://img.shields.io/badge/extension-1.2.1+-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

```kotlin
import com.rakuten.android.ads.runa.AdStateListener
import com.rakuten.android.ads.runa.AdView
import com.rakuten.android.ads.runa.extension.ContentGenre
import com.rakuten.android.ads.runa.extension.CustomTargeting
import com.rakuten.android.ads.runa.extension.AdViewHelper
...

    // Create ContentGenre class
    val genre = ContentGenre(GENRE_MASTER_ID, GENRE_CODE, GENRE_TYPE)
    // Create CustomTargeting class
    val customTargeting = CustomTargeting.Builder().apply {
                          put(KEY, VALUE)
                          put(KEY2, VALUE2)
    }.buil()

    val adViewHelper = AdViewHelper.Builder()
                              .with(genre)
                              .with(customTargeting)
                              .with(location)
                              .withRzCookie("RZ_COOKIE")
                              .build()

    findViewById<AdView>(R.id.adview).apply {
        adSpotId = "AD_SPOT_ID"
        adViewSize = AdSize.ASPECT_FIT
        adStateListener = object : AdStateListener() {
            override fun onLoadSuccess() {
                visibility = View.VISIBLE
            }
            override fun onLoadFailure(view: View?, errorState: ErrorState) {
                visibility = View.GONE
            }
        }
        adViewHelper.apply(this)
    }.show()
```

> `AdViewHelper` is added from extension module v1.2.1, but `ExtensionProperty` has been deprecated in this version.

</details>
</details>
<br>
<details>
<summary>1.4.1+</summary>

[![support version](http://img.shields.io/badge/extension-1.4.1+-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

```kotlin
import com.rakuten.android.ads.runa.AdStateListener
import com.rakuten.android.ads.runa.AdView
import com.rakuten.android.ads.runa.extension.ContentGenre
import com.rakuten.android.ads.runa.extension.CustomTargeting
import com.rakuten.android.ads.runa.extension.AdViewHelper
...

    // Create ContentGenre class
    val genre = ContentGenre(GENRE_MASTER_ID, GENRE_CODE, GENRE_TYPE)
    // Create CustomTargeting class
    val customTargeting = CustomTargeting.Builder().apply {
                          put(KEY, VALUE)
                          put(KEY2, VALUE2)
    }.buil()

    val adViewHelper = AdViewHelper.Builder()
                              .with(genre)
                              .with(customTargeting)
                              .withRzCookie("RZ_COOKIE")
                              .withRpCookie("RP_COOKIE")
                              .build()

    findViewById<AdView>(R.id.adview).apply {
        adSpotId = "AD_SPOT_ID"
        adViewSize = AdSize.ASPECT_FIT
        adStateListener = object : AdStateListener() {
            override fun onLoadSuccess() {
                visibility = View.VISIBLE
            }
            override fun onLoadFailure(view: View?, errorState: ErrorState) {
                visibility = View.GONE
            }
        }
        adViewHelper.apply(this)
    }.show()
```

</details>

<br><br><br><br><br>

---
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/img/lang/ja.png)](/doc/ja/extension/README.md)

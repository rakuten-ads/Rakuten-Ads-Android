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
  implementation 'com.rakuten.android.ads:runa:1.6.4'
  implementation 'com.rakuten.android.ads:runa-extension:1.6.1'
```

#### Corresponding versions

| runa-extension |      runa       |
|:--------------:|:---------------:|
|    〜 v1.1.0    |    〜 v1.1.5     |
|     v1.2.0     | v1.2.0, v1.2.1  |
|     v1.2.1     | v1.2.2 〜 v1.2.7 |
|     v1.3.0     | v1.3.0 〜 v1.3.5 |
|     v1.4.0     | v1.4.0 〜 v1.4.1 |
|     v1.4.1     | v1.4.2 〜 v1.5.0 |
|     v1.5.0     |     v1.5.0      |
|     v1.6.0     | v1.6.0 〜 v1.6.2 |
|     v1.6.1     | v1.6.3 〜 v1.6.4 |

<div id="helper_adview"></div>

## 2. Set special parameters to AdView

Using `runa-extension` module allows you to set the following special parameters to AdView.

### 2.1 ContentGenre class

[![support version](http://img.shields.io/badge/extension-1.0.0+-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

ContentGenre(int masterId, String code, Type type)

> **masterID** : Rakuten Ichiba Genre ID. (e.g. 1)
>
> **code** : Ad Request's Genre ID. (e.g. "12345")
>
> **type** : (enum) Choice a type `Type.Children` or `Type.L1`

### 2.2 CustomTargeting class

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

#### Use Normalizer

Normalizer module provides api to normalize any string values for convenience, contains following rules:

* convert half-width to full-width (カナ, 濁点, 半濁点, 長音符)
* convert full-width to half-width (digit, alphabet, space, double quotation)
* convert upper-case to lower-case (alphabet)
* convert multi (>=2) spaces to single space trim spaces
* remove spaces at start and end of phrase

> e.g. `"　Orange APPLE　梨　　ｻｶﾅ"` -> `"orange apple 梨 サカナ"`

Import `normalizer` module to project gradle file.
```gradle
implementation 'com.rakuten.android.ads:normalizer:1.0.0'
```

```kotlin
import com.rakuten.android.ads.normalizer.QueryNormalizer
...

val customTargeting = CustomTargeting.Builder().apply {
    put("K1", QueryNormalizer.normalize("Orange APPLE　梨　　ｻｶﾅ"))
}.build()
```

### 2.3 RzCookie

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

### 2.4 RpCookie

[![support version](http://img.shields.io/badge/extension-_1.4.1+-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.4.2)

```kotlin
import com.rakuten.android.ads.runa.extension.setRp

...
    AdView().setRp("RP_COOKIE")
```

<div id="helper_adloader"></div>

## 3. Set special parameters to AdLoader

Set special parameters to AdLoader with AdLoaderHelper.<br>
Using `runa-extension` module allows you to set the following special parameters to [`AdLoader`](../api/AdLoader.md).

```kotlin
import com.rakuten.android.ads.runa.extension.AdLoaderHelper

...
val adView1Builder = AdLoaderHelper.AdViewBuilder(findViewById<AdView>(R.id.adView1)).apply {
    setAdSpotId("{AD_SPOT_ID1}")
    val customTargeting = CustomTargeting.Builder().apply {
      put("K1", "V1", "V2", "V3")
    }.build()
    setCustomTargeting(customTargeting)
    setContentGenre(ContentGenre("{MasterID}", "{CODE}", "{TYPE}"))
}

val adView2 = findViewById<AdView>(R.id.adView2).apply {
  adSpotId = "{AD_SPOT_ID2}"
  adStateListener = object : AdLoaderStateListener() {
    ...
  }
}
...

val adLoaderHelper = AdLoaderHelper(context)
  // Add AdView with basic settings
  .add(
      adView1Builder,
      AdLoaderHelper.AdViewBuilder(adView2),
      AdLoaderHelper.AdViewBuilder(adView3),
      AdLoaderHelper.AdViewBuilder(adView4)
  )
  // Set AdLoaderStateListener
  .with(setAdStateListener(object : AdLoaderStateListener() {
    ...
  }))
  // Set RZ Cookie
  .withRzCookie("{RZ_COOKIE}")
  // Set RP Cookie
  .withRpCookie("{RP_COOKIE}")
  .build()
  // Execute loading
  .execute()
```

<div id="implemention_sample"></div>

## 4. Sample Implementation

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

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
  implementation 'com.rakuten.android.ads:runa:1.2.0'
  implementation 'com.rakuten.android.ads:runa-extension:1.2.0'
```

#### Corresponding versions

|runa-extension|runa|
|:---:|:---:|
|〜 v1.1.0|〜v1.1.5|
|v1.2.0〜|v1.2.0〜|


## 2. ContentGenre class

ContentGenre(int masterId, String code, Type type)

> **masterID** : Rakuten Ichiba Genre ID. (e.g. 1)
>
> **code** : Ad Request's Genre ID. (e.g. "12345")
>
> **type** : (enum) Choice a type `Type.Children` or `Type.L1`

## 3. CustomTargeting class

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

```kotlin
    AdView().setRz("RZ_COOKIE")
```

## 5. Sample Implementation

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

<br><br><br><br><br>

---
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/ja/extension/README.md)

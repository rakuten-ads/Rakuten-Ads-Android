[TOP](/README.md#top)　>　App to App

---

# App to App

## Objective

How to activate the A2A module is explained in this document.<br>
The activation of this module enables you to have new sources of revenue through new ad formats.<br>
Just in case you have a question related to the business background, please feel free to contact with our sales person in charge.

## Import the AppToApp SDK

Needs add below an implementation to the 'dependencies' of `build.gradle` file.<br>
In addition to the runa module, add the runa-a2a module.

```gradle
  implementation 'com.rakuten.android.ads:runa:1.2.0'
  implementation 'com.rakuten.android.ads:runa-a2a:1.0.0'
```

#### Corresponding versions

|runa-extension|runa|
|:---:|:---:|
|〜 v0.2.0|〜v1.1.5|
|v1.0.0〜|v1.2.0〜|

## Implementation

### The targeting by keyword

Sets keywords by `setKeywords()` method.

```kotlin
    AdView(context).apply {
        setKeywords(Keywords("PC", "MAC"))
    }.show()
```

The other implementation method is the same as the banner. Please [see it](../bannerads/README.md).

<br><br><br><br><br>

---
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/ja/a2a/README.md)

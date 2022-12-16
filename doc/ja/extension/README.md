[TOP](../#top)　>　Extension

---

# バナー広告拡張モジュール

拡張モジュールは特定のクライアントに向けて特別なオプションを提供しています。<br>
本モジュールを組み込む前に、楽天市場管理者から適切な設定値を確認する必要があります。

---

## 1. 拡張モジュールのインポート

以下を`build.gradle`のdependenciesに追加してください。<br>
runaモジュールに加え、runa-aextensionモジュールを追加します。

```gradle
  implementation 'com.rakuten.android.ads:runa:1.6.3'
  implementation 'com.rakuten.android.ads:runa-extension:1.6.1'
```

### モジュール間の対応バージョン

|runa-extension|runa|
|:---:|:---:|
|〜 v1.1.0|〜 v1.1.5|
|v1.2.0〜|v1.2.0, v1.2.1|
|v1.2.1|v1.2.2 〜 v1.2.7|
|v1.3.0|v1.3.0 〜 v1.3.5|
|v1.4.0|v1.4.0 〜 v1.4.1|
|v1.4.1|v1.4.2 〜 v1.5.0|
|v1.5.0|v1.5.0|
|v1.6.0|v1.6.0 〜 v1.6.2|
|     v1.6.1     |     v1.6.3      |

<div id="helper_adview"></div>

## 2. 特殊なパラメータをAdViewにセットする

### 2.1 ContentGenreクラス

[![support version](http://img.shields.io/badge/extension-1.0.0+-informational.svg?style=flat)](https://developer.android.com)

ContentGenre(int masterId, String code, Type type)

> **masterID** : 楽天市場のジャンル ID. (e.g. 1)
>
> **code** : 広告リクエストのジャンル ID. (e.g. "12345")
>
> **type** : (enum) タイプを選択 `Type.Children` または `Type.L1`

### 2.2 CustomTargetingクラス

[![support version](http://img.shields.io/badge/extension-1.0.0+-informational.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases)

CustomTargetingはBuilderパターンのクラスであるため、Builder()を使用しターゲティング設定を行います。

```
val targeting = CustomTargeting.Builder().apply {
    put("K1", "V1", "V2", "V3")
}.build()
```

> * ターゲティングはput()メソッドを用いてKey/Valueを指定します。
> * 必要な値を指定したあとは、build()メソッドでCustomTargetingクラスを生成します。

#### Normalizerを利用する

Normalizerモジュールは文字列を以下のルールの基、標準化します。

* 半角文字列を全角文字列に変換 (カナ, 濁点, 半濁点, 長音符)
* 全角英数字記号スペースを半角に変換 (digit, alphabet, space, double quotation)
* アルファベットの大文字を小文字に変換
* スペース(全角含む)を半角スペースに変換
* 文字列の始まりまたは終わりのスペースを消去

> e.g. `"　Orange APPLE　梨　　ｻｶﾅ"` -> `"orange apple 梨 サカナ"`

gradleファイルに以下を追加しインポートします。
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

RzCookieを設定します。

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

## 3. 特殊なパラメータをAdLoaderにセットする

特殊なパラメータをAdLoaderにセットするにはAdLoaderHelperを利用します。<br>
`runa-extension`モジュールを利用することで、AdLoaderに特殊なパラメータをセットすることができます。

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

**拡張プロパティの実装例**

<details>
<summary>v1.0.0+ (共通)</summary>

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
<summary>v1.2.0+</summary>

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

> `ExtensionProperty`はExtensionモジュール v1.2.0 から追加されました。

</details>
<br>
<details>
<summary>v1.2.1+</summary>

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

> `AdViewHelper`はExtensionモジュール v1.2.1 から追加され、`ExtensionProperty`は当バージョンから非推奨となりました。

</details>
<br>
<details>
<summary>v1.4.1+</summary>

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
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/img/lang/en.png)](/doc/extension/README.md)

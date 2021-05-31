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
  implementation 'com.rakuten.android.ads:runa:1.3.2'
  implementation 'com.rakuten.android.ads:runa-extension:1.3.0'
```

### モジュール間の対応バージョン

|runa-extension|runa|
|:---:|:---:|
|〜 v1.1.0|〜 v1.1.5|
|v1.2.0〜|v1.2.0, v1.2.1|
|v1.2.1|v1.2.2 〜 v1.2.7|
|v1.3.0|v1.3.0 〜 v1.3.2|

## 2. ContentGenreクラス

[![support version](http://img.shields.io/badge/extension-1.0.0+-informational.svg?style=flat)](https://developer.android.com)

ContentGenre(int masterId, String code, Type type)

> **masterID** : 楽天市場のジャンル ID. (e.g. 1)
>
> **code** : 広告リクエストのジャンル ID. (e.g. "12345")
>
> **type** : (enum) タイプを選択 `Type.Children` または `Type.L1`

## 3. CustomTargetingクラス

[![support version](http://img.shields.io/badge/extension-1.0.0+-informational.svg?style=flat)](https://developer.android.com)

CustomTargetingはBuilderパターンのクラスであるため、Builder()を使用しターゲティング設定を行います。

```
val targeting = CustomTargeting.Builder().apply {
    put("K1", "V1", "V2", "V3")
}.build()
```

> * ターゲティングはput()メソッドを用いてKey/Valueを指定します。
> * 必要な値を指定したあとは、build()メソッドでCustomTargetingクラスを生成します。

## 4. RzCookie

RzCookeiを設定します。

[![support version](http://img.shields.io/badge/extension-_1.1.5_〜_1.2.0-informational.svg?style=flat)](https://developer.android.com)

```kotlin
    AdView().setRz("RZ_COOKIE")
```

[![support version](http://img.shields.io/badge/extension-1.2.1+-informational.svg?style=flat)](https://developer.android.com)

```kotlin
    AdView().setRzCookie("RZ_COOKIE")
```

## 5. Sample Implementation

### 5.1 拡張プロパティの実装例 (共通)

[![support version](http://img.shields.io/badge/extension-1.0.0+-informational.svg?style=flat)](https://developer.android.com)

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

### 5.2 拡張プロパティの実装例

[![support version](http://img.shields.io/badge/extension-1.2.0-informational.svg?style=flat)](https://developer.android.com)

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

### 5.3 T拡張プロパティの実装例

[![support version](http://img.shields.io/badge/extension-1.2.1+-informational.svg?style=flat)](https://developer.android.com)

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

> `AdViewHelper`はExtensionモジュール v1.2.1 から追加され、`ExtensionProperty`は当バージョンから非推奨となりました。

<br><br><br><br><br>

---
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/extension/README.md)

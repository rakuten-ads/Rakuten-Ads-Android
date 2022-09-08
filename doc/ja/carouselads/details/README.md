[TOP](../../)　>　[カルーセル広告](../) > パラメータ別実装詳細

---

# カルーセル広告 パラメータ別実装詳細

* **[1. ページングが無効(AdSize: DEFAULT)](#1_0)**
  * **[1.1 基本実装](#1_1)**
  * **[1.2 offsetStartWidthの指定](#1_2)**
  * **[1.3 offsetEndWidthの指定](#1_3)**
  * **[1.4 広告間にスペースを設定する](#1_4)**
* **[2. ページングが無効(AdSize: ASPECT_FIT)](#2_0)**
  * **[2.1 基本実装](#2_1)**
  * **[2.2 offsetStartWidthの指定](#2_2)**
  * **[2.3 offsetEndWidthの指定](#2_3)**
  * **[2.4 広告間にスペースを設定する](#2_4)**
* **[3. ページングが有効(AdSize: DEFAULT)](#3_0)**
  * **[3.1 基本実装](#3_1)**
* **[4. ページングが有効(AdSize: ASPECT_FIT)](#4_0)**
  * **[4.1 基本実装](#4_1)**
  * **[4.2 offsetを指定する](#4_2)**
  * **[4.3 隣接する広告を表示し間隔幅を設定する](#4_3)**
* **[5. インジケーターを表示する](#5_0)**
  * **[5.1 インジケータを表示する(AdSize: DEFAULT)](#5_1)**
  * **[5.2 インジケータを表示する(AdSize: ASPECT_FIT)](#5_2)**

---

<div id="1_0"></div>

## 1. ページングが無効(AdSize: DEFAULT)

`nestedAdsSize`が`DEFAULT`の設定を以下に記します。

<div id="1_1"></div>

### ■ 1.1 基本実装

AdSpotIDのみを指定すると以下のカルーセル広告が表示されます。<br>

<img src="/doc/img/carouselads/nonPageNation/default/001.png" /><br>

> ※ 一つの広告がカルーセル枠よりも大きいサイズの広告が入稿されている場合、比率を保持しカルーセル枠の幅に自動調整したサイズで表示されます。

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:adSpotIds="@array/adSpotIds"
    />
...
```

> `adSpotIds`はXMLで指定せず、コード上で指定することも可能です。<br>
> 本実装例ではXMLとコードの両方で記しています。実際にはどちらか一方で指定してください。

<details>
<summary>res/values/arrays.xml</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="adSpotIds">
        <item>{AD_SPOT_ID1}</item>
        <item>{AD_SPOT_ID2}</item>
        <item>{AD_SPOT_ID3}</item>
    </string-array>
</resources>
```

</details><br>

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds)
  .addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  .show()
```

> 広告の読み込みを実行するには`show()`を実行します。（XMLで必要なプロパティを指定しても表示にはshow()の実行は必要となります。）

<br><div id="1_2"></div>

### ■ 1.2 offsetStartWidthの指定

`offsetStartWidth`を指定すると1つめの広告の左端とカルーセル枠との間にスペースを設けることができます。

<img src="/doc/img/carouselads/nonPageNation/default/002.png"/><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:offsetStart="10dp"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  offsetStartWidth = 35
}.show()
```

<br><div id="1_3"></div>

### ■ 1.3 offsetEndWidthの指定

`offsetEndWidth`を指定すると最後の広告の右端とカルーセル枠との間にスペースを設けることができます。

<img src="/doc/img/carouselads/nonPageNation/default/003.png"/><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:offsetEnd="10dp"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  offsetEndWidth = 35
}.show()
```

<br><div id="1_4"></div>

### ■ 1.4 広告間にスペースを設定する

`adsSeparatorWidth`を指定すると広告間にスペースを設けることができます。

<img src="/doc/img/carouselads/nonPageNation/default/004.png"/><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:adsSeparatorWidth="10dp"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  adsSeparatorWidth = 35
}.show()
```

<div id="2_0"></div>

## 2. ページングが無効(AdSize: ASPECT_FIT)

`nestedAdsSize`が`ASPECT_FIT`の設定を以下に記します。

<br><div id="2_1"></div>

### ■ 2.1 基本実装

AdSpotIDのみを指定すると以下のカルーセル広告が表示されます。<br>
各広告枠はカルーセル枠の横幅サイズにフィットするよう比率を維持し自動調整され表示します。

<img src="/doc/img/carouselads/nonPageNation/aspectfit/001.png" /><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:nestedAdsSize="AspectFit"
    app:adSpotIds="@array/adSpotIds"
    />
...
```

<details>
<summary>res/values/arrays.xml</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="adSpotIds">
        <item>{AD_SPOT_ID1}</item>
        <item>{AD_SPOT_ID2}</item>
        <item>{AD_SPOT_ID3}</item>
    </string-array>
</resources>
```

</details><br>

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  nestedAdsSize = AdSize.ASPECT_FIT
}.show()
```

<br><div id="2_2"></div>

### ■ 2.2 offsetStartWidthの指定

`offsetStartWidth`を指定すると1つめの広告の左端とカルーセル枠との間にスペースを設けることができます。<br>
(n個の広告を表示する場合、2番目〜n-1番目の広告にoffsetの幅は表示されません。)

<img src="/doc/img/carouselads/nonPageNation/aspectfit/002.png" /><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:nestedAdsSize="AspectFit"
    app:offsetStart="10dp"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  nestedAdsSize = AdSize.ASPECT_FIT
  offsetStartWidth = 35
}.show()
```

<br><div id="2_3"></div>

### ■ 2.3 offsetEndWidthの指定

`offsetEndWidth`を指定すると最後の広告の右端とカルーセル枠との間にスペースを設けることができます。<br>
(n個の広告を表示する場合、2番目〜n-1番目の広告にoffsetの幅は表示されません。)

<img src="/doc/img/carouselads/nonPageNation/aspectfit/003.png" /><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:nestedAdsSize="AspectFit"
    app:offsetEnd="10dp"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  nestedAdsSize = AdSize.ASPECT_FIT
  offsetEndWidth = 35
}.show()
```

<br><div id="2_4"></div>

### ■ 2.4 広告間にスペースを設定する

`adsSeparatorWidth`を指定すると広告間にスペースを設けることができます。

<img src="/doc/img/carouselads/nonPageNation/aspectfit/004.png"/><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:nestedAdsSize="AspectFit"
    app:adsSeparatorWidth="10dp"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  nestedAdsSize = AdSize.ASPECT_FIT
  adsSeparatorWidth = 35
}.show()
```

<div id="3_0"></div>

## 3. ページングが有効(AdSize: DEFAULT)

ページングを有効にするには`isPagerSnapEnabled`をtrueにします。(デフォルト:false)

<br><div id="3_1"></div>

### 3.1 基本実装

ページングを有効にしてAdSizeがDEFAULTの場合、常に表示する広告は１つとなりカルーセル枠の中心に配置されます。<br>
また、カルーセル枠内を左右にスワイプする度に吸着するようにスクロールします。

<img src="/doc/img/carouselads/pageNation/default/001.png"/><br>

> ※ カルーセル枠よりも大きいサイズの広告が入稿されている場合、比率を保持しカルーセル枠の幅に自動調整したサイズで表示されます。

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:adSpotIds="@array/adSpotIds"
    app:pagerSnapEnabled="true"
    />
...
```

<details>
<summary>res/values/arrays.xml</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="adSpotIds">
        <item>{AD_SPOT_ID1}</item>
        <item>{AD_SPOT_ID2}</item>
        <item>{AD_SPOT_ID3}</item>
    </string-array>
</resources>
```

</details><br>

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  isPagerSnapEnabled = true
}.show()
```

<div id="4_0"></div>

## 4. ページングが有効(AdSize: ASPECT_FIT)

<br><div id="4_1"></div>

### 4.1 基本実装

ページングを有効にしてAdSizeがASPECT_FITの場合、常に表示する広告は１つとなりカルーセル枠の横幅のサイズに自動調整し表示されます。<br>
また、カルーセル枠内を左右にスワイプする度に吸着するようにスクロールします。

<img src="/doc/img/carouselads/pageNation/aspectfit/001.png"/><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:adSpotIds="@array/adSpotIds"
    app:nestedAdsSize="AspectFit"
    app:pagerSnapEnabled="true"
    />
...
```

<details>
<summary>res/values/arrays.xml</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="adSpotIds">
        <item>{AD_SPOT_ID1}</item>
        <item>{AD_SPOT_ID2}</item>
        <item>{AD_SPOT_ID3}</item>
    </string-array>
</resources>
```

</details><br>

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  nestedAdsSize = AdSize.ASPECT_FIT
  isPagerSnapEnabled = true
}.show()
```

<br><div id="4_2"></div>

### 4.2 offsetを指定する

offsetを指定すると表示する各広告の左右(指定した側)にスペースを設定します。

<img src="/doc/img/carouselads/pageNation/aspectfit/002.png"/><br>

> ※ ページングが有効な状態で、offsetの指定と`adsSeparatorWidth`や`overhangWidth`と併用指定することはできません。

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:nestedAdsSize="AspectFit"
    app:pagerSnapEnabled="true"
    app:offsetStart="10dp"
    app:offsetEnd="10dp"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  nestedAdsSize = AdSize.ASPECT_FIT
  isPagerSnapEnabled = true
  offsetStartWidth = 35
  offsetEndWidth = 35
}.show()
```

<br><div id="4_3"></div>

### 4.3 隣接する広告を表示し間隔幅を設定する

overhangWidthとadsSeparatorWidthを指定し、下図のようなカルーセル広告を表示します。

<img src="/doc/img/carouselads/pageNation/aspectfit/003.png"/><br>

> ※ offset幅の指定と併用することはできません。
>
> ※ 入稿している広告のサイズによっては適切に隣接する広告がはみ出ない場合があります。

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:nestedAdsSize="AspectFit"
    app:pagerSnapEnabled="true"
    app:adsOverhangWidth="20dp"
    app:adsSeparatorWidth="8dp"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  nestedAdsSize = AdSize.ASPECT_FIT
  isPagerSnapEnabled = true
  overhangWidth = 56
  adsSeparatorWidth = 12
}.show()
```

<div id="5_0"></div>

## 5. インジケーターを表示する

<br><div id="5_1"></div>

### 5.1 インジケータを表示する(AdSize: DEFAULT)

[ページングをDEFAULTサイズで表示](#3_1)したカルーセル広告にインジケーターを表示したものとなります。インジケーターはカルーセル枠内に広告が2以上表示された場合に有効となります。

<img src="/doc/img/carouselads/pageNation/indicator/default/001.png"/><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:pagerSnapEnabled="true"
    app:indicatorEnabled="true"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  isPagerSnapEnabled = true
  isIndicatorEnabled = true
}.show()
```

<br><div id="5_2"></div>

### 5.2 インジケータを表示する(AdSize: ASPECT_FIT)

[ページングをASPECT_FITサイズで表示](#4_1)したカルーセル広告にインジケーターを表示したものとなります。インジケーターはカルーセル枠内に広告が2以上表示された場合に有効となります。

<img src="/doc/img/carouselads/pageNation/indicator/aspectfit/001.png"/><br>

**&lt;XMLで指定する場合&gt;**

```xml
...
<com.rakuten.android.ads.runa.CarouselAdView
    android:id="@+id/carouselAds"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:nestedAdsSize="AspectFit"
    app:pagerSnapEnabled="true"
    app:indicatorEnabled="true"
    />
...
```

**&lt;コードで指定する場合&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  nestedAdsSize = AdSize.ASPECT_FIT
  isPagerSnapEnabled = true
  isIndicatorEnabled = true
}.show()
```

---
[戻る](../README.md#any_implementations)

[TOP](../../)

---
LANGUAGE :
> [![en](/doc/img/lang/en.png)](/doc/carouselads/details/README.md)

[TOP](../../)　>　[CarouselAds](../) > Implementation details by parameter

---

# CarouselAds Implementation details by parameter

* **[1. NestedAdSize: DEFAULT](#1_0)**
  * **[1.1 Basic implementation](#1_1)**
  * **[1.2 Specify offsetStartWidth](#1_2)**
  * **[1.3 Specify offsetEndWidth](#1_3)**
  * **[1.4 Sets space between ads](#1_4)**
* **[2. NestedAdSize: ASPECT_FIT](#2_0)**
  * **[2.1 Basic implementation](#2_1)**
  * **[2.2 Specify offsetStartWidth](#2_2)**
  * **[2.3 Specify offsetEndWidth](#2_3)**
  * **[2.4 Sets space between ads](#2_4)**
* **[3. Enable pageNation(AdSize: DEFAULT)](#3_0)**
  * **[3.1 Basic implementation](#3_1)**
* **[4. Enable pageNation(AdSize: ASPECT_FIT)](#4_0)**
  * **[4.1 Basic implementation](#4_1)**
  * **[4.2 Specify offset](#4_2)**
  * **[4.3 Display Adjacent Ads and Set Separator Width](#4_3)**
* **[5. Enable indicator](#5_0)**
  * **[5.1 Enable indicator(AdSize: DEFAULT)](#5_1)**
  * **[5.2 Enable indicator(AdSize: ASPECT_FIT)](#5_2)**

---

<div id="1_0"></div>

## 1. NestdAdSize: DEFAULT

Below are the settings in case of `nestedAdsSize` is `DEFAULT`.

<div id="1_1"></div>

### ■ 1.1 Basic implementation

If you specify only AdSpotID, the following carousel ads will be displayed.<br>

<img src="/doc/img/carouselads/nonPageNation/default/001.png" /><br>

> ※ If an ad that is larger than the carousel frame is set on *DashBoard*, it will be displayed in the size that is automatically adjusted to the width of the carousel frame while maintaining the ratio.

**&lt;Defined in XML&gt;**

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

> - It is also possible to specify `adSpotIds` in code without specifying them in XML.
> - This implementation example is written in both XML and code. Please specify one or the other.

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds)
  .addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  .show()
```

> ※ Execute `show()` to load ads.(Even if you specify the required properties in XML, it is necessary to execute `show()` to display them.)

<br><div id="1_2"></div>

### ■ 1.2 Specify offsetStartWidth

By specifying `offsetStartWidth`, it is possible to set width of a space between the left edge of the first ad and the carousel frame.

<img src="/doc/img/carouselads/nonPageNation/default/002.png"/><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  offsetStartWidth = 35
}.show()
```

<br><div id="1_3"></div>

### ■ 1.3 Specify offsetEndWidth

By specifying `offsetEndWidth`, it is possible to set width of a space between the right edge of the first ad and the carousel frame.

<img src="/doc/img/carouselads/nonPageNation/default/003.png"/><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  offsetEndWidth = 35
}.show()
```

<br><div id="1_4"></div>

### ■ 1.4 Sets space between ads

Specify `adsSeparatorWidth` to allow space between ads.

<img src="/doc/img/carouselads/nonPageNation/default/004.png"/><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  adsSeparatorWidth = 35
}.show()
```

<div id="2_0"></div>

## 2. NestedAdSize: ASPECT_FIT

Below are the settings in case of `nestedAdsSize` is `ASPECT_FIT`.

<br><div id="2_1"></div>

### ■ 2.1 Basic implementation

If you specify only AdSpotID, the following carousel ads will be displayed.<br>
Each ad spots are automatically adjusted and displayed that it fit to the width size of the carousel frame and keep the ratio.

<img src="/doc/img/carouselads/nonPageNation/aspectfit/001.png" /><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  nestedAdsSize = AdSize.ASPECT_FIT
}.show()
```

<br><div id="2_2"></div>

### ■ 2.2 Specify offsetStartWidth

By specifying `offsetStartWidth`, it can set a space between the left edge of the first ad and the carousel frame.<br>
(When displaying 'n' ads, the width of offset is not displayed for the 2nd to 'n-1'th ads.)

<img src="/doc/img/carouselads/nonPageNation/aspectfit/002.png" /><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  nestedAdsSize = AdSize.ASPECT_FIT
  offsetStartWidth = 35
}.show()
```

<br><div id="2_3"></div>

### ■ 2.3 Specify offsetEndWidth

By specifying `offsetEndWidth`, it can set a space between the right edge of the last ad and the carousel frame.<br>
(When displaying 'n' ads, the width of offset is not displayed for the 2nd to 'n-1'th ads.)

<img src="/doc/img/carouselads/nonPageNation/aspectfit/003.png" /><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  nestedAdsSize = AdSize.ASPECT_FIT
  offsetEndWidth = 35
}.show()
```

<br><div id="2_4"></div>

### ■ 2.4 Sets spaces between ads

By specifying `adsSeparatorWidth`, it can set spaces between ads.

<img src="/doc/img/carouselads/nonPageNation/aspectfit/004.png"/><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{FIRST_ID}", "{SECOND_ID}", "{THIRD_ID}")
  nestedAdsSize = AdSize.ASPECT_FIT
  adsSeparatorWidth = 35
}.show()
```

<div id="3_0"></div>

## 3. Enable pageNation (AdSize: DEFAULT)

Set `isPagerSnapEnabled` to true to enable paging.(Default is false)

<br><div id="3_1"></div>

### 3.1 Basic implementation

In case of AdSize is default and during enable `pageNation`, ad is displayed always one in center of the carousel frame. And swipe left or right within the carousel frame to scroll like adsorption.

<img src="/doc/img/carouselads/pageNation/default/001.png"/><br>

> ※ When an ad that is larger than the carousel frame is set in DashBoard, it is automatically adjusted and displayed what fit to the width size of the carousel frame and keep the ratio.

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  isPagerSnapEnabled = true
}.show()
```

<div id="4_0"></div>

## 4. Enable pageNation (AdSize: ASPECT_FIT)

<br><div id="4_1"></div>

### 4.1 Basic implementation

In case of set `AdSize` is `ASPECT_FIT` and enable `pageNation`, the carousel frame display always one ad that it is automatically adjust the size of one's width. And swipe left or right within the carousel frame to scroll like adsorption.

<img src="/doc/img/carouselads/pageNation/aspectfit/001.png"/><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  nestedAdsSize = AdSize.ASPECT_FIT
  isPagerSnapEnabled = true
}.show()
```

<br><div id="4_2"></div>

### 4.2  Specify the offset

By specifying the offset that it set spaces to left (or/and right) of displayed each ads.

<img src="/doc/img/carouselads/pageNation/aspectfit/002.png"/><br>

> ※ When paging is enabled, offset cannot be specified together with `adsSeparatorWidth` or `overhangWidth`.

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

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

### 4.3 Display Adjacent Ads and Set Separator Width

Specify overhangWidth and adsSeparatorWidth to display carousel ads as shown below.

<img src="/doc/img/carouselads/pageNation/aspectfit/003.png"/><br>

> ※ Cannot be used together with offset width specification.
>
> ※ Adjacent ads may not overhang properly depending on the size of the ad you are set on the DashBoard.

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

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

## 5. Show indicator

<br><div id="5_1"></div>

### 5.1 Enable indicator(AdSize: DEFAULT)

This is a carousel ad that [displays paging](#3_1) in DEFAULT size and displays an indicator. The indicator is valid when 2 or more ads are displayed within the carousel frame.

<img src="/doc/img/carouselads/pageNation/indicator/default/001.png"/><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  isPagerSnapEnabled = true
  isIndicatorEnabled = true
}.show()
```

<br><div id="5_2"></div>

### 5.2 Enable indicator(AdSize: ASPECT_FIT)

This is a carousel ad that [displays paging](#4_1) in ASPECT_FIT size and displays an indicator. The indicator is valid when 2 or more ads are displayed within the carousel frame.

<img src="/doc/img/carouselads/pageNation/indicator/aspectfit/001.png"/><br>

**&lt;Defined in XML&gt;**

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

**&lt;Defined in code&gt;**

```java
findViewById<CarouselAdView>(R.id.carouselAds).apply {
  addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
  nestedAdsSize = AdSize.ASPECT_FIT
  isPagerSnapEnabled = true
  isIndicatorEnabled = true
}.show()
```

---
[CarouselAds](../README.md#any_implementations)

[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/img/lang/ja.png)](/doc/ja/carouselads/details/README.md)

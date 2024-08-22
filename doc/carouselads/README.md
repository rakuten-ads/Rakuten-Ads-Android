[TOP](/README.md#top)　>　CarouselAds

---

# CarouselAds

[![support version](http://img.shields.io/badge/runa-1.6.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.6.0)

* **[1. Overview](#implementation)**
* **[2. Basic implementation of Carousel Ads](#implementation)**
  * **[2.1 Basic implementation](#basis_of_implementation)**
  * **[2.2 Detect Carousel Ads State](#event_detection)**
* **[4. Implementation by each parameter](#any_implementations)**


---

## 1. Overview

Carousel ads are horizontal banner ads that allow app users to scroll horizontally.<br>
Ads can be displayed in the carousel ad frame as many as the specified ad space ID (AdSpotID).<br>
Based on the size specified in the ad space setting on the dashboard, it is drawn according to the resolution of the device.<br>
Runa recommends that you keep the size of the ads displayed in the carousel frame consistent.

<center><img src="/doc/img/carouselads/001.png" height="200" /></center>

#### Prerequisite

* Supported version : [v1.6.0+](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.6.0)

<div id="implementation"></div>

## 2. Basic implementation of Carousel Ads

<div id="basis_of_implementation"></div>

### 2.1 Basic implementation

Use the [`CarouselAdView`](/doc/ja/api/CarouselAdView.md) class to implement carousel ads.<br>
In the display of this advertisement, the included ad space is displayed left-aligned and cannot be displayed right-aligned.<br>
There are two ways to place it on the Activity or Fragment to be displayed, defining it in the layout XML file or defining it directly in the program.<br>

<details>
<summary><b>Definition by XML</b></summary>

<br>
res/layout/main_activity.xml

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

</details>
<br>

MainActivity.kt

```java
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.main_activity)

    findViewById<CarouselAdView>(R.id.carouselAds).show()
}
```

</details>

<br>

<details>
<summary><b>Programmatically Definition</b></summary>

<br>
MainActivity.kt

```java
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.main_activity)
    val yourView = findViewById<ViewGroup>(R.id.anyParentView)    

    val carouselAdView = CarouselAdView(this).apply {
        addAdSpotId("{AD_SPOT_ID1}", "{AD_SPOT_ID2}", "{AD_SPOT_ID3}")
    }
    yourView.addView(
        carouselAdView,
        ViewGroup.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.WRAP_CONTENT)
    )
}
```

</details>

<div id="event_detection"></div>

### 2.2 Detect Carousel Ads State

Use [`CarouselAdStateListener`](/doc/ja/api/CarouselAdStateListener.md) class to detect ad events and customize app behavior.<br>
By setting the defined CarouselAdStateListener in the CarouselAdView$`setCarouselAdStateListener()` method, you will be able to handle the event.

```java
val carouselAdView = CarouselAdView(this).apply {
    carouselAdStateListener = object: CarouselAdStateListener() {

        override fun onAllLoadsFinished() {}

        override fun onLoadSuccess(view: View? = null) {
            // Checking Example
            val adSpotId = (view as? AdView)?.adSpotId
        }

        override fun onLoadFailure(view: View? = null, errorState: ErrorState) {
            // Checking Example
            val adSpotId = (view as? AdView)?.adSpotId
        }

        override fun onClick(view: View? = null, errorState: ErrorState?) {
            // Checking Example
            val adSpotId = (view as? AdView)?.adSpotId
        }

        override fun onLeftApplication() {}

        override fun onAdClosed() {}

        override fun onWebViewCrashed(adView: AdView?) {}
    }
}
```

|method|details|
|:---|:---|
|onLoadSuccess(View)|Called every time loading is successful for each ad spot ID set in CarouselAdView|
|onLoadFailure(View, ErrorState)|Called each time an ad request fails for each ad spot ID set in CarouselAdView.|
|onClick(View, ErrorState)|Called when an ad is clicked.|
|onLeftApplication()|Called when an ad is clicked and leaves the application.|
|onAdCloseed()|Called Return to app after clicking ad and navigating to destination.|
|onAllLoadsFinished()|Called when all loading of the ad spot ID set in CarouselAdView is completed. In this case, it will be called when the read process is completed regardless of the success or failure of each read result.|
|onWebViewCrashed(AdView?)|Called when the process inside WebView in AdView is crashed.|

<div id="any_implementations"></div>

## 4. Implementation by each parameter

### 4.1 Disable pageNation(Default)

|Displayed image|Parameters|Details|
|:---:|:---|:---:|
|<img src="/doc/img/carouselads/nonPageNation/default/001.png" width=500/>|・nestedAdsSizeAdSize : DEFAULT<br>・adsSeparatorWidth : 0|[->](./details/README.md#1_1)|
|<img src="/doc/img/carouselads/nonPageNation/default/002.png" width=500/>|・nestedAdsSizeAdSize : DEFAULT<br>・offsetStartWidth : 35<br>|[->](./details/README.md#1_2)|
|<img src="/doc/img/carouselads/nonPageNation/default/003.png" width=500/>|・nestedAdsSizeAdSize : DEFAULT<br>・offsetEndWidth : 35<br>|[->](./details/README.md#1_3)|
|<img src="/doc/img/carouselads/nonPageNation/default/004.png" width=500/>|・nestedAdsSizeAdSize : DEFAULT<br>・adsSeparatorWidth : 35|[->](./details/README.md#1_4)|
|<img src="/doc/img/carouselads/nonPageNation/aspectfit/001.png" width=500/>|・nestedAdsSizeAdSize : ASPECT_FIT|[->](./details/README.md#2_1)|
|<img src="/doc/img/carouselads/nonPageNation/aspectfit/002.png" width=500/>|・nestedAdsSizeAdSize : ASPECT_FIT<br>・offsetStartWidth : 35<br>|[->](./details/README.md#2_2)|
|<img src="/doc/img/carouselads/nonPageNation/aspectfit/003.png" width=500/>|・nestedAdsSizeAdSize : ASPECT_FIT<br>・offsetEndWidth : 35<br>|[->](./details/README.md#2_3)|
|<img src="/doc/img/carouselads/nonPageNation/aspectfit/004.png" width=500/>|・nestedAdsSizeAdSize : ASPECT_FIT<br>・adsSeparatorWidth : 35<br>|[->](./details/README.md#2_4)|

### 4.2 Enable pageNation

|Displayed image|Parameters|Details|
|:---:|:---|:---:|
|<img src="/doc/img/carouselads/pageNation/default/001.png" width=500/>|・isPagerSnapEnabled : true<br>・nestedAdsSizeAdSize : DEFAULT|[->](./details/README.md#3_1)|
|<img src="/doc/img/carouselads/pageNation/aspectfit/001.png" width=500/>|・isPagerSnapEnabled : true<br>・nestedAdsSizeAdSize : ASPECT_FIT<br>|[->](./details/README.md#4_1)|
|<img src="/doc/img/carouselads/pageNation/aspectfit/002.png" width=500/>|・isPagerSnapEnabled : true<br>・nestedAdsSizeAdSize : ASPECT_FIT<br>・offsetStartWidth : 35<br>・offsetEndWidth : 35|[->](./details/README.md#4_2)|
|<img src="/doc/img/carouselads/pageNation/aspectfit/003.png" width=500/>|・isPagerSnapEnabled : true<br>・nestedAdsSizeAdSize : ASPECT_FIT<br>・overhangWidth : 35<br>・adsSeparatorWidth : 10|[->](./details/README.md#4_3)|

### 4.3 Enable pageNation and enable indicator

> ※ The display of the indicator is possible only when the pager is valid.

|Displayed image|Parameters|Details|
|:---:|:---|:---:|
|<img src="/doc/img/carouselads/pageNation/indicator/default/001.png" width=500/>|・isPagerSnapEnabled : true<br>・isIndicatorEnabled : true<br>・nestedAdsSizeAdSize : DEFAULT|[->](./details/README.md#5_1)|
|<img src="/doc/img/carouselads/pageNation/indicator/aspectfit/001.png" width=500/>|・isPagerSnapEnabled : true<br>・isIndicatorEnabled : true<br>・nestedAdsSizeAdSize : ASPECT_FIT|[->](./details/README.md#5_2)|

---
[TOP](/README.md#top)


---
LANGUAGE :
> [![ja](/doc/img/lang/ja.png)](/doc/ja/carouselads/README.md)

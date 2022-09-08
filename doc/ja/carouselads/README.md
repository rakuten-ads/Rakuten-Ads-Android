[TOP](../#top)　>　カルーセル広告

---

# カルーセル広告

[![support version](http://img.shields.io/badge/runa-1.6.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.6.0)

* **[1. 概要](#implementation)**
* **[2. カルーセル広告の基本実装](#implementation)**
  * **[2.1 ベーシックな実装](#basis_of_implementation)**
  * **[2.2 カルーセル広告の状態を検知する](#event_detection)**
* **[4. 各パラメータ別実装](#any_implementations)**


---

## 1. 概要

カルーセル広告はバナー広告を横並びに羅列し、アプリユーザーが水平方向にスクロールが可能な広告です。<br>
広告枠ID(AdSpotID)を指定した分だけ広告を表示することができます。
ダッシュボード上の広告枠設定で指定しているサイズがベースとなり端末の解像度に合わせ描画します。<br>
カルーセル枠内に表示する広告のサイズは統一しておくことを推奨します。

<center><img src="/doc/img/carouselads/001.png" height="200" /></center>

#### 前提条件

* 対応バージョン : [v1.6.0](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.6.0)以上

<div id="implementation"></div>

## 2. カルーセル広告の基本実装

<div id="basis_of_implementation"></div>

### 2.1 ベーシックな実装

カルーセル広告を実装するには[`CarouselAdView`](/doc/ja/api/CarouselAdView.md)クラスを利用します。<br>
当広告の標準表示では、内包される広告枠は左詰めで表示し、右詰での表示をすることはできません。<br>
表示させる対象となるActivityまたはFragment上に配置するには、それらのレイアウトXMLファイルにて定義する方法と直接プログラム上で定義する２通りの方法があります。<br>

<details>
<summary><b>XMLファイルによる定義</b></summary>

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
<summary><b>プログラムのみによる定義</b></summary>

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

### 2.2 カルーセル広告の状態を検知する

広告のイベントに沿ってアプリの動作をカスタマイズするには、[`CarouselAdStateListener`](/doc/ja/api/CarouselAdStateListener.md)クラスを利用します。<br>
CarouselAdView$`setCarouselAdStateListener()`メソッドに定義したCarouselAdStateListenerをセットすることでイベントをハンドリングすることができるようになります。

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
    }
}
```

|メソッド名|説明|
|:---|:---|
|onLoadSuccess(View)|CarouselAdViewにセットした広告枠IDごとに読み込みが成功する度に呼ばれます|
|onLoadFailure(View, ErrorState)|CarouselAdViewにセットした広告枠IDごとに、広告リクエストが失敗した都度呼ばれます。|
|onClick(View, ErrorState)|広告がクリックされた時に呼ばれます。|
|onLeftApplication()|広告がクリックされ、アプリケーションから離れる時に呼ばれます。|
|onAdCloseed()|広告をクリックしリンク先への遷移後、アプリに戻ると呼ばれます。|
|onAllLoadsFinished()|CarouselAdViewにセットした広告枠IDのロードが全て終了した時に呼ばれます。この場合、各々の読み込み結果の成否に関係なく読み込み処理が終了した時点で呼ばれます。|

<div id="any_implementations"></div>

## 4. 各パラメータ別実装

### 4.1 ページングが無効(Default)

|描画イメージ|パラメータ|詳細|
|:---:|:---|:---:|
|<img src="/doc/img/carouselads/nonPageNation/default/001.png" width=500/>|・nestedAdsSizeAdSize : DEFAULT<br>・adsSeparatorWidth : 0|[->](./details/README.md#1_1)|
|<img src="/doc/img/carouselads/nonPageNation/default/002.png" width=500/>|・nestedAdsSizeAdSize : DEFAULT<br>・offsetStartWidth : 35<br>|[->](./details/README.md#1_2)|
|<img src="/doc/img/carouselads/nonPageNation/default/003.png" width=500/>|・nestedAdsSizeAdSize : DEFAULT<br>・offsetEndWidth : 35<br>|[->](./details/README.md#1_3)|
|<img src="/doc/img/carouselads/nonPageNation/default/004.png" width=500/>|・nestedAdsSizeAdSize : DEFAULT<br>・adsSeparatorWidth : 35|[->](./details/README.md#1_4)|
|<img src="/doc/img/carouselads/nonPageNation/aspectfit/001.png" width=500/>|・nestedAdsSizeAdSize : ASPECT_FIT|[->](./details/README.md#2_1)|
|<img src="/doc/img/carouselads/nonPageNation/aspectfit/002.png" width=500/>|・nestedAdsSizeAdSize : ASPECT_FIT<br>・offsetStartWidth : 35<br>|[->](./details/README.md#2_2)|
|<img src="/doc/img/carouselads/nonPageNation/aspectfit/003.png" width=500/>|・nestedAdsSizeAdSize : ASPECT_FIT<br>・offsetEndWidth : 35<br>|[->](./details/README.md#2_3)|
|<img src="/doc/img/carouselads/nonPageNation/aspectfit/004.png" width=500/>|・nestedAdsSizeAdSize : ASPECT_FIT<br>・adsSeparatorWidth : 35<br>|[->](./details/README.md#2_4)|

### 4.2 ページングが有効

|描画イメージ|パラメータ|詳細|
|:---:|:---|:---:|
|<img src="/doc/img/carouselads/pageNation/default/001.png" width=500/>|・isPagerSnapEnabled : true<br>・nestedAdsSizeAdSize : DEFAULT|[->](./details/README.md#3_1)|
|<img src="/doc/img/carouselads/pageNation/aspectfit/001.png" width=500/>|・isPagerSnapEnabled : true<br>・nestedAdsSizeAdSize : ASPECT_FIT<br>|[->](./details/README.md#4_1)|
|<img src="/doc/img/carouselads/pageNation/aspectfit/002.png" width=500/>|・isPagerSnapEnabled : true<br>・nestedAdsSizeAdSize : ASPECT_FIT<br>・offsetStartWidth : 35<br>・offsetEndWidth : 35|[->](./details/README.md#4_2)|
|<img src="/doc/img/carouselads/pageNation/aspectfit/003.png" width=500/>|・isPagerSnapEnabled : true<br>・nestedAdsSizeAdSize : ASPECT_FIT<br>・overhangWidth : 35<br>・adsSeparatorWidth : 10|[->](./details/README.md#4_3)|

### 4.3 ページャーが有効・インジケーターが有効

> ※ インジケーターの表示はページャー有効時のみ可能です。

|描画イメージ|パラメータ|詳細|
|:---:|:---|:---:|
|<img src="/doc/img/carouselads/pageNation/indicator/default/001.png" width=500/>|・isPagerSnapEnabled : true<br>・isIndicatorEnabled : true<br>・nestedAdsSizeAdSize : DEFAULT|[->](./details/README.md#5_1)|
|<img src="/doc/img/carouselads/pageNation/indicator/aspectfit/001.png" width=500/>|・isPagerSnapEnabled : true<br>・isIndicatorEnabled : true<br>・nestedAdsSizeAdSize : ASPECT_FIT|[->](./details/README.md#5_2)|

---
[TOP](../#top)


---
LANGUAGE :
> [![en](/doc/img/lang/en.png)](/doc/carouselads/README.md)

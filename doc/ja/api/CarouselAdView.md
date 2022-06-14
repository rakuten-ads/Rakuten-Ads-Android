[TOP](../#top)　>　[API](./README.md)　>　CarouselAdView

---

# CarouselAdView

[![support version](http://img.shields.io/badge/runa-1.6.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.6.0)

[android.view.ViewGroup](https://developer.android.com/reference/android/view/ViewGroup)<br>
&nbsp;&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.CarouselAdView

複数のAdViewをカルーセル表示するためのViewオブジェクト。

### 公開メソッド

|戻り値|メソッド名|説明|
:---:|:---|:---
[CarouselAdStateListener](./CarouselAdStateListener.md)? | setCarouselAdStateListener | カルーセル広告の状態のコールバックのセッターとゲッター。
void | isPagerSnapEnabled(Boolean) | CarouselAdViewをスワイプした際のスライド時に慣性を働かせず吸着するアニメーションを有効にします。デフォルト: false
[AdSize](./AdSize.md) | nestedAdsSize | カルーセル内に表示する広告のサイズの指定および取得します。(デフォルト:DEFAULT。)<br>DEFAULT : ダッシュボードで設定したサイズで表示します。<br>ASPECT_FIT : 広告のサイズの比率を保ちCarouselAdViewのwidthに合わせます。<br>CUSTOM : 任意の横幅・縦幅を指定することができます。
Int | nestedAdsCustomWidth |　AdSizeをCUSTOMとした際に任意の横幅(px)を指定することができます。<br>本パラメータに実数値を指定した場合には、nestedAdsCustomHeightをwrap_contentにすることで表示する広告の比率を崩すことなく表示することができます。
Int | nestedAdsCustomHeight | AdSizeをCUSTOMとした際に任意の縦幅を指定することができます。<br>本パラメータに実数値を指定した場合には、nestedAdsCustomWidthをwrap_contentにすることで表示する広告の比率を崩すことなく表示することができます。
Int | overhangWidth | nestedAdsSizeをASPECT_FITを設定し複数の広告を表示した際に、隣接する広告をはみ出させる幅を指定できます。
Int | adsSeparatorWidth | 広告間の幅を指定できます。
Boolean | isIndicatorEnabled | インジケーターの表示有無の設定および取得します。2つ以上の広告が表示される場合に有効となります。
Drawable | indicatorBackground | インジケーターの背景の設定および取得します。
CarouselAdView | addAdSpotId(vararg String) | 広告枠IDを追加します。
CarouselAdVIew | addAdSpotId(String, JSONObject) | 広告枠IDとその枠のプロパティを追加します。
Array<Pair<String, JSONObject?>> | getAdSpotIds() | 追加済みの広告枠IDとそのプロパティのペアを配列で取得します。
void | clearAdSpotIds() | 追加している広告枠ID情報を削除します。
void | addAdSpotCode(vararg String) | 広告枠コードを追加します。
CarouselAdVIew | addAdSpotCode(String, JSONObject) | 広告枠コードとその枠のプロパティを追加します。
Array<Pair<String, JSONObject?>> | getAdSpotCodes() | 追加済みの広告枠コードとそのプロパティのペアを配列で取得します。
void | clearAdSpotCodes() | 追加している広告枠コード情報を削除します。
CarouselAdView | add(vararg AdViews) | AdViewを追加し広告を表示します。AdViewにはadSpotIdまたはadSpotCodeが指定されていなければエラーとなります。
Array<AdView> | getAdViews() | 追加してあるAdViewを配列で返します。
void | clearAdViews() | 追加済みのAdViewを削除します。
CarouselAdView | putProperty(String, Any) | 必要に応じてKey/Valueでプロパティを追加します。
Bundle | getProperty() | 設定済みのプロパティをBundleで返します。
void | setProperty(Bundle) | プロパティをBundleで設定します。
Boolean | isLoading() | 広告の読み込み中かを返します。
void | show() | 広告の描画を開始します。

### XML属性

XMLレイアウトから以下のパラメータの設定が可能です。

- #### adSpotIds
> Related Methods : `addAdSpotId(vararg String)`
- #### pagerSnapEnabled
> Related Methods : `isPagerSnapEnabled(Boolean)`
- #### nestedAdsSize
> Related Methods : `setNestedAdsSize(AdSize)`
- #### nestedAdsCustomWidth
> Related Methods : `setNestedAdsCustomWidth(Int)`
- #### nestedAdsCustomHeight
> Related Methods : `setNestedAdsCustomHeight(Int)`
- #### adsOverhangWidth
> Related Methods : `setAdsOverhangWidth(Int)`
- #### adsSeparatorWidth
> Related Methods : `setAdsSeparatorWidth(Int)`
- #### indicatorEnabled
> Related Methods : `isIndicatorEnabled(Boolean)`
- #### indicatorBackground
> Related Methods : `setIndicatorBackground(Drawable)`


### サンプル

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:runa="http://schemas.android.com/apk/res-auto"

    <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <com.rakuten.android.ads.runa.CarouselAdView
                    android:id="@+id/carouselAd"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    runa:nestedAdsSize="AspectFit"
                    runa:adsSeparatorWidth="8dp"
                    runa:pagerSnapEnabled="true"
                    app:layout_constraintStart_toStartOf="parent"
                    app:layout_constraintTop_toTopOf="parent"
                    app:layout_constraintEnd_toEndOf="parent" />

    </androidx.constraintlayout.widget.ConstraintLayout>

</layout>
```

```kotlin
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        binding.carouselAd.apply {
            addAdSpotId(100, 101, 102)
            carouselAdStateListener = object: CarouselAdStateListener {
                override fun onLoadSuccess(view: View?) {

                }
                override fun onLoadFailure(view: View?, errorState: ErrorState) {

                }
                override fun onAllLoadsFinished() {

                }
            }
        }.show()
}
...
```


---

* [API一覧](./README.md)

* [TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/api/CarouselAdView.md)

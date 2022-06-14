[TOP](../#top)　>　[API](./README.md)　>　CarouselAdView

---

# CarouselAdView

[![support version](http://img.shields.io/badge/runa-1.6.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.6.0)

[android.view.ViewGroup](https://developer.android.com/reference/android/view/ViewGroup)<br>
&nbsp;&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.CarouselAdView

View object for carousel ads. Ad spot ID or Ad spot Code must be set prior to calling `show()`.

### Public Method / Field

|Return|method / field|Details|
:---:|:---|:---
[CarouselAdStateListener](./CarouselAdStateListener.md)? | setCarouselAdStateListener | Sets a listener for receiving notifications during the lifecycle of ads.
void | isPagerSnapEnabled(Boolean) | Enables animation that sticks without inertia when swiping CarouselAdView.<br>(Default : false)
[AdSize](./AdSize.md) | nestedAdsSize | Specify and get the size of the ad to display in the carousel.<br>(Default : AdSize.DEFAULT)<br>DEFAULT : It is displayed with the size set on the dashboard.<br>ASPECT_FIT : Keep the ad size ratio to fit the width of the Carousel AdView.<br>CUSTOM : Specify any width and height.
Int | nestedAdsCustomWidth |　Any width(px) can be specified when AdSize is set to CUSTOM.<br>If you specify a real value for this parameter, you can display it without breaking the ratio of the displayed advertisement by setting `nestedAdsCustomHeight` to wrap_content.
Int | nestedAdsCustomHeight | Any height(px) can be specified when AdSize is set to CUSTOM.<br>If you specify a real value for this parameter, you can display it without breaking the ratio of the displayed advertisement by setting `nestedAdsCustomWidth` to wrap_content.
Int | overhangWidth | If you set ASPECT_FIT to `nestedAdsSize` and display multiple ads, you can specify the width to extend the adjacent ads.
Int | adsSeparatorWidth | pecify the interval width of the ad.
Boolean | isIndicatorEnabled | Set and get whether to display the indicator.(Valid when more than one ad is displayed.)
Drawable | indicatorBackground | Set and get the background of the indicator's dot.
CarouselAdView | addAdSpotId(vararg String) | Adds ad spot ID.
CarouselAdVIew | addAdSpotId(String, JSONObject) | Adds ad spot ID and a property of this ad spot.
Array<Pair<String, JSONObject?>> | getAdSpotIds() | Get an array of added ad spot IDs and their property pairs.
void | clearAdSpotIds() | Delete the added ad spot IDs information.
void | addAdSpotCode(vararg String) | Adds ad spot code.
CarouselAdVIew | addAdSpotCode(String, JSONObject) | Adds ad spot code and a property of this ad spot.
Array<Pair<String, JSONObject?>> | getAdSpotCodes() | Get an array of added ad spot code and their property pairs.
void | clearAdSpotCodes() | Delete the added ad spot code information.
CarouselAdView | add(vararg AdViews) | Add an AdView to show your ad. If adSpotId or adSpotCode is not specified in AdView, an error will occur.
Array<AdView> | getAdViews() | Returns the added AdView as an array.
void | clearAdViews() | Delete the added AdView.
CarouselAdView | putProperty(String, Any) | Add properties with Key / Value as needed.
Bundle | getProperty() | Returns the set properties as a Bundle.
void | setProperty(Bundle) | Sets the property in Bundle.
Boolean | isLoading() | Returns whether the ad is loading.
void | show() | Start drawing the ad.


### Sample

The following is a sample defined in xml and called from Kotlin.

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

```java
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

* [API](./README.md)

* [TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/ja/api/CarouselAdView.md)

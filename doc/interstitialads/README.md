[TOP](../#top)　>　Interstitial Ads

---

# Interstitial Ads

[![support version](http://img.shields.io/badge/runa-1.6.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.9.1)

An interstitial is a full-screen advertisement that is primarily displayed during transitions between screens.

> **[Screen A] -> [Display InterstitialAds] -> <Close ads> -> [Screen B]**

### Basic implementation

　To display an interstitial ads, you can use the `InterstitialAd` class.<br>
You can start loading the ad with the `load` method and detect when the loading is complete using the `InterstitialAdLoadListener` that you set as an argument.<br>
When the ad is successfully loaded, the `onLoadSuccess` method is called and you can obtain the `InterstitialAd` object as an argument.<br>
You can detect events for the interstitial ad after it is displayed by setting an `InterstitialAdListener` on the `InterstitialAd` object.<br>
Finally, to display the interstitial ad, call `InterstitialAd.show(Activity)` method.

```java
import com.rakuten.android.ads.runa.ErrorState
import com.rakuten.android.ads.runa.InterstitialAd
import com.rakuten.android.ads.runa.InterstitialAdListener
import com.rakuten.android.ads.runa.InterstitialAdLoadListener import com.rakuten.android.ads.runa.InterstitialAdSpotData
private var mInterstitialAd: InterstitialAd? = null

...

  val adSpotData = InterstitialAdSpotData(
    adSpotId = "{adSpotId}",
    adSpotCode = "{adSpotCode}",
    adSize = AdSize.ASPECT_FIT
  )

  InterstitialAd.load(context,
    adSpotData,
    object : InterstitialAdLoadListener() {
      override fun onLoadSuccess(interstitialAd: InterstitialAd) {
        // This method should be called when the interstitial ad is ready to be displayed.
        mInterstitialAd = interstitialAd
        mInterstitialAd?.interstitialAdListener = object : InterstitialAdListener() {
          override fun onDismiss() {
            // You can detect when the interstitial ad is closed using an event listener.
            // And implement the logic to transition to the next screen primarily after the interstitial ad is closed.
            Intent(requireActivity(), ScreenB::java.class).run {
                startActivity(this)
            }
          }
        }
      }

      override fun onLoadFailure(errorState: ErrorState) {
        // When ad load is failed
      }
    })
...

override fun onClick(v: View) {
  // You can display the interstitial ad when transitioning to the next screen.
  mInterstitialAd.show(requireActivity())
}
```

### Detect Interstitial Ads State

|Method|Details|
|:---|:---|
|onLoadSuccess(View)|Called every time loading is successful for each ad spot ID set in CarouselAdView|
|onLoadFailure(View, ErrorState)|Called each time an ad request fails for each ad spot ID set in CarouselAdView.|
|onClick(View, ErrorState)|Called when an ad is clicked.|
|onLeftApplication()|Called when an ad is clicked and leaves the application.|
|onAdCloseed()|Called Return to app after clicking ad and navigating to destination.|
|onDismiss()|Called when an interstitial ad is closed.|
|onWebViewCrashed(AdView?)|Called when the process inside WebView in AdView is crashed.|

---
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/img/lang/ja.png)](/doc/ja/interstitialads/README.md)

[TOP](../#top)　>　Ad Mediation

---

# Ad Mediation

Ad mediation is a digital advertising strategy where multiple ad networks are managed through a single SDK to help publishers increase advertising revenue, fill rates, and efficiency for their available ad space.

We currently support the ad banner feature of GoogAd Mediation SDK.

---

## How to use

### Prepare Google Mobile Ads SDK

Please follow the [introduction](https://developers.google.com/admob/android/banner) to get your ad unit ID and load ads from google.

#### Enable mediation configurations in Admob console.

Ask your business side to enable the configuration of the Admob Mediation. The following 2 steps will be done.

1. Set up a mediation group

2. Add ad custom event and map it with class name `com.rakuten.android.ads.runa.gad.adapter.RunaGADCustomEvent` as the ad source.

### Introduce `RunaGADCustomEvent`

#### Import RUNA SDK

Apps can import the RDN Mobile Ads SDK with a Gradle dependency. In order to use that repository, you need to reference it in the app's project-level build.gradle file. Open yours and look for an allprojects section:

```groovy
allprojects {
    repositories {
        jcenter()
        maven {
          url 'https://github.com/rakuten-ads/Rakuten-Ads-Android/raw/master/maven'
        }
    }
}
```

Next, open the app-level `build.gradle` file for your app, and add runa and runa-gad-adapter to "dependencies" section.

```groovy
  implementation 'com.rakuten.android.ads:runa:1.12.1'
  implementation 'com.rakuten.android.ads:runa-gad-adapter:1.0.0'
```

#### Configure RUNA parameters

You can set some parameters of RUNA with `RunaCustomEventConfig` and pass it to `addNetworkExtrasBundle()` in `AdRequest`.

You have to set `adSpotId` or `adSpotCode` at least.

```kotlin
val adView = AdView(context)
val size = getSize(args.adSize, view)
adView.setAdSize(size)
adView.adUnitId = "<Your Ad Unit ID>"

val adRequestBuilder = AdRequest.Builder()
val runaConf = RunaCustomEventConfig()
runaConf.setAdSpotId(123456)
adRequestBuilder.addNetworkExtrasBundle(RunaGADCustomEvent::class.java, runaConf.bundle())
adView.loadAd(adRequestBuilder.build())
```

__Supported parameters__

- adSpotId
- adSpotCode
- adSpotBranchId
- rz
- rp
- easyId
- rpoint
- customTargeting
- genre

---
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/img/lang/ja.png)](/doc/ja/mediation/README.md)

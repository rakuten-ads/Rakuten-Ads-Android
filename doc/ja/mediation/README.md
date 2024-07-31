[TOP](../#top)　>　Ad Mediation

---

# Ad Mediation

広告メディエーションはデジタル広告戦略であり、複数の広告ネットワークが単一の SDK を通じて管理され、サイト運営者が広告収入、広告掲載率、利用可能な広告スペースの効率を向上させるのに役立ちます。

現在、GoogAd Mediation SDK の広告バナー機能をサポートしています。

---

## How to use

### Google Mobile Ads SDK の導入

こちらの[ドキュメント](https://developers.google.com/admob/android/banner)に従って、Ad Unit ID を取得し Google の広告を取得できるように実装してください。

#### AdMob のコンソール画面で Mediation の機能を有効化

所属している組織のビジネス側の担当者に Admob メディエーションの設定を有効にするよう依頼してください。以下の2ステップを行います。

1. メディエーショングループのセットアップ

2. 広告カスタムイベントを追加し、クラス名「com.rakuten.android.ads.runa.gad.adapter.RunaGADCustomEvent」を広告ソースとしてマッピング

### `RunaGADCustomEvent` の導入

#### RUNA SDK のインポート

Gradle の依存設定でアプリにインポートすることが出来ます。プロジェクト直下のbuild.gradleの repositories に以下のように参照先を追加する必要があります。

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

次に、アプリ直下のbuild.gradleのdependenciesに以下の指定を追加します。

```groovy
  implementation 'com.rakuten.android.ads:runa:1.12.0'
  implementation 'com.rakuten.android.ads:runa-gad-adapter:1.0.0'
```

#### RUNA のパラメータを設定

RunaCustomEventConfig のインスタンスに RUNA の各パラメータを設定することができ、それを Google SDK の `AdRequest` 内の `addNetworkExtrabundles()` の引数として渡すことで RUNA 広告に適用することができます。

`adSpotId` もしくは `adSpotCode` は必須パラメータです。

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

__利用可能なパラメータ__

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
> [![en](/doc/img/lang/en.png)](/doc/interstitialads/README.md)

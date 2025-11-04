[TOP](../#top)　>　インタースティーシャル広告

---

# インタースティーシャル広告

インタースティーシャルは全画面表示の広告です。<br>
主に画面遷移の間に表示させる用途となります。

> **[画面A] -> [インタースティーシャル広告表示] -> <広告を閉じる> -> [画面B]**

### 広告を表示する

　インタースティーシャル広告の表示には`InterstitialAd`クラスを利用します。<br>
`load`メソッドで読み込みを開始し、引数に設定した`InterstitialAdLoadListener`で読み込み完了を検知させます。<br>
正常に読み込まれると`onLoadSuccess`が呼ばれ、引数の`InterstitialAd`を取得することができます。<br>
`InterstitialAd`に`InterstitialAdListener`をセットすることで表示後のインタースティーシャル広告のイベントの検知ができます。<br>
最終的にインタースティーシャル広告の表示は`InterstitialAd$show(Activity)`を実行してください。

```java
import com.rakuten.android.ads.runa.ErrorState
import com.rakuten.android.ads.runa.InterstitialAd
import com.rakuten.android.ads.runa.InterstitialAdListener
import com.rakuten.android.ads.runa.InterstitialAdLoadListener
import com.rakuten.android.ads.runa.InterstitialAdSpotData

var mInterstitialAd: InterstitialAd? = null

val adSpotData = InterstitialAdSpotData(
  adSpotId = "{adSpotId}",
  adSpotCode = "{adSpotCode}",
  adSize = AdSize.ASPECT_FIT
)

InterstitialAd.load(context,
  adSpotData,
  object : InterstitialAdLoadListener() {
    override fun onLoadSuccess(interstitialAd: InterstitialAd) {
      // インタースティーシャル広告の表示が可能な状態になると呼ばれます
      mInterstitialAd = interstitialAd
      mInterstitialAd?.interstitialAdListener = object : InterstitialAdListener() {
        override fun onDismiss() {
          // インタースティーシャル広告を閉じたイベントを検知します
          // 主に次の画面に遷移するための処理を実装します
          Intent(requireActivity(), ScreenB::java.class).run {
              startActivity(this)
          }
        }
      }
    }

    override fun onLoadFailure(errorState: ErrorState) {
      // 読み込みが失敗した時に呼ばれます
    }
  })
...

override fun onClick(v: View) {
  // 画面を遷移するタイミングでインタースティーシャル広告の表示を実行します
  mInterstitialAd.show(requireActivity())
}
```

### 広告の状態を検知する

|メソッド名|説明|
|:---|:---|
|onLoadSuccess(View)|CarouselAdViewにセットした広告枠IDごとに読み込みが成功する度に呼ばれます|
|onLoadFailure(View, ErrorState)|CarouselAdViewにセットした広告枠IDごとに、広告リクエストが失敗した都度呼ばれます。|
|onClick(View, ErrorState)|広告がクリックされた時に呼ばれます。|
|onLeftApplication()|広告がクリックされ、アプリケーションから離れる時に呼ばれます。|
|onAdCloseed()|広告をクリックしリンク先への遷移後、アプリに戻ると呼ばれます。|
|onDismiss()|インタースティシャル広告が閉じられた時に呼ばれます。|
|onWebViewCrashed(AdView?)|CarouselAdView内のそれぞれのAdViewのWebViewの中でクラッシュが発生した際呼ばれます。|

### ステータスバーの非表示

`hideStatusBar` オプションを使用することでインタースティシャル広告が表示されるアクティビティのステータスバーを非表示にすることができます。

```kotlin
import com.rakuten.android.ads.runa.InterstitialAd

InterstitialAd.hideStatusBar = true
```

---
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/img/lang/en.png)](/doc/interstitialads/README.md)

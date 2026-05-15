[TOP](../#top)　>　動画広告

---

# 動画広告

* **[1. 概要](#overview)**
* **[2. レイアウト XML に VideoAdView を定義する](#define_xml)**
* **[3. RUNA 広告サーバーから広告データを取得する](#fetch_ad)**
* **[4. 動画広告を表示する](#display)**
* **[5. 広告の状態を検知する](#detect_state)**

---

<div id="overview"></div>

## 1. 概要

`VideoAdView` は VAST ベースのインフィード動画広告を表示するためのビューです。

- **アスペクト比**: 16:9 固定（高さは横幅から自動計算）
- **自動再生**: 画面上に 50% 以上表示された時点で自動的に再生を開始
- **自動一時停止**: 表示面積が 50% 未満になると自動的に一時停止
- **ビューアブルインプレッション**: 50% 以上の表示が 2 秒以上継続した時点でビューアブルインプレッションリクエストを送信

---

<div id="define_xml"></div>

## 2. レイアウト XML に VideoAdView を定義する

`VideoAdView` の横幅は `match_parent` を指定してください。高さは `横幅 × 9 / 16` で自動計算されます。

```xml
<com.rakuten.android.ads.runa.VideoAdView
    android:id="@+id/video_ad_view"
    android:layout_width="match_parent"
    android:layout_height="wrap_content" />
```

---

<div id="fetch_ad"></div>

## 3. RUNA 広告サーバーから広告データを取得する

`VideoAdView` の表示には、RUNA 広告サーバーのレスポンスから取得した以下の 3 つの値が必要です。

| プロパティ | レスポンスフィールド | 説明 |
|:---|:---|:---|
| `vastXml` | `seatbid[].bid[].ext.vast_xml` | 動画レンダリング用の VAST XML 文字列 |
| `impUrl` | `seatbid[].bid[].ext.impression_url` | インプレッション計測 URL |
| `inviewUrl` | `seatbid[].bid[].ext.inview_url` | ビューアブルインプレッション計測 URL |

広告枠 ID を指定して RUNA 広告サーバーの `POST /ad2` エンドポイントを呼び出すことでレスポンスを取得できます。

<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.VideoAdView

class YourFragment : Fragment() {

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        val videoAdView = view.findViewById<VideoAdView>(R.id.video_ad_view)

        // RUNA 広告サーバーから広告レスポンスを取得
        fetchAdResponse(adspotId = YOUR_ADSPOT_ID) { response ->
            val ext = response.seatbid.firstOrNull()?.bid?.firstOrNull()?.ext
                ?: return@fetchAdResponse

            // 広告なし（unfilled）の場合はスキップ
            if (ext.unfilledImpressionUrl.isNotEmpty()) return@fetchAdResponse

            videoAdView.vastXml   = ext.vastXml
            videoAdView.impUrl    = ext.impressionUrl
            videoAdView.inviewUrl = ext.inviewUrl
            videoAdView.show()
        }
    }
}
```

</details>

---

<div id="display"></div>

## 4. 動画広告を表示する

`VideoAdView` に必要なプロパティをセットして `show()` を呼び出します。

| プロパティ | 型 | 必須 | 説明 |
|:---|:---|:---:|:---|
| `vastXml` | `String` | ✓ | VAST XML 文字列 |
| `impUrl` | `String` | ✓ | インプレッション計測 URL |
| `inviewUrl` | `String` | ✓ | ビューアブルインプレッション計測 URL |
| `adStateListener` | `VideoAdStateListener` | | 広告イベントを検知するリスナー |

`vastXml`・`impUrl`・`inviewUrl` のいずれかが未設定の状態で `show()` を呼び出すと `IllegalArgumentException` がスローされます。

<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.VideoAdView

videoAdView.vastXml   = ext.vastXml
videoAdView.impUrl    = ext.impressionUrl
videoAdView.inviewUrl = ext.inviewUrl
videoAdView.adStateListener = object : VideoAdView.VideoAdStateListener() {
    override fun onLoadSuccess(adView: View?) {
        // 動画の読み込み成功・再生準備完了
    }
    override fun onLoadFailure(adView: View?, errorState: ErrorState) {
        // 動画広告の読み込み失敗
    }
    override fun onClick(adView: View?, errorState: ErrorState?) {
        // 動画広告がクリックされた
    }
    override fun onVideoError(adView: VideoAdView?, err: Error) {
        // 動画再生中にエラーが発生した
    }
}
videoAdView.show()
```

</details>

---

<div id="detect_state"></div>

## 5. 広告の状態を検知する

`VideoAdView.VideoAdStateListener` を使用して広告のライフサイクルイベントを処理します。<br>
`VideoAdStateListener` は [`AdStateListener`](../api/AdStateListener.md) を継承し、動画固有のコールバックを 1 つ追加しています。

| メソッド | 説明 |
|:---|:---|
| `onLoadSuccess(adView: View?)` | 動画の読み込みが成功し、再生準備が完了したときに呼ばれる |
| `onLoadFailure(adView: View?, errorState: ErrorState)` | 内部の HTML テンプレート取得に失敗したときに呼ばれる（`ErrorState.INTERNAL_ERROR` のみ） |
| `onClick(adView: View?, errorState: ErrorState?)` | 動画広告がクリックされたときに呼ばれる |
| `onVideoError(adView: VideoAdView?, err: Error)` | 動画再生中にエラーが発生したときに呼ばれる |

<details>
<summary><b>Kotlinによる実装</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.VideoAdView
import com.rakuten.android.ads.runa.ErrorState

videoAdView.adStateListener = object : VideoAdView.VideoAdStateListener() {

    override fun onLoadSuccess(adView: View?) {
        // 動画の再生準備が完了
    }

    override fun onLoadFailure(adView: View?, errorState: ErrorState) {
        // 読み込み失敗時にコンテナを非表示にする例
        adView?.visibility = View.GONE
    }

    override fun onClick(adView: View?, errorState: ErrorState?) {
        // クリック時の処理
    }

    override fun onVideoError(adView: VideoAdView?, err: Error) {
        // 再生エラー時の処理
    }
}
```

</details>

---

[TOP](../#top)

---

LANGUAGE :

> [![en](/doc/img/lang/en.png)](/doc/video/README.md)

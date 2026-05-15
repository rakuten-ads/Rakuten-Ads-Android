[TOP](/README.md#top)　>　Video Ads

---

# Video Ads

* **[1. Overview](#overview)**
* **[2. Define VideoAdView in layout XML](#define_xml)**
* **[3. Fetch ad data from RUNA ad server](#fetch_ad)**
* **[4. Display video ad](#display)**
* **[5. Detect ad state](#detect_state)**

---

<div id="overview"></div>

## 1. Overview

`VideoAdView` displays VAST-based in-feed video ads.

- **Aspect ratio**: Fixed at 16:9 (height is calculated automatically from width)
- **Auto-play**: Starts automatically when 50% or more of the view is visible on screen
- **Auto-pause**: Pauses when less than 50% is visible
- **Viewable impression**: Sends a viewable impression request when 50% or more of the view remains visible for 2 seconds or more

---

<div id="define_xml"></div>

## 2. Define VideoAdView in layout XML

`VideoAdView` width should be set to `match_parent`. Height is automatically calculated as `width × 9 / 16`.

```xml
<com.rakuten.android.ads.runa.VideoAdView
    android:id="@+id/video_ad_view"
    android:layout_width="match_parent"
    android:layout_height="wrap_content" />
```

---

<div id="fetch_ad"></div>

## 3. Fetch ad data from RUNA ad server

`VideoAdView` requires three values obtained from the RUNA ad server response:

| Property | Response field | Description |
|:---|:---|:---|
| `vastXml` | `seatbid[].bid[].ext.vast_xml` | VAST XML string for video rendering |
| `impUrl` | `seatbid[].bid[].ext.impression_url` | Impression tracking URL |
| `inviewUrl` | `seatbid[].bid[].ext.inview_url` | Viewable impression tracking URL |

Call the RUNA ad server `POST /ad2` endpoint with your adspot ID to retrieve the response.

<details>
<summary><b>Kotlin</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.VideoAdView

class YourFragment : Fragment() {

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        val videoAdView = view.findViewById<VideoAdView>(R.id.video_ad_view)

        // Fetch ad response from RUNA ad server
        fetchAdResponse(adspotId = YOUR_ADSPOT_ID) { response ->
            val ext = response.seatbid.firstOrNull()?.bid?.firstOrNull()?.ext
                ?: return@fetchAdResponse

            // Check for unfilled
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

## 4. Display video ad

Set the required properties on `VideoAdView` and call `show()`.

| Property | Type | Required | Description |
|:---|:---|:---:|:---|
| `vastXml` | `String` | ✓ | VAST XML string |
| `impUrl` | `String` | ✓ | Impression tracking URL |
| `inviewUrl` | `String` | ✓ | Viewable impression tracking URL |
| `adStateListener` | `VideoAdStateListener` | | Listener to detect ad events |

`show()` throws `IllegalArgumentException` if any of `vastXml`, `impUrl`, or `inviewUrl` is not set.

<details>
<summary><b>Kotlin</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.VideoAdView

videoAdView.vastXml   = ext.vastXml
videoAdView.impUrl    = ext.impressionUrl
videoAdView.inviewUrl = ext.inviewUrl
videoAdView.adStateListener = object : VideoAdView.VideoAdStateListener() {
    override fun onLoadSuccess(adView: View?) {
        // Video loaded successfully and is ready to play
    }
    override fun onLoadFailure(adView: View?, errorState: ErrorState) {
        // Failed to load the video ad
    }
    override fun onClick(adView: View?, errorState: ErrorState?) {
        // Video ad was clicked
    }
    override fun onVideoError(adView: VideoAdView?, err: Error) {
        // An error occurred during video playback
    }
}
videoAdView.show()
```

</details>

---

<div id="detect_state"></div>

## 5. Detect ad state

Use `VideoAdView.VideoAdStateListener` to handle ad lifecycle events.  
`VideoAdStateListener` extends [`AdStateListener`](../api/AdStateListener.md) and adds one video-specific callback.

| Method | Description |
|:---|:---|
| `onLoadSuccess(adView: View?)` | Called when the video has loaded successfully and is ready to play |
| `onLoadFailure(adView: View?, errorState: ErrorState)` | Called when the HTML template fetch fails internally (`ErrorState.INTERNAL_ERROR`) |
| `onClick(adView: View?, errorState: ErrorState?)` | Called when the video ad is clicked |
| `onVideoError(adView: VideoAdView?, err: Error)` | Called when an error occurs during video playback |

<details>
<summary><b>Kotlin</b></summary>

[![Language](http://img.shields.io/badge/language-Kotlin-green.svg?style=flat)](https://kotlinlang.org/)

```kotlin
import com.rakuten.android.ads.runa.VideoAdView
import com.rakuten.android.ads.runa.ErrorState

videoAdView.adStateListener = object : VideoAdView.VideoAdStateListener() {

    override fun onLoadSuccess(adView: View?) {
        // Video is ready to play
    }

    override fun onLoadFailure(adView: View?, errorState: ErrorState) {
        // Hide the container if ad failed to load
        adView?.visibility = View.GONE
    }

    override fun onClick(adView: View?, errorState: ErrorState?) {
        // Handle click
    }

    override fun onVideoError(adView: VideoAdView?, err: Error) {
        // Handle playback error
    }
}
```

</details>

---

[TOP](/README.md#top)

---

LANGUAGE :

> [![ja](/doc/img/lang/ja.png)](/doc/ja/video/README.md)

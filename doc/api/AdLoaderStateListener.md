[TOP](../#top)　>　[API](./README.md)　>AdLoaderStateListener

---

# AdLoaderStateListener

[![support version](http://img.shields.io/badge/runa-1.3.0+-blueviolet.svg?style=flat)](https://developer.android.com)

Abstract class

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;[com.rakuten.android.ads.runa.AdStateListener](./AdStateListener.md)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdLoaderStateListener

A Listener to notify the the ad loading status by AdLoader.

### Public Constructors Summary

|constructors|
|:---|
|AdLoaderStateListener()|

### Public Method Summary

|Return|Method|Details|
|:---:|:---|:---|
|void|onAllLoadsFinished(adLoader: AdLoader, loadedAdViews: List<AdView>?)|Called when AdViews added to [AdLoader](./AdLoader.md) have been ​all loaded. The argument loadedAdViews is a list of AdViews to return if the load is successful. Returns null if all loads failed or received UNFILLED.|

### Inherited Method Summary

#### From:
* [com.rakuten.android.ads.runa.AdStateListener](./AdStateListener.md)

---

* [API](./README.md)

* [TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/api/AdLoaderStateListener.md)

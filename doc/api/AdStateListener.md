[TOP](/README.md#top)　>　[API](./README.md)　>　AdStateListener

---

# AdStateListener

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdStateListener

public abstract class **AdStateListener** extends [Object](https://developer.android.com/reference/java/lang/Object.html)<br>

A listener for receiving notifications during the lifecycle of an ad.

### Public Constructor

|constructor|
|:---|
|AdStateListener()|

### Public Method Summary

|Return|Method|Details|
|:---:|:---|:---|
|void|onLoadSuccess()|Called when ad ad request succeed.|
|void|onLoadFailure()|Called when an ad request failed. If it failed, AdView will be hidden(View.GONE) automatically.|
|void|onClick()|Called when an ad is clicked.|
|void|onLeftApplication()|Called when an ad leaves the application.|

---
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/ja/api/AdStateListener.md)

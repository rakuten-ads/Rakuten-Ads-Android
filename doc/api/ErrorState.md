[TOP](/README.md#top)　>　[API](./README.md)　>　ErrorState

---

# ErrorState

[![support version](http://img.shields.io/badge/runa-1.0.0+-blueviolet.svg?style=flat)](https://developer.android.com)

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.ErrorState

public enum class **ErrorState** extends [Object](https://developer.android.com/reference/java/lang/Object.html)<br>

Indicates the status when an error occurred in AdRequest.

### Public Parameters

|Parameter|Description|
|:---|:---|
|UNFILLED|The ad request was successful, but no ad was returned due to lack of ad inventory.|
|FATAL_ERROR|The ad request was invalid. For instance, the ad spot ID was incorrect.|
|NETWORK_ERROR|The ad request was unsuccessful due to network connectivity.|
|INTERNAL_ERROR|Something happened internally.For instance, an invalid response was received from the ad server.|

---
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/ja/api/ErrorState.md)

[TOP](../#top)　>　[API](./README.md)　>AdLoaderStateListener

---

# AdLoaderStateListener

[![support version](http://img.shields.io/badge/runa-1.3.0+-blueviolet.svg?style=flat)](https://github.com/rakuten-ads/Rakuten-Ads-Android/releases/tag/1.3.0)

Abstract class

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;[com.rakuten.android.ads.runa.AdStateListener](./AdStateListener.md)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdLoaderStateListener

[AdLoader](./AdLoader.md)による広告の読み込み状況を通知するためのListenerクラス

### コンストラクタ

|コンストラクタ|
|:---|
|AdLoaderStateListener()|

### 公開メソッド

|戻り値|メソッド名|説明|
|:---:|:---|:---|
|void|onAllLoadsFinished(adLoader: AdLoader, loadedAdViews: List&lt;AdView&gt;?)|[AdLoader](./AdLoader.md)に追加したAdViewのロードが全て終了した時に呼ばれます。引数の`loadedAdViews`はロードが成功したAdViewが含まれます。全てロードが失敗したりUnfilledの場合はnullが渡されます。|

### 継承されているメソッド

以下のクラスのメソッドを継承:
* [com.rakuten.android.ads.runa.AdStateListener](./AdStateListener.md)

---

* [API一覧](./README.md)

* [TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/api/AdLoaderStateListener.md)

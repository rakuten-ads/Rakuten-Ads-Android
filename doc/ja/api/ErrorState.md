[TOP](/README.md#top)　>　[API](./README.md)　>　ErrorState

---

# ErrorState

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.ErrorState

public enum class **ErrorState** extends [Object](https://developer.android.com/reference/java/lang/Object.html)<br>

広告リクエストでエラーが発生した時のステータスを示します。

### Public Parameters

|パラメータ|説明|
|:---|:---|
|UNFILLED|広告リクエストが成功しても、広告の在庫がない場合|
|FATAL_ERROR|広告枠IDの指定が正しくない時などの不正な広告リクエストを行う場合|
|NETWORK_ERROR|ネットワークの状況により広告リクエストが失敗した場合|
|INTERNAL_ERROR|サーバーから無効なレスポンスを受信した場合など|

---
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/api/ErrorState.md)
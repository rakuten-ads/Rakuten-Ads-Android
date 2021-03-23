[TOP](../#top)　>　[API](./README.md)　>　AdView

---

# AdView

[![support version](http://img.shields.io/badge/runa-1.0.0+-blueviolet.svg?style=flat)](https://developer.android.com)

[android.view.ViewGroup](https://developer.android.com/reference/android/view/ViewGroup)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdView

バナー広告を表示するためのViewオブジェクト。`show()`メソッドを呼び出す前に必ず、xmlレイアウト、またはコード上で`広告枠ID`をセットする必要があります。

### コンストラクタ

|constructors|
|:---|
|AdView([Context](https://developer.android.com/reference/android/content/Context.html) context)<br>　コード上で定義する際のコンストラクタ|
|AdView([Context](https://developer.android.com/reference/android/content/Context.html) context, [AttributeSet](https://developer.android.com/reference/android/util/AttributeSet.html) attrs)<br>　XMLレイアウトで定義するためのコンストラクタ|
|AdView([Context](https://developer.android.com/reference/android/content/Context.html) context, [AttributeSet](https://developer.android.com/reference/android/util/AttributeSet.html) attrs, int defStyleAttr)<br>　XMLレイアウトで定義するためのコンストラクタ|

<div id="public_methods"></div>

### 公開メソッド

|戻り値|メソッド名|説明|
|:---:|:---|:---|
|String|getAdSpotId()|広告枠IDを返します。|
|void|setAdSpotId(String adSpotId)|広告枠IDをセットします。|
|void|setAdStateListener([AdStateListener](./AdStateListener.md) listener)|[AdStateListener](./AdStateListener.md)をセットします。|
|void|show()|広告リクエストの送信と広告表示の準備をします。|

### Protectedメソッド

|戻り値|メソッド名|
|:---:|:---|
|void|onLayout(boolean changed, int left, int top, int right, int bottom)|
|void|onMeasure(int widthMeasureSpec, int heightMeasureSpec)|

### 継承されているメソッド

#### 以下のクラスのメソッドを継承:
* class [android.view.ViewGroup](https://developer.android.com/reference/android/view/ViewGroup)
* class [android.view.View](https://developer.android.com/reference/android/view/View)
* class [java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)

### XML属性
XMLレイアウトから以下のパラメータの設定が可能です。
* **adSpotId**<br>
関連するメソッド : setAdSpotId(String adSpotId)

### サンプルコード

main_layout.xml :
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:gravity="center_horizontal"
              android:orientation="vertical">

              <com.rakuten.android.ads.runa.AdView
                              xmlns:ads="http://schemas.android.com/apk/res-auto"
                              android:id="@+id/adview"
                              android:layout_width="wrap_content"
                              android:layout_height="wrap_content"
                              ads:adSpotId="1" />
</LinearLayout>
```

<br>
Activity :

```java
  @Override
  public void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.main_layout);

      AdView adView = (AdView) findViewById(R.id.adview);
      adView.setAdStateListener(new AdStateListener() {
          @Override
          public void onLoadSuccess() {
              // load succeed
          }
      });
      adView.show();
  }
```

---

* [API一覧](./README.md)

* [TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/api/AdView.md)

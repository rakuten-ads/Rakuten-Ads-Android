[TOP](/README.md#top)　>　[API](./README.md)　>　AdView

---

# AdView

[![support version](http://img.shields.io/badge/runa-1.0.0+-blueviolet.svg?style=flat)](https://developer.android.com)

[android.view.ViewGroup](https://developer.android.com/reference/android/view/ViewGroup)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdView

The View to display the Banner ad. An ad spot ID must be set via xml layout or programatically, before call `show()`.

### Public Constructors Summary

|constructors|
|:---|
|AdView([Context](https://developer.android.com/reference/android/content/Context.html) context)<br>　Construct an AdView from code.|
|AdView([Context](https://developer.android.com/reference/android/content/Context.html) context, [AttributeSet](https://developer.android.com/reference/android/util/AttributeSet.html) attrs)<br>　Construct an AdView from xml layout.|
|AdView([Context](https://developer.android.com/reference/android/content/Context.html) context, [AttributeSet](https://developer.android.com/reference/android/util/AttributeSet.html) attrs, int defStyleAttr)<br>　Construct an AdView from xml layout.|

### Public Method Summary

|Return|Method|Details|
|:---:|:---|:---|
|String|getAdSpotId()|Returns the set ad spot ID.|
|void|setAdSpotId(String adSpotId)|Sets an ad spot ID.|
|void|setAdStateListener([AdStateListener](./AdStateListener.md) listener)|Sets an [AdStateListener](./AdStateListener.md).|
|void|show()|Sends ad request and display a prepared ad.|

### Protected Method Summary

|Return|Method|
|:---:|:---|
|void|onLayout(boolean changed, int left, int top, int right, int bottom)|
|void|onMeasure(int widthMeasureSpec, int heightMeasureSpec)|

### Inherited Method Summary

#### From:
* class [android.view.ViewGroup](https://developer.android.com/reference/android/view/ViewGroup)
* class [android.view.View](https://developer.android.com/reference/android/view/View)
* class [java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)

### XML Attribute

* **adSpotId**<br>
Related method : setAdSpotId(String adSpotId)

### Sample Code

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
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/lang/ja.png)](/doc/ja/api/AdView.md)

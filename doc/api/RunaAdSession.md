[TOP](../#top)　>　[API](./README.md)　>　RunaAdSession

---

# RunaAdSession

[![support version](http://img.shields.io/badge/runa-1.2.0+-blueviolet.svg?style=flat)](https://developer.android.com)

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.RunaAdSession

An object to avoid duplication between multiple AdViews.


### Public Method Summary

|Return|Method|Details|
|:---:|:---|:---|
|void|bind([AdView](./AdView.md))|Avoid duplication of ads displayed between added AdViews.<br>This method must be call before execute [`AdView$show()`](./AdView.md#public_methods).|

### Implementation Sample

```kotlin
import com.rakuten.android.ads.runa.AdView
import com.rakuten.android.ads.runa.AdStateListener
...

private val adSession = RunaAdSession()

...

override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        val adView1 = findViewById<AdView>(R.id.adview1)
        val adView2 = findViewById<AdView>(R.id.adview2)

        adSession.bind(adView1, adView2)


        adView1.apply {
              adStateListener = object: AdStateListener() {
                    override fun onLoadSuccess() {
                        adView2.show()
                    }
                    override fun onLoadFailure(adView: View?) {
                        adView2.show()
                    }
              }
        }.show()
}
...
```

> [Other samples](../bannerads/sample_ad_session.md) when implementing on a list.


---
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/api/RunaAdSession.md)

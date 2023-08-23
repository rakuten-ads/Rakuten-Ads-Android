[TOP](/README.md#top)　>　[API](./README.md)　>　 AdSize

---

# AdSize

![support version](http://img.shields.io/badge/runa-1.0.0+-blueviolet.svg?style=flat)

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdSize

public enum class **AdSize** extends [Object](https://developer.android.com/reference/java/lang/Object.html)<br>

An enum class for adjusting the size of the [AdView](./AdView.md).

### Public Parameters

| Parameter     | Description                                                                                                                                           |
| :------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------- |
| DEFAULT       | The ad size that set in DashBoard.                                                                                                                    |
| ASPECT_FIT    | The ad is automatically adjusted to the screen width without changing the aspect ratio of the ad.                                                     |
| CUSTOM        | Can be specified to any size(pixel).<br>However, this specify is calculated based on the width.<br>Specifiable range: (DEFAULT < CUSTOM < ASPECT_FIT) |
| UNSAFE_CUSTOM | Can be specified to any size(pixel).<br>This mode ignores the size of an ad content, please be carefully to use it.                                   |

---

[TOP](/README.md#top)

---

LANGUAGE :

> [![ja](/doc/img/lang/ja.png)](/doc/ja/api/AdSize.md)

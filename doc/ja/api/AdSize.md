[TOP](/README.md#top)　>　[API](./README.md)　>　 AdSize

---

# AdSize

![support version](http://img.shields.io/badge/runa-1.0.0+-blueviolet.svg?style=flat)

[java.lang.Object](https://developer.android.com/reference/java/lang/Object.html)<br>
&nbsp;&nbsp;&nbsp;↳&nbsp;com.rakuten.android.ads.runa.AdSize

public enum class **AdSize** extends [Object](https://developer.android.com/reference/java/lang/Object.html)<br>

[AdView](./AdView.md)のサイズを定義するための enum クラス

### Public Parameters

| パラメータ名  | 詳細                                                                                                                                                                                                              |
| :------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DEFAULT       | ダッシュボードで設定した広告サイズ                                                                                                                                                                                |
| ASPECT_FIT    | デフォルトの広告サイズの比率で画面横幅に合わせたサイズ                                                                                                                                                            |
| CUSTOM        | 標準サイズが下限、画面横幅サイズを上限に任意のサイズ(px)を指定することができます。但し、この指定は広告の横幅のサイズと標準サイズの比率を基に算出されます。<br>指定可能なサイズ: (DEFAULT < `CUSTOM` < ASPECT_FIT) |
| UNSAFE_CUSTOM | 任意のサイズ(px)を指定することができます。但し、この指定は広告自体のサイズを無視するので使用の際は注意してください。                                                                                              |

---

- [API 一覧](./README.md)

- [TOP](../#top)

---

LANGUAGE :

> [![ja](/doc/img/lang/ja.png)](/doc/api/AdSize.md)

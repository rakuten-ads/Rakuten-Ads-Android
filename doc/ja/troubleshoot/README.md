[TOP](/README.md#top)　> トラブルシューティング

---

# トラブルシューティング

- [01. 広告が表示されない](#cant_display_ad)

<div class="cant_display_ad" />

## 01. 広告が表示されない

**もし `AdStateListener$onLoadSuccess`がコールバックされても広告が表示されない場合、以下を試してください。**<br>**GoogleChrome または WebView が古い場合、広告が表示されない場合がございます。**

エミュレータまたはデバイスにインストールされている[`Google Chrome`](https://play.google.com/store/apps/details?id=com.android.chrome)のバージョンを確認し、もし古ければ最新にアップデートしてください。

|                 アップデート前                 |                 アップデート後                 |
| :--------------------------------------------: | :--------------------------------------------: |
| <img src="./01/chrome/01.png" width="300px" /> | <img src="./01/chrome/02.png" width="300px" /> |

<br>

エミュレータまたはデバイスにインストールされている[`Android System WebView`](https://play.google.com/store/apps/details?id=com.google.android.webview)のバージョンを確認し、もし古ければ最新版にアップデートしてください。

|                  Before update                  |                  After update                   |
| :---------------------------------------------: | :---------------------------------------------: |
| <img src="./01/webview/01.png" width="300px" /> | <img src="./01/webview/02.png" width="300px" /> |

また、下記のような状態または操作を行うと Chrome や WebView のバージョンが初期状態になってしまう可能性があります。

- 購入した状態
- リセット
- OS クリーンアップ

---

[TOP](/README.md#top)

---

LANGUAGE :

> [![en](/doc/img/lang/en.png)](/doc/troubleshoot/README.md)

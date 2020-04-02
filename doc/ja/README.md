<div id="top"></div>

[![Platform](http://img.shields.io/badge/platform-Android-brightgreen.svg?style=flat)](https://developer.android.com)
[![Android](http://img.shields.io/badge/support-API_Level_15+-blue.svg?style=flat)](https://developer.android.com)

# Rakuten Unified Ads (RUNA) SDK Android

### 広告フォーマット

* **[バナー広告](./bannerads/README.md)**
* **[App to App](./a2a/README.md)**

---
# はじめに

<div id="prerequisites"></div>

## 前提

* Android Studio 1.0 以上
* Android API level 15 以上


<div id="import_sdk"></div>

## RUNA SDKのインポート

Gradleの依存設定でアプリにインポートすることが出来ます。プロジェクト直下の`build.gradle`のrepositoriesに以下のように参照先を追加する必要があります。

**プロジェクト全体のbuild.gradle サンプル**

```groovy
allprojects {
    repositories {
        jcenter()
        maven {
            url 'https://github.com/rakuten-ads/Rakuten-Ads-Android/raw/master/maven'
        }
    }
}
```

次に、アプリ直下の`build.gradle`の`dependencies`に以下の指定を追加します。

```groovy
  implementation 'com.rakuten.android.ads:runa:0.2.1'
```

---
[Public API](./api/README.md)

[Javadoc](https://rakuten-ads.github.io/products/android/javadoc/index.html)

---
LANGUAGE :
> [![en](../lang/en.png)](/README.md#top)

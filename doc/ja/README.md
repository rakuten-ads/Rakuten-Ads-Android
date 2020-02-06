<div id="top"></div>

[![Platform](http://img.shields.io/badge/platform-Android-brightgreen.svg?style=flat)](https://developer.android.com)
[![Android](http://img.shields.io/badge/support-API_Level_15+-blue.svg?style=flat)](https://developer.android.com)

# RakutenPublisherService Android SDK

### 広告フォーマット

* **[バナー広告](./bannerads/README.md)**

---
# はじめに

<div id="prerequisites"></div>

## 前提

* Android Studio 1.0 以上
* Android API level 15 以上


<div id="import_sdk"></div>

## RDN Ads SDKのインポート

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
  implementation 'com.rakuten.android.ads:rps:0.1.3'
```

## Proguardの設定

以下の内容をProguard設定に追加ください。
```
# Rakuten Ads Android
-dontwarn com.rakuten.android.ads.**
-keep class com.rakuten.android.ads.** { *; }
-keep class rakutenads.** { *; }
-keep class com.google.android.gms.ads.identifier.* { *; }
```

---
[Public API](./api/README.md)

[Javadoc](https://rakuten-ads.github.io/products/android/javadoc/index.html)

---
LANGUAGE :
> [![en](../lang/en.png)](/README.md#top)

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
  implementation 'com.rakuten.android.ads:runa:1.2.0'
```

## 依存関係

本SDKでは以下のライブラリを使用しています。

* com.google.code.gson:gson:2.8.2
* com.google.android.gms:play-services-ads-identifier:17.0.0

## ビルド環境

Gradle build toolsは3.5.0以上をご利用ください。

* com.android.tools.build:gradle:3.5.0+

> ※ 既にご利用され重複する場合には[`exclude`](https://docs.gradle.org/current/javadoc/org/gradle/api/artifacts/ModuleDependency.html#exclude-java.util.Map-)で除外してください。

## 実装

* **[バナー広告](./bannerads/README.md)**
* **[App to App](./a2a/README.md)**


---
[Public API](./api/README.md)

[Javadoc](https://rakuten-ads.github.io/products/runa/android/javadoc/index.html)

[トラブルシューティング](./troubleshoot/README.md)

---
LANGUAGE :
> [![en](../lang/en.png)](/README.md#top)

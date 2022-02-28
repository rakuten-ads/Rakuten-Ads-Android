<div id="top"></div>

[![Platform](http://img.shields.io/badge/platform-Android-brightgreen.svg?style=flat)](https://developer.android.com)
[![Android](http://img.shields.io/badge/support-API_Level_15+-blue.svg?style=flat)](https://developer.android.com)

# Rakuten Unified Ads (RUNA) SDK Android

### 広告フォーマット

* **[バナー広告](./bannerads/README.md)**

---
# はじめに

<div id="prerequisites"></div>

## 1. 前提

* Android Studio 1.0 以上
* Android API level 21 以上
* Gradle build tools 3.5.0 以上<br>-> `com.android.tools.build:gradle:{3.5.0以上}`


<div id="import_sdk"></div>

## 2. RUNA SDKのインポート

Gradleの依存設定でアプリにインポートすることが出来ます。プロジェクト直下の`build.gradle`のrepositoriesに以下のように参照先を追加する必要があります。

### 2.1 プロジェクト全体のbuild.gradle サンプル

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
  implementation 'com.rakuten.android.ads:runa:1.4.2'
```

> * [v1.4.0未満からのマイグレーション](./migration/README.md)

### 2.2 SDKの起動

Application継承クラスのonCreate内で以下の処理を実行してください。

```kotlin
Runa.init(this)
```

## 3. 依存関係

本SDKでは以下のライブラリを使用しています。

* com.google.code.gson:gson:2.8.2
* com.google.android.gms:play-services-ads-identifier:17.0.0

<details>
<summary>これらのライブラリを除外する場合</summary>

既に同ライブラリを利用している場合、以下の記述で除外し競合を回避することが出来ます。<br>

```
implementation("com.rakuten.android.ads:runa:X.X.X") {
    exclude group: "com.google.android.gms", module: "play-services-ads-identifier"
    exclude group: "com.google.code.gson", module: "gson"
}
```
> * X.X.X : お使いのバージョン
>
> * ※ 既にご利用され重複する場合には[`exclude`](https://docs.gradle.org/current/javadoc/org/gradle/api/artifacts/ModuleDependency.html#exclude-java.util.Map-)で除外してください。

</details>

## 4. ビルド環境

本SDKは以下の条件でビルドしています。

* Kotlin version 1.3.72
* OpenJDK version 11.0.8

## 5. 実装

* **[バナー広告](./bannerads/README.md)**
* **[ビューアブルインプレッションの計測](./viewability/README.md)**

---

[Sample App Project](https://github.com/rakuten-ads/Rakuten-Ads-Android-Sample)

[Public API](./api/README.md)

[Javadoc](https://rakuten-ads.github.io/products/runa/android/javadoc/index.html)

[トラブルシューティング](./troubleshoot/README.md)

---
LANGUAGE :
> [![en](../lang/en.png)](/README.md#top)

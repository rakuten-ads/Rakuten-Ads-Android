<div id="top"></div>

[![Platform](http://img.shields.io/badge/platform-Android-brightgreen.svg?style=flat)](https://developer.android.com)
[![Android](http://img.shields.io/badge/support-API_Level_15+-blue.svg?style=flat)](https://developer.android.com)

# Rakuten Unified Ads (RUNA) SDK Android

* [広告フォーマット](#ad-formats)
* [1. 前提](#1-prerequisites)
* [2. RUNA SDK のインポート](#2-import-the-runa-sdk)
    * [2.1 プロジェクト全体の build.gradle サンプル](#21-example-project-level-buildgradle)
    * [2.2 SDK の起動](#22-launch-sdk)
    * [2.3 実装](#23-implementation)
* [3. 依存関係](#3-dependencies)
* [4. ビルド環境](#4-build-env-requirement)
* [5. 実装](#5-implementation)

### [広告フォーマット](#ad-formats)

- **[バナー広告](./bannerads/README.md)**
- **[カルーセル広告](./carouselads/README.md)**
- **[インタースティシャル広告](./interstitialads/README.md)**

---

# はじめに

<div id="prerequisites"></div>

## [1. 前提](#1-prerequisites)

- Android Studio 1.0 以上
- Android API level 21 以上
- Gradle build tools 3.5.0 以上<br>-> `com.android.tools.build:gradle:{3.5.0以上}`

<div id="import_sdk"></div>

## [2. RUNA SDK のインポート](#2-import-the-runa-sdk)

Gradle の依存設定でアプリにインポートすることが出来ます。プロジェクト直下の`build.gradle`の repositories に以下のように参照先を追加する必要があります。

### [2.1 プロジェクト全体の build.gradle サンプル](#21-example-project-level-buildgradle)

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

最新の Runa バージョン :

```groovy
  implementation 'com.rakuten.android.ads:runa:1.11.1'
```

> - [v1.4.0 未満からのマイグレーション](./migration/README.md)

### [2.2 SDK の起動](#22-launch-sdk)

Application 継承クラスの onCreate 内で以下の処理を実行してください。

```kotlin
Runa.init(this)
```

<details>
<summary>Sample</summary>

```kotlin
class Application : Application() {

    override fun onCreate() {
        super.onCreate()
        Runa.init(this)
    }
}
```

</details>

### [2.3 実装](#23-implementation)

- [バナー広告](./bannerads/README.md)

## [3. 依存関係](#3-dependencies)

本 SDK では以下のライブラリを使用しています。

- com.google.code.gson:gson:2.8.2
- com.google.android.gms:play-services-ads-identifier:17.1.0

<details>
<summary>これらのライブラリを除外する場合</summary>

既に同ライブラリを利用している場合、以下の記述で除外し競合を回避することが出来ます。<br>

```
implementation("com.rakuten.android.ads:runa:X.X.X") {
    exclude group: "com.google.android.gms", module: "play-services-ads-identifier"
    exclude group: "com.google.code.gson", module: "gson"
}
```

> - X.X.X : お使いのバージョン
>
> - ※ 既にご利用され重複する場合には[`exclude`](https://docs.gradle.org/current/javadoc/org/gradle/api/artifacts/ModuleDependency.html#exclude-java.util.Map-)で除外してください。

</details>

## [4. ビルド環境](#4-build-env-requirement)

本 SDK は以下の条件でビルドしています。

- Kotlin version : 1.4.32
- OpenJDK version : 11.0.8
- Gradle version : 7.2

## [5. 実装](#5-implementation)

- **[バナー広告](./bannerads/README.md)**
- **[カルーセル広告](./carouselads/README.md)**
- **[ビューアブルインプレッションの計測](./viewability/README.md)**

---

[Sample App Project](https://github.com/rakuten-ads/Rakuten-Ads-Android-Sample)

[Public API](./api/README.md)

[Kdoc](https://rakuten-ads.github.io/products/runa/android/kdoc/index.html)

[トラブルシューティング](./troubleshoot/README.md)

---

LANGUAGE :

> [![en](/doc/img/lang/en.png)](/README.md#top)

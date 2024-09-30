<div id="top"></div>

[![Platform](http://img.shields.io/badge/platform-Android-brightgreen.svg?style=flat)](https://developer.android.com)
[![Android](http://img.shields.io/badge/support-API_Level_15+-blue.svg?style=flat)](https://developer.android.com)

# Rakuten Unified Ads (RUNA) SDK Android
* [Ad Formats](#ad-formats)
* [1. Prerequisites](#1-prerequisites)
* [2. Import the RUNA SDK](#2-import-the-runa-sdk)
    * [2.1 Example project-level build.gradle](#21-example-project-level-buildgradle)
    * [2.2 Launch SDK](#22-launch-sdk)
    * [2.3 Implementation](#23-implementation)
* [3. Dependencies](#3-dependencies)
* [4. Build env requirement](#4-build-env-requirement)
* [5. Implementation](#5-implementation)

### [Ad Formats](#ad-formats)

- **[BannerAds](./doc/bannerads/README.md)**
- **[CarouselAds](./doc/carouselads/README.md)**
- **[InterstitialAds](./doc/interstitialads/README.md)**

---

# Get Started

<div id="prerequisites"></div>

## [1. Prerequisites](#1-prerequisites)

- Uses Android Studio 1.0 or higher
- Target Android API level 21 or higher
- Uses version 3.5.0 or higher for Gradle build tools.<br>`com.android.tools.build:gradle:{3.5.0+}`

<div id="import_sdk"></div>

## [2. Import the RUNA SDK](#2-import-the-runa-sdk)

Apps can import the RDN Mobile Ads SDK with a Gradle dependency.In order to use that repository, you need to reference it in the app's project-level `build.gradle` file. Open yours and look for an allprojects section:

### [2.1 Example project-level build.gradle](#21-example-project-level-buildgradle)

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

Next, open the app-level `build.gradle` file for your app, and look for a "dependencies" section.

Latest Runa version :

```groovy
  implementation 'com.rakuten.android.ads:runa:1.12.2'
```

- [Migration to v1.4.0+](./doc/migration/README.md)

### [2.2 Launch SDK](#22-launch-sdk)

In the onCreate method of the class that inherits Application, execute as follows and launch the SDK.

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

### [2.3 Implementation](#23-implementation)

- [Banner Ads](./doc/bannerads/README.md)

## [3. Dependencies](#3-dependencies)

This SDK depends on the following libraries:

- com.google.code.gson:gson:2.8.2
- com.google.android.gms:play-services-ads-identifier:17.1.0

<details>
<summary>In case of exclude these libraries.</summary>

If you are already using these libraries, you can exclude them in the following ways to avoid conflicts:

```
implementation("com.rakuten.android.ads:runa:X.X.X") {
    exclude group: "com.google.android.gms", module: "play-services-ads-identifier"
    exclude group: "com.google.code.gson", module: "gson"
}
```

> X.X.X : Using version.
>
> ※ Exclude it with [`exclude`](https://docs.gradle.org/current/javadoc/org/gradle/api/artifacts/ModuleDependency.html#exclude-java.util.Map-) if it is already used and duplicated.

</details>

## [4. Build env requirement](#4-build-env-requirement)

Thid SDK is built by below tools.

- Kotlin version : 1.9.25
- OpenJDK version : 17.0.12
- Gradle version : 8.9

## [5. Implementation](#5-implementation)

- **[Banner ads](./doc/bannerads/README.md)**
- **[CarouselAds](./doc/carouselads/README.md)**
- **[Viewability measurement](./doc/viewability/README.md)**

---

[Sample App Project](https://github.com/rakuten-ads/Rakuten-Ads-Android-Sample)

[Public API](./doc/api/README.md)

[Kdoc](https://rakuten-ads.github.io/products/runa/android/kdoc/index.html)

[Troubleshooting](./doc/troubleshoot/README.md)

---

LANGUAGE :

> [![jp](./doc/img/lang/ja.png)](./doc/ja)

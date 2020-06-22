<div id="top"></div>

[![Platform](http://img.shields.io/badge/platform-Android-brightgreen.svg?style=flat)](https://developer.android.com)
[![Android](http://img.shields.io/badge/support-API_Level_15+-blue.svg?style=flat)](https://developer.android.com)

# Rakuten Unified Ads (RUNA) SDK Android

### Ad Formats

* **[Banner](./doc/bannerads/README.md)**
* **[App to App](./doc/a2a/README.md)**

---
# Get Started

<div id="prerequisites"></div>

## Prerequisites

* Use Android Studio 1.0 or higher
* Target Android API level 15 or higher


<div id="import_sdk"></div>

## Import the RUNA SDK

Apps can import the RDN Mobile Ads SDK with a Gradle dependency.In order to use that repository, you need to reference it in the app's project-level `build.gradle` file. Open yours and look for an allprojects section:

**Example project-level build.gradle**

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

```groovy
  implementation 'com.rakuten.android.ads:runa:1.0.0'
```

## Dependencies

This SDK depends on the following libraries:

* com.google.code.gson:gson:2.8.2
* com.google.android.gms:play-services-ads-identifier:17.0.0

> ※ Exclude it with [`exclude`](https://docs.gradle.org/current/javadoc/org/gradle/api/artifacts/ModuleDependency.html#exclude-java.util.Map-) if it is already used and duplicated.

---

[Public API](./doc/api/README.md)

[Javadoc](https://rakuten-ads.github.io/products/android/javadoc/index.html)

---
LANGUAGE :
> [![jp](./doc/lang/ja.png)](./doc/ja)

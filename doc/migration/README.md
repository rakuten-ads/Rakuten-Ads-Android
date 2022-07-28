[TOP](/README.md#top)　>　Migration

# Migration

## 1. About migration to v1.4.0

When migrating from a version lower than v1.4.0 to v1.4.0 or above, the following new steps are required.

### 1.1 Launch Runa SDK

In the onCreate method of the class that inherits [`Application`](https://developer.android.com/reference/android/app/Application), implement as follows and launch the SDK.

```kotlin
class SampleApplication : Application() {
    override fun onCreate() {

        // Launch SDK
        Runa.init(this).also {
            // For output debug log according to status
            it.debug = BuildConfig.DEBUG
        }

    }
...
```

<br>

### 1.2 Precautions for specifying the size in the definition in XML layout.

* If AdView is placed directly under [ConstraintLayout](https://developer.android.com/reference/androidx/constraintlayout/widget/ConstraintLayout) and AspectFit is specified for `adSpotSize`, the margin specification will not work.<br> Therefore, if wrap_content is defined for layout_width, specify match_content.

```
<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:clipToPadding="false"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintTop_toTopOf="parent">

    <com.rakuten.android.ads.runa.AdView
        android:id="@+id/adView"
        android:layout_width="match_parent" <------ wrap_content to match_parent
        android:layout_height="wrap_content"
        android:layout_marginLeft="8dp"
        android:layout_marginStart="8dp"
        android:layout_marginRight="8dp"
        android:layout_marginEnd="8dp"
        app:adSpotId="XXX"
        app:adSpotSize="AspectFit"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```



---
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/img/lang/ja.png)](/doc/ja/migration/README.md)

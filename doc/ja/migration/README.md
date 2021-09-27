[TOP](/README.md#top)　>　マイグレーション

# マイグレーション

## 1. v1.4.0へのマイグレーション

v1.4.0未満のバージョンからv1.4.0以降に移行する場合は、新たに以下の手順が必要となります。

### 1.1 SDKの起動

[`Application`](https://developer.android.com/reference/android/app/Application)を継承させたクラスのonCreateメソッド内で以下の通り実装、SDKを起動します。

```kotlin
class SampleApplication : Application() {
    override fun onCreate() {

        // Runaの起動
        Runa.init(this).also {
            // デバッグステータスに合わせてデバッグログを出力
            it.debug = BuildConfig.DEBUG
        }

    }
...
```

<br>

### 1.2 XMLレイアウトにおける定義でのサイズ指定の注意

* [ConstraintLayout](https://developer.android.com/reference/androidx/constraintlayout/widget/ConstraintLayout)の直下にAdViewを配置し`adSpotSize`にAspectFitを指定している場合、マージン指定が効かなくなります。そのためlayout_widthにwrap_contentを入れている場合はmatch_contentを指定してください。

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
[TOP](../#top)

---
LANGUAGE :
> [![en](/doc/lang/en.png)](/doc/migration/README.md)

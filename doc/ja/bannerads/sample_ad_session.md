[TOP](../#top)　>　[バナー広告](./README.md)　>　RunaAdSession Sample

---

# RunaAdSession サンプル

## 1. `RecyclerView.Adapter`内での使い方の例

```kotlin
class RecyclerViewAdapter(
    private val data: Array<MultipleBannerViewingData>
) : RecyclerView.Adapter<RecyclerView.ViewHolder>() {

  private val adViewSession = RunaAdSession()      // <------------- [ Definition ]

  override fun getItemCount(): Int = data.size

  override fun getItemViewType(position: Int): Int = data[position].type.value

  override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): RecyclerView.ViewHolder {
      fun inflateView(@LayoutRes layoutRes: Int) =
          LayoutInflater.from(parent.context).inflate(layoutRes, parent, false)
      return if (viewType == TYPE_ADVIEW) {
          AdViewHolder(inflateView(R.layout.list_row_adview))
      } else {
          ContentViewHolder(inflateView(R.layout.list_row_content))
      }
  }

  override fun onBindViewHolder(holder: RecyclerView.ViewHolder, position: Int) {
      when (holder) {
          is ContentViewHolder -> holder.bind(data[position].content)
          is AdViewHolder -> holder.bind(data[position].adViewData)
      }
  }

  open class ContentViewHolder(v: View) : RecyclerView.ViewHolder(v) {
      val binding: ListRowContentBinding? = DataBindingUtil.bind(v)
      fun bind(data: ContentRow?) {
          data?.let {
              binding?.contentName?.text = it.name
              Picasso.get()
                  .load(it.url)
                  .into(binding?.contentImg)
          }
      }
  }

  inner class AdViewHolder(v: View) : RecyclerView.ViewHolder(v) {
      val binding: ListRowAdviewBinding? = DataBindingUtil.bind(v)

      fun bind(data: AdViewData?) {
          if (data == null) return
            binding?.let { binding ->
                adViewSession.bind(binding.adview)      // <------------- [ bind adView ]
                binding.adview.show()
            }
      }
  }      

  companion object {
      const val TYPE_NORMAL = 0
      const val TYPE_ADVIEW = 1
  }

}

data class MultipleBannerViewingData(
    val type: ContentType,
    // Sample Content
    val content: ContentRow? = null,
    // AdView
    val adViewData: AdViewData? = null
) : Serializable

enum class ContentType(val value: Int) {
    CONTENT(0), ADVIEW(1)
}
```
**R.layout.list_row_adview**
```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto">

    <FrameLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

        <com.rakuten.android.ads.runa.AdView
                android:id="@+id/adview"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="10dp"
                android:layout_marginBottom="10dp"
                android:layout_gravity="center"
                app:adSpotId="194"
                app:adSpotSize="Default" />

        <TextView
            android:id="@+id/error_info"
            android:layout_width="match_parent"
            android:layout_height="100dp"
            android:visibility="gone"
            android:layout_gravity="center"
            android:gravity="center"
            android:textSize="20sp"
            android:textStyle="bold"
            />
    </FrameLayout>
</layout>
```

**R.layout.list_row_content**
```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android">

    <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="100dp"
            android:gravity="center_vertical"
            android:orientation="horizontal"
            android:padding="8dp">

        <TextView
                android:id="@+id/content_name"
                android:layout_width="150dp"
                android:layout_height="wrap_content"
                android:gravity="left|center_vertical" />

        <ImageView
                android:id="@+id/content_img"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_marginStart="10dp"
                android:layout_marginLeft="10dp" />
    </LinearLayout>
</layout>
```


---
[バナー広告](./README.md)

[TOP](../#top)

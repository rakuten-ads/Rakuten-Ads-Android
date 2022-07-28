[TOP](/README.md#top)　>　The Visibility Measurement

---

# The Visibility Measurement for Search Ads

This function can measure the visibility of any target View and call back after the visibility is established.
<br>

> ※ The use of this API is for apps that can use the Rakuten Ichiba search API.

<br>

## Visibility monitoring for a View

Use `ViewabilityProvider` to monitor the visibility of the View.

### Registration of the View to monitor

To start monitoring the View, use the `register` method.<br>
This method takes a URL and the target View as arguments.

`ViewabilityProvider$register(view: View, url: String, callback: ViewabilityListener)`

> Method `register` requires the following arguments.<br>
>
> * `view` (required) : Target view
> * `url` (required) : An url to send the results
> * `callback` (optional) : Called after submitting the result. A callback if needed.


The following is an implementation example.


```java

val sampleTargetView = findViewById<LinearLayout>(R.id.sampleTarget)

ViewabilityProvider.register(sampleTargetView, "URL", object: ViewabilityListener {

  override fun onEstablished() {
      // Transmission completed
  }
})
```

> ※ It is desirable to execute `register` after the drawing of the target View is completed.
>
> ※ After `onEstablished` is called, it implicitly unregisters, so you don't have to manually call `'unregister'`.

<br>

## Stop monitoring View visibility

If you want to stop while monitoring, use the `unregister` method.

`ViewabilityProvider$unregister(view: View)`

> Method `unregister` requires the following arguments.<br>
>
> * `view` (required) : Target view

```java
val sampleTargetView = findViewById<LinearLayout>(R.id.sampleTarget)

ViewabilityProvider.unregister(sampleTargetView)

```

<br><br><br><br><br>

---
[TOP](/README.md#top)

---
LANGUAGE :
> [![ja](/doc/img/lang/ja.png)](/doc/ja/viewability/README.md)

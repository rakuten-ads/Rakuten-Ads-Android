[TOP](/README.md#top)　>　 The Visibility Measurement

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
> - `view` (required) : Target view
> - `url` (required) : An url to send the results
> - `callback` (optional) : Called after submitting the result. A callback if needed.

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
> - `view` (required) : Target view

```java
val sampleTargetView = findViewById<LinearLayout>(R.id.sampleTarget)

ViewabilityProvider.unregister(sampleTargetView)

```

### Enable Open Measurement SDK

Viewable module supports Open Measurement SDK. <br>
You can utilize `OpenMeasurementNativeClient` and execute following methods depending on your use cases.

| Method               | Description                                                                                                                                                                                                                            |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| start()              | Create OM SDK session. Starting the session does not trigger an impression yet – it only prepares the session for tracking. It is important to start the session before dispatching any events.                                        |
| loadedAd()           | Ideally this would occur as early in your ad session as the creative is loaded, but it is ok to send it just before the impression.                                                                                                    |
| impressionOccurred() | The definition of an impression is generally accepted to be on ad render so this is likely when you will want to dispatch the event. The event should be dispatched only once and attempting to trigger it multiple times is an error. |
| finish()             | Stop the session when the impression has completed and the ad will be destroyed. Note, that after you’ve stopped the session it is an error to attempt to start it again or trigger an impression on the finished session.             |

```java

val sampleTargetView = findViewById<LinearLayout>(R.id.sampleTarget)

ViewabilityProvider.register(sampleTargetView, "URL", object: ViewabilityListener {

  override fun onEstablished() {
      // Transmission completed
  }
})

// Enbale OM SDK
val omParams = OmNativeParameter(
    "iabtechlab.com-omid",
    URL("https://s3-us-west-2.amazonaws.com/updated-omsdk-files/compliance-js/omid-validation-verification-script-v1-RAKUTEN-03142023.js"),
    "iabtechlab-Rakuten",
    URL("https://storage.googleapis.com/rssp-dev-cdn/sdk/js/omsdk-v1-1.4.3.js")
)
val omClient = OpenMeasurementNativeClient(sampleTargetView, omParams)
omClient.start()
```

<br><br><br><br><br>

---

[TOP](/README.md#top)

---

LANGUAGE :

> [![ja](/doc/img/lang/ja.png)](/doc/ja/viewability/README.md)

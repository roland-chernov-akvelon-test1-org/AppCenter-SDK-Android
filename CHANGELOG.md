# App Center SDK for Android Change Log

## Version 1.11.1 (Under active development)

### AppCenterAnalytics

* **[Fix]** Extend the current session instead of starting a new session when sending events from the background. Sessions are also no longer started in background by sending an event or a log from another service such as push, as a consequence the push registration information will be missing from crash events information.

### AppCenterDistribute

* **[Fix]** Fix issue with forcing Chrome to open links when other browsers are the default.

___

## Version 1.11.0

### AppCenter

* **[Feature]** Allow users to set userId that applies to crashes, error and push logs. This feature adds an API, but is not yet supported on the App Center backend.
* **[Fix]** Do not delete old logs when trying to add a log larger than the maximum storage capacity.
* **[Fix]** Fix error detection of `setMaxStorageSize` API if database uses custom page size.
* **[Fix]** Fix minimum storage size verification to match minimum possible value.
* **[Fix]** Fix disabling logging of network state changes according to `AppCenter.getLogLevel`.
* **[Fix]** Fix logs duplication on unstable network.

### AppCenterCrashes

* **[Fix]** Fix a bug where crash data file could leak when the database is full.

### AppCenterPush

* **[Fix]** Fix push foreground listener after re-enabling push service.

___

## Version 1.10.0

### AppCenterAnalytics

* **[Feature]** Add API to specify event persistence priority.

### AppCenterCrashes

* **[Fix]** Preventing stack overflow crash while reading a huge throwable file.

___

## Version 1.9.0

### AppCenter

* **[Feature]** Add a `setMaxStorageSize` API which allows setting a maximum size limit on the local SQLite storage. Previously, up to 300 logs were stored of any size. The default value is 10MB.
* **[Security]** To enforce TLS 1.2 on all HTTPS connections the SDK makes, we are dropping support for API level 15 (which supports only TLS 1.0), the minimum SDK version thus becomes 16. Previous versions of the SDK were already using TLS 1.2 on API level 16+.
* **[Bug fix]** Fix validating and discarding `NaN` and infinite double values when calling `setCustomProperties`.

### AppCenterAnalytics

* **[Feature]** Add `pause`/`resume` APIs which pause/resume sending Analytics logs to App Center.
* **[Feature]** Add support for typed properties. Note that these APIs still convert properties back to strings on the App Center backend. More work is needed to store and display typed properties in the App Center portal. Using the new APIs now will enable future scenarios, but for now the behavior will be the same as it is for current event properties.
* **[Feature]** Preparation work for a future change in transmission protocol and endpoint for Analytics data. There is no impact on your current workflow when using App Center.

___

## Version 1.8.0

### AppCenterCrashes

* **[Fix]** Fix a bug where some initialize operations were executed twice.
* **[Fix]** Fix a bug where device information could be null when reading the error report client side.

### AppCenterDistribute

* **[Fix]** Fix a crash that could happen when starting the application.

### AppCenterAnalytics

* **[Feature]** Preparation work for a future change in transmission protocol and endpoint for Analytics data. There is no impact on your current workflow when using App Center.

___

## Version 1.7.0

### AppCenterAnalytics

- **[Feature]** Preparation work for a future change in transmission protocol and endpoint for Analytics data. There is no impact on your current workflow when using App Center.

### AppCenterPush

The Firebase messaging SDK is now a dependency of the App Center Push SDK to be able to support Android P and also prevent features to break after April 2019 based on [this announcement](https://firebase.googleblog.com/2018/04/time-to-upgrade-from-gcm-to-fcm.html).

You need to follow [some migration steps](https://docs.microsoft.com/en-us/appcenter/sdk/push/migration/android) after updating the SDK to actually use Firebase instead of the manual registration mechanism that we are providing. The non Firebase mechanism still works after updating the SDK but you will see a deprecation message, but this will not work on Android P devices until you migrate.

After updating the app to use Firebase, you will also no longer see duplicate notifications when uninstalling and reinstalling the app on the same device and user.

___

## Version 1.6.1

### AppCenter

- **[Feature]** Preparation work for a future change in transmission protocol and endpoint for Analytics data. There is no impact on your current workflow when using App Center.
- **[Improvement]** Enable TLS 1.2 on API levels where it's supported but not enabled by default (API level 16-19, this became a default starting API level 20). Please note we still support Android API level 15 and it uses TLS 1.0.
- **[Improvement]** Gzip is used over HTTPS when request size is larger than 1.4KB.
- **[Fix]** Fix a crash when disabling a module at the same time logs are sent.
- **[Fix]** Fix pretty print JSON in Android P when verbose logging is enabled.

### AppCenterCrashes

- **[Feature]** Enable reporting C/C++ crashes when [Google Breakpad](https://github.com/google/breakpad) is used in the application (Google Breakpad is not distributed by App Center). Please note that there is still work to be done to stabilize this feature in App Center. Stay tuned with our [Changelog](https://docs.microsoft.com/en-us/appcenter/general/changelog) to get updates on NDK crashes support.

___

## Version 1.5.1

### AppCenter

* **[Fix]** Fix a crash when network state changes at same time as SDK initializing.
* **[Fix]** Fix crashes when trying to detect we run on instrumented test environment.
* **[Fix]** Fix a deadlock when setting wrapper SDK information or setting log url while other channel operations performed such as when Crashes is starting.

### AppCenterCrashes

* **[Fix]** Fix reporting crash when process name cannot be determined.

### AppCenterPush

* **[Fix]** Fix notification text being truncated when large and now supports multi-line.

___

## Version 1.5.0

### AppCenterAnalytics

* **[Improvement]** Analytics now allows a maximum of 20 properties by event, each property key and value length can be up to 125 characters long.

### AppCenterPush

* **[Feature]** Configure default notification icon and color using meta-data.
* **[Fix]** Fixes the google.ttl field being considered custom data.
* **[Fix]** Fixes push notification not displayed if Google Play Services too old on the device.
* **[Fix]** Don't crash the application when invalid notification color is pushed.

___

## Version 1.4.0

### AppCenterDistribute

* **[Feature]** Add Session statistics for distribution group.

___

## Version 1.3.0

### AppCenterDistribute

* **[Feature]** Use tester app to enable in-app updates if it's installed.
* **[Feature]** Add reporting of downloads for in-app update.
* **[Improvement]** Add distribution group to all logs that are sent.

___

## Version 1.2.0

### AppCenter

* **[Fix]** Fix events association with crashes.
* **[Fix]** Fix network state detection.
* **[Fix]** Don't retry sending logs on HTTP error 429.
* **[Fix]** Some logs were not sent or discarded correctly on AppCenter enabled/disabled state changes.

### AppCenterCrashes

* **[Improvement]** Increase attachment file size limit from 1.5MB to 7MB.

### AppCenterPush

* **[Fix]** Fix a crash on Android 8.0 (exact version, this does not happen in 8.1) where having an adaptive icon (like launcher icon) would cause crash of the entire system U.I. on push. On Android 8.0 we replace the adaptive icon by a placeholder icon (1 black pixel) to avoid the crash, starting Android 8.1 the adaptive icon is displayed without fallback.

___

## Version 1.1.0

### AppCenter

* **[Feature]** SDK modules can be skipped from being started automatically without code modification during instrumented tests. The SDK now reads `APP_CENTER_DISABLE` variable from `InstrumentationRegistry.getArguments()` and will not start any module if the value is `All` or will just skip starting the services described by a **comma separated list** of the services to exclude from being started. Valid service names for the variable are `Analytics`, `Crashes`, `Distribute` or `Push`. The modules are always started if instrumentation context is not available (like when you build and launch your application normally).

### AppCenterCrashes

* **[Fix]** Fix a crash when sending an attachment larger than 1.4MB. The SDK is still unable to send large attachments in this release but now it does not crash anymore. An error log is printed instead.
* **[Improvement]** Allow wrapper SDKs such as Xamarin to report a managed exception (for example for .NET stack traces) while still saving the exception for client side report as Java Throwable (so the original exception can be read from client side after restart by using the SDK).

### AppCenterDistribute

* **[Improvement]** Updated translations.
* **[Improvement]** Users with app versions that still use Mobile Center can directly upgrade to versions that use this version of App Center, without the need to reinstall.

### AppCenterPush

* **[Improvement]** The Firebase SDK dependency is now optional. If Firebase SDK is not available at runtime, the push registers and generate notifications using only App Center SDK. The Firebase application and servers are still used whether the Firebase SDK is installed into the application or not.

  * The SDK is still compatible with `apply plugin: 'com.google.gms.google-services'` and `google-services.json`, but if you don't use Firebase besides App Center, you can replace that plugin and the json file by a call to `Push.setSenderId` before `AppCenter.start`. The **Sender ID** can be found on the **Cloud Messaging** tab of your Firebase console project settings (same place as the **Server Key**).
  * The SDK is still compatible with `"com.google.firebase:firebase-messaging:$version"` lines. But if you don't use Firebase besides App Center, you can now remove these dependencies.

___

## Version 1.0.0

### General Availability (GA) Announcement.

This version contains **breaking changes** due to the renaming from Mobile Center to App Center. In the unlikely event there was data on the device not sent prior to the update, that data will be discarded.

### AppCenter

* The SDK has been rebranded from Mobile Center to App Center. Please follow [the migration guide](https://review.docs.microsoft.com/en-us/appcenter/sdk/sdk-migration/android?branch=appcenter-ga) to update from an earlier version of Mobile Center SDK.

### AppCenterDistribute

* **[Fix]** The view release notes button was not correctly hidden when no release notes were available.
* **[Fix]** Added missing translations for failed to enable in-app update dialog title and buttons. The main message however is not localized yet as it's extracted from a REST API text response.
* **[Known issue]** When updating an application that uses Mobile Center SDK using the in-app update dialog to an application version that uses AppCenter SDK version, the browser will be re-opened and will fail. User will need to re-install the application from the App Center portal.

___

## Version 0.13.0

* Localize in-app update texts, see [this folder](https://github.com/Microsoft/mobile-center-sdk-android/tree/develop/sdk/mobile-center-distribute/src/main/res) for a list of supported languages.
* When in-app updates are disabled because of side-loading, a new dialog will inform user instead of being stuck on a web page. Dialog actions offer ignoring in-app updates or following a link to re-install from the portal. This new dialog has texts that are not localized yet.
* Fix a bug where a failed version check could trigger reopening the browser in failure to enable in-app updates.
* Add `MobileCenter.getSdkVersion()` API to check Mobile Center SDK version at runtime.

___

## Version 0.12.0

- **[Feature]** New feature that allows to share your applications to anyone with public link.

- **[MISC]** When you update to this release, there will be **potential data loss** if an application installed with previous versions of MobileCenter SDK on devices that has pending logs which are not sent to server yet at the time of the application is being updated.

___

## Version 0.11.2

* Truncate event name and properties automatically instead of skipping them.
* Russian localization for in-app update texts.

___

## Version 0.11.1

Fix a regression in in-app updates from [version 0.11.0](https://github.com/Microsoft/mobile-center-sdk-android/releases/tag/0.11.0) where we could show unknown sources dialog on Android 8 if targeting older versions and unknown sources enabled.

Actually in that scenario, we can't detect if unknown sources are enabled and will just skip that dialog, system dialog will be shown at install time instead.

___

## Version 0.11.0

### Strict mode

This release focuses on fixing strict mode issues (including Android 8 ones).

Since strict mode checks if you spend time reading storage on U.I. thread we had to make the following APIs asynchronous and is thus a **breaking change**:

* `{AnyClass}.isEnabled()`
* `MobileCenter.getInstallId()`
* `Crashes.hasCrashedInLastSession()`

Those APIs returns a `MobileCenterFuture` object that is used to monitor the result, you can either use `get()` or `thenAccept(MobileCenterConsumer)` to either block or get the result via callback.

For symmetry purpose, `{AnyClass}.setEnabled(boolean)` also return a `MobileCenterFuture` object but most users don't need to monitor the result of the operation (consistency of calls sequence is guaranteed even if you don't wait for the change to be persisted).

Also `Crashes.getLastSessionCrashReport` was already asynchronous but signature changed to use the new `MobileCenterFuture` object.

`MobileCenterFuture` is similar to Java 8 `CompletableFuture` but works on Java 7 on any API level and has limited number of methods and does not throw exceptions (and executes the `thenAccept` callback in the U.I. thread).

### Other changes

* Fix a bug on Android 8 where network state could be detected as disconnected while network is available.
* Fix showing unknown sources warning dialog on Distribute on Android 8.
* Update Firebase SDK dependencies in Push to 11.0.2 to avoid conflict with Firebase recent getting started instructions.
* Update internal crash code to make it more compatible with Xamarin.Android and possibly future wrapper SDKs.

___

## Version 0.10.0

* Add `MobileCenter.setCustomProperties` API to segment audiences.
* Fix push and distribute notifications on Android 8 when targeting API level 26.
* Add a new method `Push.checkLaunchedFromNotification` to use in `onNewIntent` if `launchMode` of the activity is not standard to fix push listener when clicking on background push and recycling the activity.
* Fix crashing when calling `{AnyService}.isEnabled()` / or `setEnabled` before `MobileCenter.start`, now always return false before start.
* Fix a bug where 2 sessions could be reported at once when resuming from background.

___

## Version 0.9.0

Add `getErrorAttachments` callback to CrashesListener.

___

## Version 0.8.1

Fix a memory leak in HTTP client.

___

## Version 0.8.0

* Add network state debug logs.
* Add push module relying on Firebase to push notifications to the users of your application.

___

## Version 0.7.0

This version contains bug fixes, improvements and new features.

### Analytics

* **[Misc]** Events have some validation and you will see the following in logs:

    * An error if the event name is null, empty or longer than 256 characters (event is not sent in that case).
    * A warning for invalid event properties (the event is sent but without invalid properties):

       * More than 5 properties per event (in that case we send only 5 of them and log warnings).
       * Property key null, empty or longer than 64 characters.
       * Property value null or longer than 64 characters.

### Distribute

* **[Feature]** New Distribute listener to provide an ability of in-app update customization.
* **[Feature]** New default update dialog with release notes view.
* **[Bug fix]** Fix a crash when failing to download a mandatory update while showing progress dialog.
* **[Bug fix]** Fix duplicate update dialog when a new release is detected after restarting and processing the current update.

___

## Version 0.6.1

- **[Bug fix]** Fix a crash that could happen when application going to background while progress dialog on mandatory update download was displayed.
- **[Bug fix]** Fix a bug where progress dialog could be stuck at 100%.
- **[Improvement]** Offline cache for update dialog.

___

## Version 0.6.0

- **[Feature]** New service called `Distribute` to enable in-app updates for your Mobile Center builds.
- **[Improvement]** The improvement to wait up to 5 seconds for flushing logs to storage on crash is now active even if the Crashes feature is not used.
- **[Bug fix]** `401` HTTP errors (caused by invalid `appSecret`) were retried as a recoverable error. They are now considered unrecoverable.
- **[Misc]** A new log is sent to server when `MobileCenter` is started with the list of `MobileCenter` services that are used in the application.
- **[Misc]** Renamed `setServerUrl` to `setLogUrl`.

___

## Version 0.5.0

**Breaking change**: Remove Crashes APIs related to attachments as it's not supported by backend yet.

___

## Version 0.4.0

- Most of the crash processing is now happening on a background thread when the application restarts, solving multiple strict mode policy issues.
  - As a consequence, the `getLastSessionCrashReport` is now an asynchronous function with a callback (**breaking change**).
- Fix Proguard configuration inside the main AAR file, no Proguard configuration required on application side.
- Fix a race condition crash inside HTTP channel management when counting pending logs.
- Fix other race conditions in HTTP channel management that could lead to inconsistent behavior.
- Fix crash when the default ASyncTask thread pool is saturated when sending HTTP logs (now retries later).
- `StackOverflowError` throwable object for client side inspection is now truncated to `256` frames.
- App secret is now obfuscated in logs when setting verbose log level.
- Threads where crash callbacks are executed is now documented with the support annotations and the behavior is now consistent (either always UI thread or always worker thread depending on the callback).

___

## Version 0.3.3

- Fix a bug where `CrashesListener.onBeforeSending` or `CrashesListener.onSendingFailed` could not be called.
- Truncate `StackOverFlowError` to 256 frames (128 at start and 128 at end) to allow them being reported.
- Retry more https errors due to transient ssl failures when the client or server connectivity is bad.
- On crash, wait 5 seconds for local storage to flush other pending events to disk so that they are not lost.

___

## Version 0.3.2

- Fix empty text attachment being sent along with a binary only attachment.
- Fix logs when enabling or disabling MobileCenter.
- Fix debug logs for user confirmation callbacks.
- Add possibility to add raw stack trace for Xamarin.

___

## Version 0.3.1

- Fix/improve SDK logging.
- Don't validate appSecret against UUID format anymore (server validates appSecret).
- Allow wrapper SDK such as Xamarin to store additional crash data file.

___

## Version 0.3.0

- Rename `initialize` to `configure` in `MobileCenter` methods and logs.
- Fix null pointer exception when disabling a service during an HTTP call.

___

## Version 0.2.0

- Rename Sonoma to MobileCenter.
- Fix a bug that caused crashes to be sent twice if calling Crashes.setEnabled(true) while already enabled.
- New logs in assert level for successful SDK initialization or failed to initialize.
- Allow wrapper SDKs such as Xamarin to label an exception as being generated by the wrapper SDK.

___

## Version 0.1.4

- Remove trackPage/trackException from public APIs and disable automatic page tracking.
- Add assert level logs and a new NONE constant to disable all logs included assert ones.

___

## Version 0.1.3

Refactoring to solve Xamarin bindings issues.

___

## Version 0.1.2

- start_session is sent without sending any page or event
- start_session is sent immediately if re-enabling analytics module while in foreground (only if core was enabled though)

___

## Version 0.1.1

- Calls to SQLite are now asynchronous.
- Fix corner cases in new session detection, especially for single activity applications.

___

## Version 0.1.0

First release of the Sonoma SDK for Android.

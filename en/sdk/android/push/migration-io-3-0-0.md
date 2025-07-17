# Migrating to version 3.0.0

Migrating your app from `com.yandex.android:mobmetricapushlib` to `io.appmetrica.analytics:push` shouldn't cause any issues.

## Using two versions of AppMetrica Push SDK at the same time

Since we renamed the group and main artifacts, there may be cases where the app uses two versions of AppMetrica SDK at the same time: `com.yandex.android:mobmetricapushlib` and `io.appmetrica.analytics:push`.

{% note alert %}

That could lead to anomalies in reports and isn't recommended.

{% endnote %}

## Migration guide

This guide contains examples that show the differences between SDK versions `2.3.3` and `3.0.0`.
This section only covers methods that do not have backward compatibility.

Here's how to migrate to the new version

1. Make sure you're using AppMetrica SDK version `io.appmetrica.analytics:analytics:6.0.0` or higher.
2. Change the `com.yandex.android:mobmetricapushlib:2.3.3` dependency to `io.appmetrica.analytics:push:3.0.0`.
3. In the project code, replace the classes and methods that were simply renamed or only changed their package.
   The changes you need to make are listed in the [paragraph on renaming classes](#rename_classes).
4. Temporarily comment out the code with any remaining errors to ensure the project can be built.
5. Modify any existing `exclude` rules.
   The changes you need to make are listed in the [paragraph on renaming dependencies](#rename_dep).
6. Edit the code you commented out by following the other paragraphs in this guide.
   If you have any questions, contact support.

### Renamed dependencies {#rename_dep}

* Changed the name of the `com.yandex.android:mobmetricapushlib` module to `io.appmetrica.analytics:push`.
* Changed the name of the `com.yandex.android:appmetricapush-provider-firebase` module to `io.appmetrica.analytics:push-provider-firebase`.
* Changed the name of the `com.yandex.android:appmetricapush-provider-hms` module to `io.appmetrica.analytics:push-provider-hms`.
* Changed the name of the `com.yandex.android:appmetricapush-provider-rustore` module to `io.appmetrica.analytics:push-provider-rustore`.
* Split the `com.yandex.android:appmetricapush-core` module into `io.appmetrica.analytics:push-core-utils` and `io.appmetrica.analytics:push-provider-api`.

### Renamed classes {#rename_classes}

* Renamed the `com.yandex.metrica.push.TokenUpdateListener` class as `io.appmetrica.analytics.push.TokenUpdateListener`.
* Renamed the `com.yandex.metrica.push.YandexMetricaPush` class as `io.appmetrica.analytics.push.AppMetricaPush`.
   * Changed the `EXTRA_ACTION_INFO` constant.
   * Removed the `getToken` method.
   * Changed the name of the `init` method to `activate`.
* Renamed the `com.yandex.appmetrica.push.firebase.FirebasePushServiceControllerProvider` class as `io.appmetrica.analytics.push.provider.firebase.FirebasePushServiceControllerProvider`.
* Renamed the `com.yandex.appmetrica.push.hms.HmsPushServiceControllerProvider` class as `io.appmetrica.analytics.push.provider.hms.HmsPushServiceControllerProvider`.
* Renamed the `com.yandex.appmetrica.push.hms.MetricaHmsMessagingService` class as `io.appmetrica.analytics.push.provider.hms.AppMetricaHmsMessagingService`.
* Renamed the `com.yandex.appmetrica.push.rustore.MetricaRuStoreMessagingService` class as `io.appmetrica.analytics.push.provider.rustore.AppMetricaRuStoreMessagingService`.
* Renamed the `com.yandex.appmetrica.push.rustore.RuStorePushServiceControllerProvider` class as `io.appmetrica.analytics.push.provider.rustore.RuStorePushServiceControllerProvider`.
* Renamed the `com.yandex.metrica.push.common.core.PushServiceControllerProvider` class as `io.appmetrica.analytics.push.provider.api.PushServiceControllerProvider`.
* Renamed the `com.yandex.metrica.push.common.core.PushServiceController` class as `io.appmetrica.analytics.push.provider.api.PushServiceController`.
* Renamed the `com.yandex.metrica.push.firebase.MetricaMessagingService` class as `io.appmetrica.analytics.push.provider.firebase.AppMetricaMessagingService`.

The `io.appmetrica.analytics.push.provider.firebase.AppMetricaMessagingService` class is moved to a separate [dependency](android-other-push-services-settings.md#dependencies).

### Other

* Changed the name of the default notification channel to `appmetrica_push`.
   The old default channels won't be deleted.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

# SDK integration

The AppMetrica SDK for Android is distributed as an AAR library.  The library is available in the [Maven repository](https://mvnrepository.com/artifact/io.appmetrica.analytics/analytics).

The steps below explain how to enable and initialize the AppMetrica SDK:

## Step 1. Add the AppMetrica library to your project {#integration}

If you use Gradle to build your app, add the following dependency to your app's Gradle file:

{% list tabs %}

- build.gradle.kts

  ```kotlin translate=no
  dependencies {
      // AppMetrica SDK.
      implementation("io.appmetrica.analytics:analytics:{{ io-appmetrica-analytics-analytics }}")
  }
  ```

- build.gradle

  ```groovy translate=no
  dependencies {
      // AppMetrica SDK.
      implementation 'io.appmetrica.analytics:analytics:{{ io-appmetrica-analytics-analytics }}'
  }
  ```

{% endlist %}

## Step 2. Initialize the AppMetrica library {#initialization}

{% note alert "" %}

During initialization, consider AppMetrica library specifics. For more information, see [How the AppMetrica library works](android-features.md).

{% endnote %}

Initialize the AppMetrica library in your app. To do this, extend the `Application` class and override the `onCreate()` method as follows:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class YourApplication : Application() {
      override fun onCreate() {
          super.onCreate()
          // Creating an extended library configuration.
          val config = AppMetricaConfig.newConfigBuilder(API_KEY).build()
          // Initializing the AppMetrica SDK.
          AppMetrica.activate(this, config)
      }
  }
  ```

- Java

  ```java translate=no
  public class YourApplication extends Application {
      @Override
      public void onCreate() {
          super.onCreate();
          // Creating an extended library configuration.
          AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY).build();
          // Initializing the AppMetrica SDK.
          AppMetrica.activate(this, config);
      }
  }
  ```

{% endlist %}

{% cut "What is the API key?" %}

{{ api-key }}

{% endcut %}

When initializing a library with an extended startup configuration, [logging](android-logs.md) is enabled.

## Step 3. (Optional) Configure location detection {#location}

Location detection helps you understand where your users are located geographically. By default sending device location is disabled, but can be enabled in the startup configuration. For details, see [{#T}](android-operations.md#track-location).

## Step 4. (Optional) Configure sending of events, profile attributes, and revenue (#send)

To collect information on user actions in the app, set up sending your own events. For more information, see [Sending your own events](../../../data-collection/about-events.md).

To collect information about users, set up sending profile attributes. For more information, see [Profiles](../../../data-collection/about-profiles.md).

{% note info "" %}

Unlike events, a profile attribute can take only one value. When you send a new attribute value, the old value is overwritten.

{% endnote %}

To track in-app purchases, set up Revenue sending. For more information, see [In-App purchases](../../../data-collection/about-revenue.md).

## Step 5. Test the library operation {#test}

{% note alert "" %}

Before testing the library, ensure that the SDK is initialized in compliance with [recommendations](android-features.md#recommendations).

{% endnote %}

Before starting testing, we recommend setting up [data transmission to an additional API key](android-operations#reporter-different-apikey) or [adding an app with a new API key](https://appmetrica.yandex.{{ domain }}/about). This will help you separate test data from your core statistics.

To test how the library works:

1. Start the app with the AppMetrica SDK and use it for a while.
2. Make sure your device is connected to the internet.
3. In the AppMetrica interface, make sure that:
   - There is a new user in the [Audience](../../../mobile-reports/audience-report.md) report.
   - The number of sessions in the **Engagement** → **Sessions** report has increased.
   - There are events and profile attributes in the [Events](../../../mobile-reports/events-report.md) and [Profiles](../../../mobile-reports/profile-report.md) reports.

## Learn more {#learn-more}

- [Sending a custom event](android-operations.md#report-event)
- [Sending profile attributes](android-operations.md#send-attribute-profile)
- [Sending E-commerce events](android-operations.md#send-ecommerce)
- [Sending Revenue data](android-operations.md#send-revenue)
- [Sending Ad Revenue data](android-operations.md#send-adrevenue)
- [How do I enable user location sending?](../../../troubleshooting/troubleshooting.md#region)
- [How can I make sure that I have the latest versions of the Android libraries installed?](../../../troubleshooting/troubleshooting.md#newest-android-version)

## Troubleshooting {#faq}

- [Number of sessions staying the same](android-errors.md#session)
- [No events in the report](android-errors.md#events)
- [Error adding a library to a project](android-errors.md#add-in-project)
- [Invalid duration of user session at manual tracking](android-errors.md#listen-root)
- [High power consumption by the AppMetrica library](android-errors.md#power)
- [Code conflict when using automatic collection of Ad Revenue data for Fyber](android-errors.md#fyber-unsupport-adrevenue)
- [My problem is not listed](android-errors.md#not-found)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

# Disabling automatic collection of Ad Revenue data

{% note alert %}

Automatic Ad Revenue data collection is not supported for Fyber. If you enable it in versions 6.4.0 to 7.0.0, you encounter a [conflict in the code](analytics/android-errors.md#fyber-unsupport-adrevenue).

{% endnote %}

Automatic collection of Ad Revenue data is moved to the `io.appmetrica.analytics:analytics-ad-revenue` dependency. The `io.appmetrica.analytics:analytics-ad-revenue` library version should correspond to the `io.appmetrica.analytics:analytics` library version.

To disable automatic collection of Ad Revenue data, exclude the following module from the list of dependencies:

{% list tabs %}

- build.gradle.kts

  ```kotlin translate=no
  configurations.configureEach {
      exclude(group = "io.appmetrica.analytics", module = "analytics-ad-revenue")
  }
  ```

- build.gradle

  ```groovy translate=no
  configurations.configureEach {
      exclude group: 'io.appmetrica.analytics', module: 'analytics-ad-revenue'
  }
  ```

{% endlist %}

Automatic collection is currently supported for ironSource. To disable automatic collection of Ad Revenue data from ironSource, exclude the `io.appmetrica.analytics:ad-revenue-ironsource-v7` module.

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

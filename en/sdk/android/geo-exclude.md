# Excluding geo from the list of dependencies

Geo features were added to a separate dependency: `io.appmetrica.analytics:analytics-location`. It contains a dependency on `com.google.android.gms:play-services-location:19.0.1` used to get locations. The `io.appmetrica.analytics:analytics-location` library version should correspond to the `io.appmetrica.analytics:analytics` library version.

If you need to disable geo, for example, for certain app categories to meet Google Play policies, exclude the module from the list of dependencies:

{% list tabs %}

- build.gradle.kts

   ```kotlin translate=no
   configurations.configureEach {
       exclude(group = "io.appmetrica.analytics", module = "analytics-location")
   }
   ```

- build.gradle

   ```groovy translate=no
   configurations.configureEach {
       exclude group: 'io.appmetrica.analytics', module: 'analytics-location'
   }
   ```

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

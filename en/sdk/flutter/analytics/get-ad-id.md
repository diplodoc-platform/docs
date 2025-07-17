# Getting advertising IDs

An advertising ID is a unique Google Play service identifier for displaying ads to users who agree to see personalized ads. The user can disable the personalization of ads or reset the ID in settings. In this case, advertising networks won't be able to use it to select relevant ads. The accuracy of traffic attribution will also decrease significantly.

For more information about getting advertising IDs, see the [page](../../android/get-ad-id.md).

## Excluding the library of advertising IDs from the list of dependencies {#exclude}

The described method only works for the plugin version 1.0.0 and higher.

If you don't want to get advertising IDs (for example, for children's apps), add the following lines to the `android/app/build.gradle` file:

```java translate=no
configurations {
    all*.exclude group: 'com.yandex.android', module: 'mobmetricalib-identifiers'
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

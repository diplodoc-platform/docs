# User profile

A user profile describes an individual application user as a set of attributes, such as name, gender, age, and so on. AppMetrica lets you collect this information and analyze it in [profile reports](../mobile-reports/profile-report.md), or use profile attributes to segment other reports.

{% cut "Why do I see multiple profiles for a single user?" %}

Most likely, you didn't provide the user profile ID when initializing the library. In this case, the AppMetrica SDK creates a technical profile with an ID of `appmetrica_device_id`. Calling the `setUserProfileID` method with the new ID creates a new profile, yet the technical profile still remains.

To prevent the creation of a technical profile, tweak how you send the ID when initializing the library using the extended config. On [Android](../sdk/android/analytics/android-operations.md#initialize), you can do that by calling the `withUserProfileID` method; on [iOS](../sdk/ios/analytics/ios-operations.md#initialize), edit the `userProfileID` property.

{% endcut %}

{% note alert "" %}

Unlike event attributes, a profile attribute can take only one value. When you send a new attribute value, the old value is overwritten.

{% endnote %}

There are two types of attributes in AppMetrica:

- System attributes: The attributes that the AppMetrica SDK detects automatically, such as the information about a device, app, and location or other data.

- Custom attributes: The attributes that define user characteristics, such as their gender, age, subscription type, number of levels completed, and so on. To collect this data, you need to configure sending attributes in the AppMetrica SDK. For more information, see [User profile attributes](profile-attributes.md).

System and custom attributes are displayed in the [profile card](../mobile-reports/profile-list.md) and available for grouping data in [profile reports](../mobile-reports/profile-report.md).

## Set up sending profile attributes {#profile-settings}

You can configure the AppMetrica SDK to send predefined and custom profile attributes. Predefined attributes are already defined in the SDK and have a special format of sending. To send your own custom attributes, you must add the attribute in the application settings.

{% note alert "" %}

Do not pass personal or confidential user information in profile attributes.

{% endnote %}

This section explains the steps for setting up AppMetrica to send attributes:

### Step 1. Add an attribute in the app settings {#ui-settings}

1. In the AppMetrica interface, go to the app settings from the menu on the left.
1. Open the **Profile attributes** tab.
1. In the **Custom** section enter the name of the new attribute in the corresponding field.
1. Select a variable type from the drop-down list and click **Add**.

There is a list of all attributes of the app and their status in the **Profile attributes** settings section. To stop collecting an attribute and remove it from reports, click **{{ to-archive }}**.

### Step 2. Setting up the attribute values sending in AppMetrica SDK {#sdk-settings}

{% note alert "" %}

AppMetrica doesn't display `predefined attributes` in the web interface if [ProfieId](profile-attributes.md#pre-defined) sending isn't configured.

{% endnote %}

Examples of sending profile attributes on various platforms:

- [Android](../sdk/android/analytics/android-operations.md#send-attribute-profile)
- [iOS](../sdk/ios/analytics/ios-operations.md#send-attribute-profile)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#send-attribute-profile)
- [React Native](../sdk/react-native/analytics/react-native-operations.md#send-attribute-profile)
- [Unity](../sdk/unity/analytics/unity-operations.md#send-attribute-profile)

## Learn more {#learn-more}

- [User profile](about-profiles.md)
- [User profile attributes](profile-attributes.md)
- [Profiles report](../mobile-reports/profile-report.md)
- [Profile list](../mobile-reports/profile-list.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

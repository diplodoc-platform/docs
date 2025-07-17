# User profile attributes

Custom attributes define the characteristics of the user such as gender, age, type of subscription, number of levels, etc. They are displayed in the reports and profiles can be used to segment other reports. To collect custom attributes, you should configure sending in the  AppMetrica SDK. For more information, see [{#T}](about-profiles.md#profile-settings).

AppMetrica has predefined and custom attributes.

## Predefined attributes {#pre-defined}

Attributes that are specific to users of any application and already defined to the AppMetrica SDK:

**ProfileId**

:   User profile ID. Takes the value of an arbitrary string.

    {% note alert "" %}

    AppMetrica doesn't display predefined attributes in the web interface if `ProfieId` sending isn't configured.

    {% endnote %}

**Gender**

:   Gender of the user profile. Possible values: `male`, `female`, `other`.

**Age**

:   Date of birth or age of the user profile.

**Notifications enabled**

:   Status of user profile notifications. It indicates whether the user has enabled notifications.

**Name**

:   The name of the user profile.

    {% note info "" %}

    AppMetrica also has a system **Gender** and **Age** attributes, which are detected automatically using the [Crypta] technology(https://yandex.ru/company/technologies/crypta).

    {% endnote %}

To collect predefined profile attributes, you should configure their sending in the AppMetrica SDK. For more information, see [{#T}](about-profiles.md#profile-settings).

## Custom attributes {#custom}

Attributes that are not defined in the SDK and may differ for different types of applications. The name and type of custom attributes are set manually in the application settings.

AppMetrica lets you configure sending of up to 100 custom attributes of the following types:

**String**

:   Takes the value of an arbitrary string. For example, subscription type: `Free`, `Trial`, `Premium`. 

**Number**

:   Takes a numeric value. For example, number of widgets on the screen: `1`, `2`, `3`, `4`. 

**Bool**

:   Takes the value of binary logic. For example, paid subscription: `true`, `false`. 

**Counter**

:   Performs the adding or subtracting operation. For example, number of completed levels: `+1`. 

To collect your own custom profile attributes, you must add them in the app settings and configure sending in the AppMetrica SDK. For more information, see [{#T}](about-profiles.md#profile-settings).

## Learn more {#learn-more}

- [User profile](about-profiles.md)
- [Profiles report](../mobile-reports/profile-report.md)
- [Profile list](../mobile-reports/profile-list.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

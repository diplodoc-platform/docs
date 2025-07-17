# Launching a push campaign

Before you create a push campaign, make sure that you have configured push notifications and integrated the AppMetrica Push SDK. For more information, see [Push notifications](index.md).

To create a push campaign in AppMetrica, go to the **Push campaigns** section. Click **Create Push** in the upper-left corner of the page. Complete the steps below.

## Step 1. Choose the audience {#audience}

1. Enter a name for the campaign and select the app in the drop-down list.
2. Enable the option Silent Push for sending [silent push notifications](*silent-push).
3. Use the [standard AppMetrica segments](../mobile-reports/segmentation.md) to define the audience that you are planning to send notifications to. Under the segmentation menu, you can see the number of users who will receive notifications divided by platform and language.
   The number of users shown in the push campaign settings might differ from the number of active users in the selected segment.

   {% cut "Why the numbers don't match" %}

   AppMetrica uses the device's push token for sending push notifications. The AppMetrica Push SDK ([Android](../sdk/android/push/quick-start.md) | [iOS](../sdk/ios/push/quick-start.md)) sends the push token to the server when the app starts.

   This means that the segment includes users who have the app version installed with the integrated AppMetrica Push SDK library, and who have started the app at least once. Users can also disable push notifications in the app. These users aren't included in the push campaign audience.

   {% endcut %}

4. Click **Composer** to go to the next step.

## Step 2. Create a push notification {#notification}

Use the **Composer** to create a push notification. To create a notification for a certain platform, change the setting to **On** across from the platform name.

{% note warning "" %}

When creating notifications, pay special attention to the [restrictions](#restrictions).

{% endnote %}

Common fields that are available to all platforms:

- **Title** — The title of the push message. It supports [Emojis](https://en.wikipedia.org/wiki/Emoji).
- **Text**  — You can enter the text in multiple languages, if necessary. The list of languages is based on data about the language set on user devices. The notification text supports [Emojis](https://en.wikipedia.org/wiki/Emoji).
- **Default language** — The language to use for the notification text if there isn't a text available in the language set on the user's device. For example, a push notification is sent to a device set to Turkish, but the **Text** field doesn't contain Turkish. In this case, you can set the default language to English, and the user will get a notification in English.
- **Actions** — The action to perform when the notification is opened. There are several options:
   - **Open application** (by default).
   - **URL** — Open the specified URL in the browser.
   - **Deeplink** — Open a [deeplink](*deeplink*) to a specific screen in the app. You can use a deeplink that is already defined in the app settings, or create a new one using the **New link** button.
- Test on the device — Sends the configured push message to the specified test device. Select a test device from the list or create a new one and click **Test**.
   Also note the additional fields that are specific to each platform:

{% cut "Android" %}

- **Icon resource ID** — The name of the resource for your app icon in the standard `/res/drawable` directory. The icon is shown in the notification bar. If you leave this field empty, the standard app icon is used.
- Background of icon — color of the icon. It is specified as a string in the format of the [hex code](https://ru.wikipedia.org/wiki/Цвета_HTML) `#AARRGGBB`. By default, the icon background is transparent.
- Image URL — You can display an image next to the notification text. Specify a link to the image that you want to display (for example, `http://example.com/image/pic1.png`).
- Big banner picture — Full-size (full-width) image of the notification. Expands vertically if you pull the notification from top to bottom. Specify a link to the image that you want to display (for example, `http://example.com/image/pic1.png`).
- Push notification sound — The sound played when the message is delivered on the user's device. Possible values:
   - **Default** — The sound will be played in accordance with the mode set on the device.
   - **Sound disabled** — The notification will come to the device without any sound.
- **Vibration** — Enables or disables the vibration when a notification is received.
- **LED-indicator** — The color of the LED. It is specified as a string in the format of the [hex code](https://ru.wikipedia.org/wiki/Цвета_HTML) `#RRGGBB`.
- **Push notification priority** — The push notification priority. The platform determines the priority of messages and takes appropriate actions: interrupts the user (displays a message on the screen), or does not notify the user about the message. On different devices, priority is interpreted differently.
- **Expiration time** — The length of time to continue trying to deliver the notification to the user's device. If this time expires and the device is still unavailable (for example, it doesn't have internet access), the notification isn't delivered. By default, the time is unrestricted.
- **Channel** — Push notification channel. If the channel is not specified, the default channel is used. Available for Android 8 or higher. For more information about channels, see [Android documentation](https://developer.android.com/training/notify-user/channels).

{% endcut %}

{% cut "iOS" %}

- **Badge** — The number that will appear on the app icon on the desktop when a notification is received.
- **Expiration time** — The length of time to continue trying to deliver the notification to the user's device. If this time expires and the device is still unavailable (for example, it doesn't have internet access), the notification isn't delivered. By default, the time is unrestricted.
- **Push notification sound** — The sound played when the message is delivered on the user's device. Possible values:
   - **Default** — The sound will be played in accordance with the mode set on the device.
   - **Sound disabled** — The notification will come to the device without any sound.
- **Track delivery** — Enables/disables tracking delivery of push notifications. Enabled by default. If you disable tracking, the number of delivered push notifications in reports is equal to the number of opened messages.

   {% note warning %}

   To track deliveries, you need to set up statistics collection for push notifications.

   {% endnote %}

{% endcut %}

In the **Additional data** field, you can transmit any necessary data as a string value. You can process the data string by using the appropriate AppMetrica Push SDK methods ([Android](../sdk/android/push/quick-start.md) | [iOS](../sdk/ios/push/quick-start.md)).

### Restrictions {#restrictions}

Pay attention to the following restrictions for push notifications:

- Android and iOS: the content of the entire push message should not exceed 3968 bytes.
- Windows: the header size should not exceed 256 bytes, and the text size should not exceed 512 bytes.

{% note info "" %}

Depending on the encoding, 1 character can take from 1 to 4 bytes.

{% endnote %}

### AB testing {#ab-testing}

AppMetrica lets you perform **AB testing** when launching a push campaign. This type of testing can help you assess the effectiveness of different types of notifications within a single campaign, so you can decide which notification provides the best conversion. You can create up to four hypotheses.

One of the hypotheses can be a *control set* (a push notification isn't sent for it). The control set is used for comparing the behavior of users who didn't receive a notification with all those who did.

Statistics for the testing results are available in the report on push campaigns.

## Step 3. Test your push notification {#test}

Testing is available for Android and iOS devices.

We recommend that you check how the notification looks on your test device before you launch the push campaign. To test the notification:

1. Choose an available test device from the drop-down list. If the list is empty, add a device.

   {% cut "Add a new device" %}

   1. Click New device.
   2. Specify the device ID: Google AID, Apple IDFA, IDFV, Huawei OAID, or AppMetrica Device ID.

      {% cut "How to get the Google AID" %}

      Open the "Google settings" app on the device and go to **Ads** in the menu. Google AID is shown on the screen (**Your advertising identifier**).

      {% endcut %}

      {% cut "How to get an Apple IDFA" %}

      1. Install the app [The Identifiers](https://itunes.apple.com/us/app/the-identifiers/id564618183) on the device.
      2. In the app, open the **Raw** tab. Your device's IDFA is shown in **Advertising Identifier**.

      {% note alert %}

      Starting with iOS 14.5, apps can no longer access Apple's IDFA. We recommend using the AppMetrica Device ID instead.

      {% endnote %}

      {% endcut %}

      {% cut "How to get an IDFV" %}

      1. Install your app on a test device
      2. Go to **Data export** → **To a file** and export settings with the `ios_ifv` parameter. When exporting, use filters (for example, filter by **app_version_name**).
      3. Copy the ID in the **ios_ifv** field.

      {% endcut %}

      {% cut "How to get a Huawei OAID" %}

      1. On phones with EMUI, go to **Settings** → **Privacy**  → **Ads and privacy** → **More information**.
      2. Find the ID under the **Your Ad-ID** heading. Copy it.

      {% endcut %}

      {% cut "How to get an AppMetrica Device ID" %}

      1. Install your app on a test device
      2. In the {% if locale == 'ru' %}[AppMetrica web interface](http://appmetrika.yandex.ru/){% endif %}{% if locale == 'en' %}[AppMetrica web interface](http://appmetrika.yandex.com/){% endif %}, go to **Reports** → **Profile list**.
      3. Find your profile. When searching, use segmentation (for example, by build number or device attributes).
      4. Open the profile card and copy the `appmetrica_device_id`.

      {% note alert %}

      You can't use the AppMetrica mobile app to get the AppMetrica Device ID anymore. Use the {% if locale == 'ru' %}[AppMetrica web interface](http://appmetrika.yandex.ru/){% endif %}{% if locale == 'en' %}[AppMetrica web interface](http://appmetrika.yandex.com/){% endif %} instead.

      {% endnote %}

      {% endcut %}

   3. Click **Add**. The device is shown in the drop-down list.

   {% endcut %}

2. Click **Test**. The notification will be sent to the testing device.

{% note info "For iOS devices" %}

You might not receive the push notification in the debug version: the certificate from the **Production** section doesn't work there. For that reason, we recommend testing notifications in the release build.

{% endnote %}

If testing was successful, click **Submit page** to go to the next step.

## Step 4. Check the information and send the push notification {#send}

On the page for submitting the push notification, you can see all the general information about the message that will be sent. Make sure that everything is correct.

To send a push notification:

1. To delay sending the message, go to the **Send schedule** section.
   Click **Later** and select the date and time in the calendar. If you want to adjust the sending time to use the time zone on the device, enable the **use device time zone** option.

2. To launch the campaign, click **Send push to users**.

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*silent-push]: {{ silent-push }}

[*deeplink]: {{ deeplink }}

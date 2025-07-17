# Tracking Facebook^*^ campaigns for Android devices

AppMetrica tracks Facebook[*](*stop) ad campaigns on Android using  [Google Play Install Referrer](technology.md).

For tracking to work, specify **Install Referrer Decryption Key** (Facebook's unique decryption key for attribution data) in the tracker settings for the Facebook[*](*stop) partner. You can create just one tracker for all ad campaigns of one app. It tracks all installations via Install Referrer.

The section below describes the steps for setting up a tracker to track Facebook[*](*stop) ad campaigns:

## Step 1. Get the Install Referrer Decryption Key {#step1}

1. Log in to your [Facebook for Developers](https://developers.facebook.com/) account that has access to the tracked app.
2. Go to the [My apps](https://developers.facebook.com/apps/) section and select the app that you want to set up tracking for.
3. For the selected app, go to {% if locale == 'ru' %}**Settings** → **Basic**{% endif %}{% if locale == 'en' %}**Settings** → **Basic**{% endif %}.
4. At the bottom of the page, in the section with the Android app, copy the **Install Referrer Decryption Key**.

## Step 2. Create a tracker in AppMetrica {#step2}

[Create a tracker](add-tracker.md) in the AppMetrica interface. Pay special attention to the following settings:

1. Go to the **Campaign details** section and choose Facebook[*](*stop) in the **Partner** field.
2. In the **Destination link settings** section, the **Install Referrer** tracking method is selected by default. That's the most accurate tracking method. We don't recommend changing the default method.
3. In the **Destination link settings** section, add the key that you received in the Facebook for Developers account to the **Install Referrer Decryption Key** box.

\* The service is banned in Russia.

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*stop]: \* The service is banned in Russia.

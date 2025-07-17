# In-app App Store subscriptions

<!-- {% note warning %}

This feature is discontinued and will no longer receive updates. Data accuracy not guaranteed.

AppMetrica provides an [alternative tracking technology](https://appmetrica.yandex.com/docs/en/data-collection/apphud/apphud-about) available in certain regions.

{% endnote %} -->

App Store Shared Secret and App Store Server Notifications are used to track App Store subscription statuses. You may skip using App Store Server Notifications to track subscriptions in AppMetrica (for example, if you use an additional subscription status tracking service). However, in this case, subscription data may be delayed by up to 24 hours. Some of the subscription events will also be unavailable.

Address for notifications: [https://apple.inapp.appmetrica.yandex.net](https://apple.inapp.appmetrica.yandex.net).

## App Store Shared Secret {#shared-secret}

AppMetrica uses a key for validating, decrypting the recipe, and checking the subscription status.

1. Open App Store Connect, go to [Apps](https://appstoreconnect.apple.com/apps), and select your app.
2. Go to **Subscriptions** from the **Features** menu on the left.
3. On the page, find the **App-Specific Shared Secret** section and click **Manage**.
4. Create and copy a **Shared Secret**.
5. In the AppMetrica interface, go to your app's settings, the **Revenue** section.
6. Insert the **Shared Secret** for the app in the **App Store Shared Secret** field.

## App Store Server Notifications {#notifications}

Apple enables you to connect "server-to-server" notifications, so you can receive information about subscription status changes. To do this, you need to configure notifications from App Store Server Notifications:

1. Copy the URL for App Store server notifications ([https://apple.inapp.appmetrica.yandex.net](https://apple.inapp.appmetrica.yandex.net)) or that from the AppMetrica interface (**Settings** → **Revenue**).
2. Open App Store Connect, go to [Apps](https://appstoreconnect.apple.com/apps), and select your app.
3. Go to **App Information** from the **General** menu on the left.
4. At the bottom of the page that opens, find the **App Store Server Notifications** section and click **Edit** next to **Production Server URL**.
5. In the **Production Server URL** field, enter the URL from AppMetrica.
6. In the form below, select **Version 2 Notifications** and click **Save**.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

# Configuring an iOS application to send push notifications

The Universal Push Notification Client SSL Certificate is required for sending push notifications to iOS apps. To get this certificate, you need to specify your app's identifier (App ID). You can [create one in the Apple Developer Console](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).

If you already have an App ID, request a certificate.

## Step 1. Request a certificate

1. Open **Keychain Access** on your computer.
2. Go to **Keychain Access** → **Certificate Assistant** → **Request a Certificate From a Certificate Authority** and enter the required information. Pay attention to the password. You will need it when setting up the certificate in the AppMetrica interface.
3. Under **Request is**, enable the **Saved to disk** option and click **Continue**.
4. Save the request file on your computer and click **Done**.

## Step 2. Get a certificate

1. In the Apple Developer Console, go to [Certificates, Identifiers & Profiles](https://developer.apple.com/account/ios/certificate).
2. In the **Certificates** menu, select **All** and go to the **Production** section.
3. Enable the **Apple Push Notification service SSL (Sandbox & Production)** option and click **Continue**.
4. In the **App ID** drop-down list, select the app ID that needs a certificate, and click **Continue**. The selected **App ID** must match your **bundle ID**.
5. Since the certificate request has already been sent, click **Continue**.
6. Click **Choose File**. In the window that opens, select the certificate request file (for example, `example.certSigningRequest`) and click **Choose**, then **Continue**.
7. Click **Download** to download the certificate. Then click **Done**.
8. Double-click the file to install the certificate.

## Step 3. Export a Private Key from the installed certificate

1. Open Keychain Access on your computer and choose **Certificates** in the menu.
2. In the list, select the certificate that you installed.
3. Choose **File** → **Export Items** in the menu. Then enter a name for the file to export and set the format to Personal Information Exchange (P12). Click **Save**.
4. In **Password**, set a password for the key and click **OK**. If you don't set a password, the certificate won't be accepted in the AppMetrica interface.
5. To activate the export, enter the password for your computer. Then click **Allow**. The P12 file is saved on your computer.

## Step 4. Use the Private Key in AppMetrica

1. In the AppMetrica interface, go to the {% if locale == "ru" %}[Applications](https://appmetrika.yandex.ru/application/list){% endif %}{% if locale == "en" %}[Applications](https://appmetrica.yandex.com/application/list){% endif %} section and select the app that you want to run push campaigns for.
2. In the menu on the left, select **Settings**.
3. Go to the **Push notifications** tab.
4. Under **iOS**, click **Choose file** (next to **Universal Push Notification Client SSL Certificate**).
5. In the window that opens, select the key file in P12 format and upload it.
6. In **Password**, enter the password you set when saving the key (step 3).

## See also

- [Connecting the AppMetrica Push SDK](quick-start.md)
- [Launching a push campaign](../../../push/marketing.md)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

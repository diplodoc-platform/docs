{% note alert "" %}

To track Google Ads campaigns, create a link to AppMetrica. For more information, see [Tracking Google Ads campaigns](../adwords-settings.md).

{% endnote %}

A smartLink is a universal tracking URL that automatically changes the destination URL and deeplink depending on the app store.

![](../../../_images/smart-link-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

Available fields:

- **App store**: **Google Play**, **App Store (iOS)**, **GetApps**, **AppGallery**, **Windows Phone Store**, or **Fallback**. The destination URL will lead to the selected app store.

   {% cut "Details" %}

   **GetApps**. If **GetApps** and other stores are selected as the app store and **GetApps** is not installed on the user's Xiaomi device, they won't be redirected to any other app store.

   **AppGallery**. If **AppGallery** and other stores are selected as the app store and **AppGallery** is not installed on the user's Huawei device, they will be redirected to the web version of this store.

   **Google Play**. If only **Google Play** is selected as the app store, a user with a Xiaomi or Huawei device will be directed to **Google Play**.

   {% endcut %}

   Use **Fallback** to create a destination URL for all other types of traffic. For example, you could send the user to a promo page if they clicked on the URL from a non-mobile device.

   {% note info "" %}

   You can choose to select only the **Fallback** option: this will redirect all users to the specified destination URL.

   {% endnote %}

- **Destination URL**: A link that leads to an app in the app store or a page where the user can install the app. For GetApps, specify the deeplink.

- **Deeplink**: A link in `myapp://some_data` format which can be used to send data to the app. Clicking on it will make the app open, provided it is already installed.

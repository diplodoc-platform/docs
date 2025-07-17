# Device identification using a vendor keychain

By storing `device IDs` in the app's keychain, you can uniquely identify a device for custom reports in AppMetrica. However, if a device has multiple apps from the same developer installed, the device might be identified differently in the reports for each of the apps. To avoid this issue, use a vendor keychain.

## Setting up a vendor keychain

1. In the Xcode interface, go to the **Capabilities** section and enable **Keychain Sharing**.
2. In the **Keychain Groups** field, add the group `io.appmetrica`.

  ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/images/common/appmetrica-keychain.png){style="border: solid 1px #cccccc; max-width: 800px;"}

  **Entitlements** of the target after setup:

  ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/images/common/appmetrica-keychain-entitlements.png){style="border: solid 1px #cccccc; max-width: 800px;"}

  After you have set this up, the AppMetrica SDK automatically uses the vendor keychain data.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

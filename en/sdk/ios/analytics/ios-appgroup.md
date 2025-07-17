# Work in App Extensions

AppMetrica supports extensions and can share application identifiers with its extensions. 

## Setup {#setup}

1. Follow [instruction](https://developer.apple.com/documentation/xcode/configuring-app-groups/) and add App Group into your application and extension. 

    {% note alert %}

    The App Group should be available only for application and its extension. Sharing App Group with another application can poison your data.

    {% endnote %}

2. Add the App group into Keychain Access Group according to the [instruction](https://developer.apple.com/documentation/security/sharing-access-to-keychain-items-among-a-collection-of-apps).

    ![](../../../../_images/entitlements.png){style="border: solid 1px #cccccc; max-width: 800px;"}

3. Edit applications Info.plist and add `AMAApplicationGroupIdentifier` key with App Group value (without `Team ID`). 
Extension Info.plist should be untouched. Extension gets App Group from application Info.plist.

    ![](../../../../_images/infoplist.png){style="border: solid 1px #cccccc; max-width: 800px;"}

## Deep into AppMetrica {#how-it-works}

Application and extension store identifiers in their private file storage (private keychain) and shared file storage (shared keychain and vendor keychain). 

Application and extensions try to read all storages and choose most preferred identifiers: application prefers private storages, extension prefers shared storages. If all storages are empty, new identifiers are generated. Then the identifiers are written to the remaining storages.

## Migration from separated AppMetrica to App Group support {#migration-to-appgroup}

If AppMetrica has already been configured in the extensions, the new version will use the application's identifiers. This will cause the existing data to become invalid.

In some cases (for example, if the extension was launched before the application), anomalies in the analytical data are possible due to the loss of identifiers in the extensions and subsequent synchronization in the main application.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

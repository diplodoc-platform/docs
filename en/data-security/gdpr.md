# GDPR compliance

The General Data Protection Regulation (GDPR) regulates the collection and processing of personal information belonging to citizens of the European Economic Area. It is intended to improve data privacy and require transparency for all steps involved in collecting, storing, and processing information in the internet. The legislation is effective as of May 25, 2018.

To meet the GDPR requirements, the following is implemented in AppMetrica:

**Privacy of app users**

:   All data processed by AppMetrica is non-personalized. AppMetrica reports only display technical data. They can't be used to identify the user.

**Transparency of data processing**

:   The procedures for collecting, storing, and processing data are described in detail in a [Data Processing Agreement](https://yandex.ru/legal/metrica_agreement/).

**Ability to disable data collection before the user's consent is obtained**
:   To keep data from being collected before the user consents, the AppMetrica SDK allows you to disable sending statistics on the client side ([Android](../sdk/android/analytics/android-operations.md) | [iOS](../sdk/ios/analytics/ios-operations.md)).

## How to comply with the GDPR {#to-do}

To make your app meet GDPR requirements:

1. Make sure that your app's Privacy Policy clearly states that you're using AppMetrica.
1. Carefully study and accept the [Data Processing Agreement](https://yandex.ru/legal/metrica_agreement/). It describes the procedures for collecting, storing, and processing data.

  ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/gdpr-agreement.png){style="border: solid 1px #cccccc; max-width: 800px;"}

  If you have any questions about the Agreement, contact support from the [feedback form](../troubleshooting/feedback-new.md).

## See also

- [ISO/IEC 27001 compliance](iso-27001.md)
- [Masking the IP address](ip-masking.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

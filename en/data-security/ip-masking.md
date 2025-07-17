# Masking IP addresses

You might need IP masking in order to meet the requirements for personal data security, including privacy policies on third-party resources and federal laws.

By default, AppMetrica stores the full IP address of users. They are used to determine a user's location more precisely, but aren't shown in any AppMetrica reports.

If you enable IP address masking, Yandex.Metrica disguises the address as soon as it's technically possible at the earliest stages of data collection. When Yandex.Metrica receives the data, the last [octet](https://clck.ru/CyWcY) of an IPv4 address or the last 64 bits of an IPv6 address are replaced with zeros. For example, 192.0.2.2 changes to 192.0.2.0.

## Enabling IP masking {#how-to-enable}

To enable IP address masking:

1. Open the app settings in AppMetrica.
2. Enable **Do not store full IP addresses of users from the EU**.

  ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/gdpr-agreement.png){style="border: solid 1px #cccccc; max-width: 800px;"}

### See also

- [GDPR compliance](gdpr.md)
- [ISO/IEC 27001 compliance](iso-27001.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

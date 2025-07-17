# Profile attributes

Transmits user parameters.

Usage example: You can send user parameters to the Post API to supplement user profiles and use this data for audience-based segmentation. For example, add an attribute indicating that the user is a loyalty program member.

Event properties can be passed in parameters or in the body of the request. When you pass data in the body, you should add `.csv` to the URL of the request. For more information, see [Sample request](#sample).

To bind an event to a user, you should use one of the following fields in the API request:

- `profile_id`
- `appmetrica_device_id`

{% note alert %}

The Post API has restrictions on loading data. For more information, see [Restrictions](restrictions.md).

{% endnote %}

## Request format

```
POST {{ api-url }}/logs/v1/import/profiles
  ? post_api_key=<string>
  & application_id=<int>
  & profile_id=<string>
  & attributes=<>
```

#|
|| `post_api_key`* | {{ post_api_key }} ||
|| `application_id`* | {{ application_id }} ||
|| `profile_id`* | {{ post-profile_id }}

{% note alert %}

Do not pass the value with the `appmetrica_device_id` parameter. The server accepts only one of these parameters.

{% endnote %}

||
|| `attributes`* | A set of custom attribute values in `{key:value}` format. Possible value types: string, number, bool, or counter. If the value of the passed attribute is already written for the profile, it will be overwritten with a new one. Former attribute values will be deleted. Learn more about [User profile attributes](../../data-collection/profile-attributes.md).

{% note alert %}

To collect custom profile attributes, add them in the app settings. To do this, open the app page, select **Settings**, and click **Profile attributes**.

{% endnote %}
||
|#

## Response codes

| Code | Description |
| ----- | ----- |
| 200 | Data has been uploaded successfully. |
| 403 | The request omitted an authorization header, or an invalid token was specified. |
| 400 | One or more required parameters were missing in the request. |

## Sample request {#sample}

{% list tabs %}

- Sending data in the request body

  ```http translate=no
  POST /logs/v1/import/profiles.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Connection: close

  application_id,profile_id,attributes
  1234567890,1234567890abcdef,"{""string_attribute_name"":""string_value"",""number_attribute_name"":1234,""bool_attribute_name"":true,""counter_attribute_name"":-1}"
  ```

- Sending data in request parameters

  ```http translate=no
  POST /logs/v1/import/profiles?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012&application_id=1234567890&profile_id=1234567890abcdef&attributes={"string_attribute_name":"string_value","number_attribute_name":1234,"bool_attribute_name":true,"counter_attribute_name":-1} HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 0
  Connection: close
  ```

{% endlist %}

You can only use the Post API to change the user's [custom](../../data-collection/profile-attributes.md#custom) attributes. To deliver [predefined](../../data-collection/profile-attributes.md) attributes, use the AppMetrica SDK. For more information, see [{#T}](../../data-collection/about-profiles.md#profile-settings).

## Other Post API methods {#other-methods}

- [Uploading events](post-import-events.md)
- [Uploading In-App Revenue events](post-revenue.md)
- [Uploading Ad Revenue events](post-adrevenue.md)
- [Uploading E-commerce events](post-ecommerce.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

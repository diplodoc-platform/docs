# Introduction

You can use the {% if locale == 'ru' %}[AppMetrica](http://appmetrika.yandex.ru/){% endif %}{% if locale == 'en' %}[AppMetrica](http://appmetrica.yandex.com/){% endif %} API to:

- Manage your apps without using the web interface.
- Get app statistics (the number of users, devices, and so on).
- Generate reports, including segmented reports.

To access the AppMetrica API, you must [get authorization using an OAuth token](intro/authorization.md). You must transmit the access token in every API request.

To demonstrate the features of the API, the reference guide provides examples of accessing the service. The methods in the examples return sample data that all users can view.

## Structure of the API {#structure}

The API has the following parts:

- The [Management API](management/intro.md) for adding, editing, and deleting apps.
- The [Reporting API](api_v1/intro.md) for getting app statistics.
- The [Logs API](logs/about.md) for getting raw data about your application.
- The [Data Stream API](datastream/about.md) for exporting data as CSV or JSON files.
- [Post API](post/about.md) for uploading event information.
- The [Push API](push/about.md) for creating push campaigns.

## Versioning {#version}

All parts of the AppMetrica API support versioning. Each version has a specific identifier (v1, v2, and so on). When a new version of the API is released, the previous version continues functioning to support backward compatibility.

If you are just getting started with the API, use the latest version. If you are already using previous versions of the API, we recommend gradually migrating to the latest version, since older versions are supported for a limited time.

When making API requests, always specify the version you want to work with.

```
{{ api-url }}/stat/v1/data?id=...
{{ api-url }}/stat/v2/data?id=...
```

## Resources {#recource}

The AppMetrica API is built on REST principles.

Everything that can be managed via the API is represented by resources: statistics, the list of counters, the counter itself, counter goals and each specific goal, counter access, and so on.

So a resource is an integral part of the system that you can work with:

- Read the contents and current status of the resource (GET).
- Modify the contents and status and write it to the resource (PUT).
- Delete the resource (DELETE).
- Perform special actions, such as adding new elements to a list (POST).

Each resource has its own unique URL. All actions are executed by the corresponding HTTP methods at the resource URLs.

### See also

- [Representational State Transfer (Wikipedia, english version)](http://en.wikipedia.org/wiki/Representational_State_Transfer)
- [REST (Wikipedia, Russian version)](http://ru.wikipedia.org/wiki/REST)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

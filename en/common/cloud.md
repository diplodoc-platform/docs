---
noIndex: true

content: noindex
name: robots
---

# Exporting data to Yandex Cloud

{% note alert %}

Data export is temporarily unavailable for new users.

{% endnote %}

If you use [Yandex Cloud](https://cloud.yandex.ru/) and [Managed Service for ClickHouse](https://cloud.yandex.ru/services/managed-clickhouse), you can export data from AppMetrica to your cluster. You can use the data, for example, to create your own reports in [Yandex DataLens](https://cloud.yandex.ru/services/datalens).

Data can be exported in real time: export runs on a regular basis.

This section below describes the steps for configuring export:

## Step 1. Check the ClickHouse cluster settings {#check-zookeeper}

1. Ensure that your ClickHouse cluster has two or more hosts. This is necessary for [replication](https://cloud.yandex.ru/docs/managed-clickhouse/concepts/replication).
   If the cluster is with a single host, add one or more hosts.

2. Ensure that the **Access from Metrica and AppMetrica** option is enabled in the cluster settings.
3. _(Optional)_ To create reports in Yandex DataLens, ensure that the **Access from the DataLens** option is enabled in the cluster settings.

{% note info %}

The **User management via SQL** option is currently unavailable.

{% endnote %}

## Step 2. Create a service account and an authorized key {#create-service-account}

1. Create a service account in the Yandex Cloud console. When creating select a role **editor**.

   For more information, see [Creating a service account](https://cloud.yandex.ru/docs/iam/operations/sa/create) in the Yandex Cloud Help.

2. Create an authorized key. After creating, save the secret part of the key, for example, in a text file. You need it to link your service account to AppMetrica.

   For more information, see [Creating an authorized key](https://cloud.yandex.ru/docs/iam/operations/authorized-key/create) in the Yandex Cloud Help.

## Step 3. Start exporting process {#create-an-export}

{% note alert %}

When the export is running, you cannot change the cluster configuration. To change the configuration, stop all running export processes, change the configuration, and start the export again.

{% endnote %}

1. In the AppMetrica interface, click **{{data-export}}** → **{{upload-cloud}}**.
2. On the **Yandex Cloud data exports** page, click **Create new export**.
3. Link your Yandex Cloud service account To do this, in the **Service account** field click the **Create** button. In the window that opens, specify the following:

    {% cut "Name" %}

    Enter a name.

    {% endcut %}

    {% cut "Service account id" %}

    1. Open your folder in Yandex Cloud.
    2. Go to the **Service accounts** page by using the menu on the left.
    3. Click on the service account you created, for example, **appmetrica**.
    4. In the **Overview** section, copy the **ID** value.

    ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/cloud_service-account.png){style="border: solid 1px #cccccc; max-width: 800px;"}

    {% endcut %}

    {% cut "Public key id" %}

    5. Open your folder in Yandex Cloud.
    6. Go to the **Service accounts** page by using the menu on the left.
    7. Click on the service account you created, for example, **appmetrica**.
    8. In the **Authorized keys** section, copy the**ID** value.

    ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/cloud_open-account.png){style="border: solid 1px #cccccc; max-width: 800px;"}

    {% endcut %}

    {% cut "Private key" %}

    The key that you saved when creating an authorized key.

    {% endcut %}

    {% cut "Folder ID" %}

    9. Open the Yandex Cloud console.
    10. Copy the ID of your folder.

    ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/images/common/cloud_console.png){style="border: solid 1px #cccccc; max-width: 800px;"}

    {% endcut %}

    Click **Create**.

4. Select the date period to export. If the **Realtime** option is enabled, the export process is run regularly.
5. In the field **Event fields** select the parameters to export.

   For more information about event parameters, see the Logs API [available endpoints](../mobile-api/logs/endpoints.md#events) .

6. In the **Cluster** field select the cluster to export. It creates a table with exported parameters.
7. Click the **Launch export** button.

{% note info %}

If you want to create a [MaterializedView](https://clickhouse.tech/docs/en/engines/table-engines/special/materializedview/) based on the exported table, do the following before creating the MaterializedView:

1. Start exporting data to the cluster. This creates a user named `appmetrica_export_user` with certain permissions.
2. In the Yandex Cloud interface, go to the folder page and select **Managed Service for ClickHouse**.
3. Click on the name of the appropriate cluster and select the **Users** tab.
4. Grant the `appmetrica_export_user` the rights to write data to the database where you want to create the MaterializedView. Otherwise, the export is suspended.

{% endnote %}

## Troubleshooting {#troubleshooting}

{% cut "The FAILED_PRECONDITION: operation not permitted when SQL user management is enabled error." %}

The **User management via SQL** option is currently unavailable. Disable the option and restart the export.

{% endcut %}

## Learn more {#learn-more}

- [Events](../mobile-reports/events-report.md)
- [Logs API](../mobile-api/logs/about.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

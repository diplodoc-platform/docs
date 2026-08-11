# Setting up a personal domain and its proxying.

## Creating a repository in Diplodoc

The Quick Start service allows you to create a repository and link it to the external Diplodoc service.

To create basic documentation:

1. Open [Quick Start](https://diplodoc.com/quickstart/).
1. In step 1, authorize in GitHub.
1. In step 2, click **Create** and create a repository in GitHub. As a result, a project named "diplodoc-example" will be created, pre-filled by the Diplodoc team.
1. In step 3, click **Create** and create a project in Diplodoc.
1. After completing the step-by-step instructions, you will receive a message:
  
    ```
    Ключи от каталога с документацией в S3.
    Идентификатор ключа:
    ***********************
    Секретный ключ:
    ***********************

    Сохраните идентификатор и ключ. После закрытия диалога значение ключа будет недоступно. Ключ будет добавлен в созданный репозиторий автоматически.
    ```

1. Wait for the release to complete; the project will be available via the link in step 3 on the [Quick Start](https://diplodoc.com/quickstart) page.

## Preparing Yandex Cloud for domain linking

### Creating an API gateway

1. Register a domain (you can use a [domain registrar](https://yandex.ru/search/?text=доменнный+регистратор)).
1. Authorize or create an account in [Yandex Cloud](https://yandex.cloud/).

    {% note warning %}

    On the [Billing](https://billing.yandex.cloud/accounts) page, make sure you have a [billing account](https://yandex.cloud/ru/docs/billing/concepts/billing-account) connected and it is in the `ACTIVE` or `TRIAL_ACTIVE` status. If there is no billing account, [create one](https://yandex.cloud/ru/docs/billing/quickstart/#create_billing_account).

    {% endnote %}

1. Go to the [Yandex Cloud console](https://console.yandex.cloud/folders/).
1. Open **All services** → **API Gateway**.
    
    {% note info %}

    API Gateway is a simplified server in Yandex Cloud for handling external requests. It is configured using an OpenAPI specification.

    {% endnote %}

1. Click the **Create API gateway** button.

1. Fill in the **Name\*** and description fields. The field with an asterisk is required.

1. In the **Network** field, select `default` or your own option.

1. Fill in the **Specification** field: you can use your own OpenAPI specification or an example.

    {% cut "Example of an OpenAPI specification" %}

    {% note warning %}

    You can use the example OpenAPI specification, but do not forget to change some important parameters, such as: the address of the external domain or the path to which the documentation should be proxied.

    {% endnote %}

    #### OpenAPI Specification

    ```
    openapi: 3.0.0
    info:
      title: Proxy Example
      version: 1.0.0
    servers:
    - url: https://d5dj3947rd2qu5g1lbak.apigw.yandexcloud.net
    - url: example-for-your-domain.net
    paths:
      /путь/{path+}:
        get:
          x-yc-apigateway-integration:
            headers:
              x-real-host: example-for-your-domain.net
              x-docs-proxy-base: docs
              x-docs-project-name: diplodoc-platform--docs
            http_method: get
            query:
              '*': '*'
            type: http
            url: https://diplodoc-platform--docs.viewer.diplodoc.com/{path}
          parameters:
            - name: path
              in: path
              required: false
              schema:
                type: string
    ```

    #### Description of OpenAPI specification parameters

    #|
    || Parameter | Parameter description ||
    || `servers` | Configuring the nested `url` parameters of the `servers` section allows you to specify the address to which the documentation should be proxied.
    To proxy documentation to your domain, configure the nested parameters:

    - The first `url` parameter contains the address where the API Gateway operates — leave the default value.
    - For the second `url` parameter, specify the external domain to which the documentation should be proxied. ||
    || `paths` | Contains a nested rule that allows configuring the response for the parameter `url` from the `servers` section. The parameter `/путь/{path+}:`, nested in the `paths` section, specifies the path where the documentation should be located. 

    {% note info %}

    If you use the OpenAPI specification example, the documentation will be located at `example-for-your-domain.net/docs`.
    
    {% endnote %}||

    || `get` | A nested rule that handles all GET requests. ||
    || `headers` | The section contains service headers. To configure service headers:

    1\. In the parameter `x-real-host:` specify the domain address.
    2\. In the parameter `x-docs-proxy-base:` specify the directory where the documentation will be hosted.
    3\. In the parameter `x-docs-project-name:` specify the project name.||
    || `url` | The parameter, nested in the `get` rule, contains the address to which the documentation is redirected.

    {% note info %} 

    If you use the OpenAPI specification example, the documentation will be redirected to the Diplodoc domain.
    
    {% endnote %}||

    || `parameters` | The section processes the `path` parameter according to the specified rule. ||  
    |#

    {% note warning %}

    To place it in the domain root, change the following in the OpenAPI configuration:

    1. For the parameter `x-docs-proxy-base`, set the value to `' '`.
    1. For the parameter `paths:`, set the value to `/{path+}:`.

    {% endnote %}

    {% endcut %}

1. Click **Create**.
1. If a billing account is not linked, click **Link**.
1. As a result, an API gateway with the status `active` should appear.
1. Now Yandex Cloud can proxy the documentation to its URL.
1. To make proxying to an external domain work, [create a new or upload a personal certificate]((#cert-creating)).

### Creating/uploading a certificate {#cert-creating}

To create or upload a personal certificate:

1. Go to the [console](https://console.yandex.cloud/folders/).
1. Open **All services** → **Certificate Manager**.
1. Click **Create certificate**.
1. On the page, select **Add certificate** → **Certificate from Let's Encrypt**.

    {% note info %}

    If you already have a certificate registered with an external service, you can use it by selecting **User certificate** from the dropdown menu.

    {% endnote %}

1. Fill in the fields **Name\*** and description. The field with an asterisk is required.
1. Specify the **Domains\*** for which the certificate needs to be added. This field is required.
1. In the **Check type** field, select DNS.
1. The created certificate will await confirmation with the status `Validating`.
1. [Confirm](#cert-validating) that you are the domain owner.

### Certificate validation {#cert-validating}

To confirm domain ownership:

1. Go to the [console](https://console.yandex.cloud/folders/).
1. Open **All services** → **Certificate Manager**.
1. Select the created or added certificate.
1. Confirm domain ownership using one of the suggested methods.
1. Domain ownership has been confirmed.
1. [Connect the domain](#connect-domain).

## Linking a domain to Yandex Cloud

### Connecting a domain {#connect-domain}

To complete linking the domain to Yandex Cloud:

1. Open **All services** → **API Gateway**.
1. Select the created API gateway.
1. In the left menu, click **Domains** → **Connect**.
1. Select the created certificate.
1. Specify the domain.
1. Click **Connect**.
1. Setting up proxying to a personal domain is complete.

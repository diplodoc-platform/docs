# Идентификация устройств — vendor keychain

Хранение `device ID` в keychain приложения позволяет однозначно идентифицировать устройство для пользовательских отчетов в AppMetrica. Однако, если на устройстве установлено несколько приложений одного разработчика, то в отчетах по каждому из них одно и то же устройство может идентифицироваться по-разному. Чтобы избежать этого, используйте vendor keychain.

## Настройка

1. В интерфейсе Xcode, в разделе **Capabilities** включите **Keychain Sharing**.
2. Добавьте в поле **Keychain Groups** группу `io.appmetrica`.

  ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/images/common/appmetrica-keychain.png){style="border: solid 1px #cccccc; max-width: 800px;"}

  **Entitlements** таргета после настройки:

  ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/images/common/appmetrica-keychain-entitlements.png){style="border: solid 1px #cccccc; max-width: 800px;"}

  После настройки SDK автоматически использует данные vendor keychain.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

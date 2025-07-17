# Руководство по миграции на версию 3.0.0

## Одновременное использование двух версий AppMetrica SDK {#two-versions}

В одном приложении могут использоваться сразу две версии AppMetrica SDK. Такая ситуация нежелательна. Статистика должна
собираться нормально, хотя допустимы небольшие отклонения. В этом случае возможно некоторое увеличение размера
приложения, так как в составе приложения будут присутствовать два SDK, вместо одного.

{% note alert %}

Категорически не рекомендуется одновременная работа в коде приложения двух версий SDK с одним `API_KEY`. Это не приведет
к сбоям и крэшам в приложении, но вызовет искажение и нарушение статистики. При миграции на `@appmetrica/react-native-analytics`
проверьте, что у вас в `package-lock.json` или в `yarn.lock` нет упоминания `react-native-appmetrica` плагина.

{% endnote %}

## Руководство по миграции {#about-migration}

Руководство содержит примеры, демонстрирующие различия между версиями плагина `2.0.0` и `3.0.0`. В разделе
рассматриваются только те методы, в которых нарушена обратная совместимость.

Для миграции на новую версию выполните следующие шаги:

1. Поменяйте зависимость `react-native-appmetrica` на `@appmetrica/react-native-analytics`. Пример в [разделе про замену зависимостей](#dependencies).
2. Поменяйте импорт в коде. Необходимые изменения указаны в [разделе про импортирование зависимостей](#import).
3. В коде проекта замените те классы и методы, которые были просто переименованы. Необходимые изменения указаны в [разделе про переименования](#rename).

## Замена зависимостей {#dependencies}

{% list tabs %}

- yarn

  ```bash translate=no
  yarn remove react-native-appmetrica && yarn add @appmetrica/react-native-analytics
  ```

- npm

  ```bash translate=no
  npm uninstall react-native-appmetrica && npm install @appmetrica/react-native-analytics
  ```

{% endlist %}

## Импортирование зависимостей {#import}

```javascript translate=no
import AppMetrica from 'react-native-appmetrica';
```
Замените на:
```sh translate=no
import AppMetrica from '@appmetrica/react-native-analytics';
```

## Переименование {#rename}

- Метод `requestAppMetricaDeviceId()` удален. Для получения идентификаторов используйте метод `requestStartupParams()`.
- Метод `setStatisticsSending()` переименован в `setDataSendingEnabled()`.
